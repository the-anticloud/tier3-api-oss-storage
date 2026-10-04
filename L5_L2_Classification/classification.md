# L5 Narrow / L2 General Classification — api-oss-storage
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign object storage: local S3-compatible API for Anticloud artifacts

## L5 Narrow
api-oss-storage specializes in sovereign object storage: local s3-compatible api for anticloud artifacts within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means api-oss-storage is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B is used for intelligent storage tiering: given access patterns, PAX recommends which objects to keep in fast NVMe vs compress to slow storage.

## AIOSS Audit Relevance
Every storage operation (object key + object hash + operation type + encrypted size) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
GDPR Art. 32 (storage encryption), NIST SP 800-111 (storage encryption)
