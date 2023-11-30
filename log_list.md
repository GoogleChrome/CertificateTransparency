# Recognized Logs

The following table includes information about the Certificate Transparency Logs
that are recognized by Chromium. It includes information about who operates the
log, the name the log has been given, and the URL that can be used for logging
certificates or inspecting the certificates that have been logged.

**_Note: The authoritative list is maintained in the [Chromium code base](https://cs.chromium.org/chromium/src/components/certificate_transparency/data/log_list.json). This is merely informational._**

|Log Name                       |Log URL                                       |Log State |MMD    |Temporal Interval Start|Temporal Interval End  |Log Operator    |Contact Info                       |
|-------------------------------|----------------------------------------------|----------|-------|-----------------------|-----------------------|----------------|-----------------------------------|
|Google 'Argon2023' log         | https://ct.googleapis.com/logs/argon2023/    | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-01T00:00:00Z |  Google        |  google-ct-logs@googlegroups.com  |
|Google 'Argon2024' log         | https://ct.googleapis.com/logs/us1/argon2024/| Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  Google        |  google-ct-logs@googlegroups.com  |
|Google 'Xenon2023' log         | https://ct.googleapis.com/logs/xenon2023/    | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-01T00:00:00Z |  Google        |  google-ct-logs@googlegroups.com  |
|Google 'Xenon2024' log         | https://ct.googleapis.com/logs/eu1/xenon2024/| Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  Google        |  google-ct-logs@googlegroups.com  |
|Cloudflare 'Nimbus2023' Log    | https://ct.cloudflare.com/logs/nimbus2023/   | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-01T00:00:00Z |  Cloudflare    |  ct-logs@cloudflare.com           |
|Cloudflare 'Nimbus2024' Log    | https://ct.cloudflare.com/logs/nimbus2024/   | Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  Cloudflare    |  ct-logs@cloudflare.com           |
|DigiCert Yeti2024 Log          | https://yeti2024.ct.digicert.com/log/        | Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  DigiCert      |  ctops@digicert.com               |
|DigiCert Yeti2025 Log          | https://yeti2025.ct.digicert.com/log/        | Usable   | 86400 |  2025-01-01T00:00:00Z |  2026-01-01T00:00:00Z |  DigiCert      |  ctops@digicert.com               |
|DigiCert Nessie2023 Log        | https://nessie2023.ct.digicert.com/log/      | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-01T00:00:00Z |  DigiCert      |  ctops@digicert.com               |
|DigiCert Nessie2024 Log        | https://nessie2024.ct.digicert.com/log/      | Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  DigiCert      |  ctops@digicert.com               |
|DigiCert Nessie2025 Log        | https://nessie2025.ct.digicert.com/log/      | Usable   | 86400 |  2025-01-01T00:00:00Z |  2026-01-01T00:00:00Z |  DigiCert      |  ctops@digicert.com               |
|Sectigo 'Sabre' CT log         | https://sabre.ct.comodo.com/                 | Usable   | 86400 |                       |                       |  Sectigo       |  ctops@sectigo.com                |
|Sectigo 'Mammoth' CT log       | https://mammoth.ct.comodo.com/               | Retired  | 86400 |                       |  2023-01-15 00:00:00Z |  Sectigo       |  ctops@sectigo.com                |
|Let's Encrypt 'Oak2023' log    | https://oak.ct.letsencrypt.org/2023/         | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-07T00:00:00Z |  Let's Encrypt |  sre@letsencrypt.org              |
|Let's Encrypt 'Oak2024H1' log  | https://oak.ct.letsencrypt.org/2024h1/       | Usable   | 86400 |  2023-12-20T00:00:00Z |  2024-07-20T00:00:00Z |  Let's Encrypt |  sre@letsencrypt.org              |
|Let's Encrypt 'Oak2024H2' log  | https://oak.ct.letsencrypt.org/2024h2/       | Usable   | 86400 |  2024-06-20T00:00:00Z |  2025-01-20T00:00:00Z |  Let's Encrypt |  sre@letsencrypt.org              |
|Trust Asia Log2023             | https://ct.trustasia.com/log2023/            | Usable   | 86400 |  2023-01-01T00:00:00Z |  2024-01-01T00:00:00Z |  TrustAsia     |  trustasia-ct-logs@trustasia.com  |
|Trust Asia Log2024-2           | https://ct2024.trustasia.com/log2024/        | Usable   | 86400 |  2024-01-01T00:00:00Z |  2025-01-01T00:00:00Z |  TrustAsia     |  trustasia-ct-logs@trustasia.com  |
