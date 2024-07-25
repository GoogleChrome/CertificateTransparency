# Recognized Logs

The following table includes information about the Certificate Transparency Logs
that are recognized by Chromium. It includes information about who operates the
log, the name the log has been given, and the URL that can be used for logging
certificates or inspecting the certificates that have been logged.

**_Note: The authoritative list is maintained in the [Chromium code base](https://cs.chromium.org/chromium/src/components/certificate_transparency/data/log_list.json). This is merely informational._**

|Log Name                     |Log URL                                        |Log State|MMD  |Temporal Interval Start|Temporal Interval End|Log Operator |Contact Info                   |
|-----------------------------|-----------------------------------------------|---------|-----|-----------------------|---------------------|-------------|-------------------------------|
|Google 'Argon2024' log       |https://ct.googleapis.com/logs/us1/argon2024/  |Usable   |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2025h1' log     |https://ct.googleapis.com/logs/us1/argon2025h1/|Usable   |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2025h2' log     |https://ct.googleapis.com/logs/us1/argon2025h2/|Usable   |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2026h1' log     |https://ct.googleapis.com/logs/us1/argon2026h1/|Qualified|86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2026h2' log     |https://ct.googleapis.com/logs/us1/argon2026h2/|Qualified|86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2024' log       |https://ct.googleapis.com/logs/eu1/xenon2024/  |Usable   |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2025h1' log     |https://ct.googleapis.com/logs/eu1/xenon2025h1/|Usable   |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2025h2' log     |https://ct.googleapis.com/logs/eu1/xenon2025h2/|Usable   |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2026h1' log     |https://ct.googleapis.com/logs/eu1/xenon2026h1/|Qualified|86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2026h2' log     |https://ct.googleapis.com/logs/eu1/xenon2026h2/|Qualified|86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Cloudflare 'Nimbus2024' Log  |https://ct.cloudflare.com/logs/nimbus2024/     |Usable   |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |Cloudflare   |ct-logs@cloudflare.com         |
|Cloudflare 'Nimbus2025'      |https://ct.cloudflare.com/logs/nimbus2025/     |Usable   |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |Cloudflare   |ct-logs@cloudflare.com         |
|DigiCert Yeti2024 Log        |https://yeti2024.ct.digicert.com/log/          |Usable   |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert Yeti2025 Log        |https://yeti2025.ct.digicert.com/log/          |Usable   |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert Nessie2024 Log      |https://nessie2024.ct.digicert.com/log/        |Retired  |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert Nessie2025 Log      |https://nessie2025.ct.digicert.com/log/        |Usable   |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2024h1' Log  |https://wyvern.ct.digicert.com/2024h1/         |Qualified|86400|2024-01-01T00:00:00Z   |2024-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2024h2' Log  |https://wyvern.ct.digicert.com/2024h2/         |Qualified|86400|2024-07-01T00:00:00Z   |2025-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2025h1' Log  |https://wyvern.ct.digicert.com/2025h1/         |Qualified|86400|2025-01-01T00:00:00Z   |2025-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2025h2' Log  |https://wyvern.ct.digicert.com/2025h2/         |Qualified|86400|2025-07-01T00:00:00Z   |2026-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2024h1' Log  |https://sphinx.ct.digicert.com/2024h1/         |Qualified|86400|2024-01-01T00:00:00Z   |2024-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2024h2' Log  |https://sphinx.ct.digicert.com/2024h2/         |Qualified|86400|2024-07-01T00:00:00Z   |2025-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2025h1' Log  |https://sphinx.ct.digicert.com/2025h1/         |Qualified|86400|2025-01-01T00:00:00Z   |2025-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2025h2' Log  |https://sphinx.ct.digicert.com/2025h2/         |Qualified|86400|2025-07-01T00:00:00Z   |2026-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|Sectigo 'Sabre' CT log       |https://sabre.ct.comodo.com/                   |ReadOnly |86400|                       |                     |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2024h1'        |https://sabre2024h1.ct.sectigo.com/            |Usable   |86400|2024-01-01T00:00:00Z   |2024-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2024h2'        |https://sabre2024h2.ct.sectigo.com/            |Usable   |86400|2024-07-01T00:00:00Z   |2025-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2025h1'        |https://sabre2025h1.ct.sectigo.com/            |Usable   |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2025h2'        |https://sabre2025h2.ct.sectigo.com/            |Usable   |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2024h1'      |https://mammoth2024h1.ct.sectigo.com/          |Retired  |86400|2024-01-01T00:00:00Z   |2024-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2024h1b'     |https://mammoth2024h1b.ct.sectigo.com/         |Usable   |86400|2024-01-01T00:00:00Z   |2024-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2024h2'      |https://mammoth2024h2.ct.sectigo.com/          |Usable   |86400|2024-07-01T00:00:00Z   |2025-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2025h1'      |https://mammoth2025h1.ct.sectigo.com/          |Usable   |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2025h2'      |https://mammoth2025h2.ct.sectigo.com/          |Usable   |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Let's Encrypt 'Oak2024H1' log|https://oak.ct.letsencrypt.org/2024h1/         |Usable   |86400|2023-12-20T00:00:00Z   |2024-07-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2024H2' log|https://oak.ct.letsencrypt.org/2024h2/         |Usable   |86400|2024-06-20T00:00:00Z   |2025-01-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2025h1'    |https://oak.ct.letsencrypt.org/2025h1/         |Usable   |86400|2024-12-20T00:00:00Z   |2025-07-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2025h2'    |https://oak.ct.letsencrypt.org/2025h2/         |Usable   |86400|2025-06-20T00:00:00Z   |2026-01-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Trust Asia Log2024-2         |https://ct2024.trustasia.com/log2024/          |Usable   |86400|2024-01-01T00:00:00Z   |2025-01-01T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia Log2025a           |https://ct2025-a.trustasia.com/log2025a/       |Usable   |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia Log2025b           |https://ct2025-b.trustasia.com/log2025b/       |Usable   |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia 'log2026a'         |https://ct2026-a.trustasia.com/log2026a/       |Qualified|86400|2025-12-24T00:00:00Z   |2027-01-08T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia 'log2026b'         |https://ct2026-b.trustasia.com/log2026b/       |Qualified|86400|2025-12-24T00:00:00Z   |2027-01-08T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
