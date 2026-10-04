# Developer Cookbook — api-oss-storage
**Stack:** Python 3.11, AES-256-GCM, SQLite (metadata), mmap, AIOSS_FORMAT
**Domain:** Sovereign object storage: local S3-compatible API for Anticloud artifacts
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```python
from api_oss_storage import SovereignStorage
store = SovereignStorage('./objects/', encryption_key=vault_key, aioss_chain='./storage.aioss')

# Store object
store.put('pax-benchmarks/t4_results.json', data=json_bytes)

# Retrieve
data = store.get('pax-benchmarks/t4_results.json')

# List
for obj in store.list(prefix='pax-benchmarks/'):
    print(f'{obj.key}: {obj.size_bytes} bytes, hash: {obj.content_hash[:16]}')

# Tiering recommendation
tier = store.pax_tier_recommend(pax_model='./pax-27b-q4.gguf')
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every api-oss-storage output:
chain_hash = aioss_append("./api_oss_storage.aioss",
                           result_bytes, "api-oss-storage")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all api-oss-storage operations are logged to api-oss-logging and audited by api-oss-compliance.
