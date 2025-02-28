# Recognized Logs

The following table includes information about the Certificate Transparency Logs
that are recognized by Chromium. It includes information about who operates the
log, the name the log has been given, and the URL that can be used for logging
certificates or inspecting the certificates that have been logged.

**_Note: The authoritative list is maintained in the [Chromium code base](https://cs.chromium.org/chromium/src/components/certificate_transparency/data/log_list.json). This is merely informational._**

|Log Name                     |Log URL                                        |Log State|Log Spec|MMD  |Temporal Interval Start|Temporal Interval End|Log Operator |Contact Info                   |
|-----------------------------|-----------------------------------------------|---------|--------|-----|-----------------------|---------------------|-------------|-------------------------------|
|Google 'Argon2025h1' log     |https://ct.googleapis.com/logs/us1/argon2025h1/|Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2025h2' log     |https://ct.googleapis.com/logs/us1/argon2025h2/|Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2026h1' log     |https://ct.googleapis.com/logs/us1/argon2026h1/|Usable   |RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Argon2026h2' log     |https://ct.googleapis.com/logs/us1/argon2026h2/|Usable   |RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2025h1' log     |https://ct.googleapis.com/logs/eu1/xenon2025h1/|Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2025h2' log     |https://ct.googleapis.com/logs/eu1/xenon2025h2/|Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2026h1' log     |https://ct.googleapis.com/logs/eu1/xenon2026h1/|Usable   |RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Google 'Xenon2026h2' log     |https://ct.googleapis.com/logs/eu1/xenon2026h2/|Usable   |RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Google       |google-ct-logs@googlegroups.com|
|Cloudflare 'Nimbus2025'      |https://ct.cloudflare.com/logs/nimbus2025/     |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |Cloudflare   |ct-logs@cloudflare.com         |
|Cloudflare 'Nimbus2026'      |https://ct.cloudflare.com/logs/nimbus2026/     |Qualified|RFC6962 |86400|2026-01-01T00:00:00Z   |2027-01-01T00:00:00Z |Cloudflare   |ct-logs@cloudflare.com         |
|DigiCert Yeti2025 Log        |https://yeti2025.ct.digicert.com/log/          |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert Nessie2025 Log      |https://nessie2025.ct.digicert.com/log/        |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2025h1' Log  |https://wyvern.ct.digicert.com/2025h1/         |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2025h2' Log  |https://wyvern.ct.digicert.com/2025h2/         |Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2026h1'      |https://wyvern.ct.digicert.com/2026h1/         |Qualified|RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Wyvern2026h2'      |https://wyvern.ct.digicert.com/2026h2/         |Qualified|RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2025h1' Log  |https://sphinx.ct.digicert.com/2025h1/         |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2025h2' Log  |https://sphinx.ct.digicert.com/2025h2/         |Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-07T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2026h1'      |https://sphinx.ct.digicert.com/2026h1/         |Qualified|RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|DigiCert 'Sphinx2026h2'      |https://sphinx.ct.digicert.com/2026h2/         |Qualified|RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |DigiCert     |ctops@digicert.com             |
|Sectigo 'Sabre' CT log       |https://sabre.ct.comodo.com/                   |ReadOnly |RFC6962 |86400|                       |                     |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2025h1'        |https://sabre2025h1.ct.sectigo.com/            |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2025h2'        |https://sabre2025h2.ct.sectigo.com/            |Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2025h1'      |https://mammoth2025h1.ct.sectigo.com/          |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2025-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2025h2'      |https://mammoth2025h2.ct.sectigo.com/          |Usable   |RFC6962 |86400|2025-07-01T00:00:00Z   |2026-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2026h1'      |https://mammoth2026h1.ct.sectigo.com/          |Qualified|RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Mammoth2026h2'      |https://mammoth2026h2.ct.sectigo.com/          |Qualified|RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2026h1'        |https://sabre2026h1.ct.sectigo.com/            |Qualified|RFC6962 |86400|2026-01-01T00:00:00Z   |2026-07-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Sectigo 'Sabre2026h2'        |https://sabre2026h2.ct.sectigo.com/            |Qualified|RFC6962 |86400|2026-07-01T00:00:00Z   |2027-01-01T00:00:00Z |Sectigo      |ctops@sectigo.com              |
|Let's Encrypt 'Oak2025h1'    |https://oak.ct.letsencrypt.org/2025h1/         |Usable   |RFC6962 |86400|2024-12-20T00:00:00Z   |2025-07-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2025h2'    |https://oak.ct.letsencrypt.org/2025h2/         |Usable   |RFC6962 |86400|2025-06-20T00:00:00Z   |2026-01-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2026h1'    |https://oak.ct.letsencrypt.org/2026h1/         |Qualified|RFC6962 |86400|2025-12-20T00:00:00Z   |2026-07-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|Let's Encrypt 'Oak2026h2'    |https://oak.ct.letsencrypt.org/2026h2/         |Qualified|RFC6962 |86400|2026-06-20T00:00:00Z   |2027-01-20T00:00:00Z |Let's Encrypt|sre@letsencrypt.org            |
|TrustAsia Log2025a           |https://ct2025-a.trustasia.com/log2025a/       |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia Log2025b           |https://ct2025-b.trustasia.com/log2025b/       |Usable   |RFC6962 |86400|2025-01-01T00:00:00Z   |2026-01-01T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia 'log2026a'         |https://ct2026-a.trustasia.com/log2026a/       |Usable   |RFC6962 |86400|2025-12-24T00:00:00Z   |2027-01-08T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
|TrustAsia 'log2026b'         |https://ct2026-b.trustasia.com/log2026b/       |Usable   |RFC6962 |86400|2025-12-24T00:00:00Z   |2027-01-08T00:00:00Z |TrustAsia    |trustasia-ct-logs@trustasia.com|
