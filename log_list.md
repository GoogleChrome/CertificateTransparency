# Recognized Logs

The following table includes information about the Certificate Transparency Logs
that are recognized by Chromium. It includes information about who operates the
log, the name the log has been given, and the URL that can be used for logging
certificates or inspecting the certificates that have been logged.

**_Note: The authoritative list is maintained in the [Chromium code base](https://cs.chromium.org/chromium/src/components/certificate_transparency/data/log_list.json). This is merely informational._**

## Qualified Logs

| Log Operator                              | Log Name                                | Log URL                                    | MMD      | Qualified In                          | Current State |
| ----------------------------------------- | --------------------------------------- | ------------------------------------------ | -------- | ------------------------------------- | ------------- |
| [Google](https://www.google.com/)         | Google 'Aviator' Log                    | https://ct.googleapis.com/aviator          | 24 hours | [Chrome 35](https://crrev.com/237785) | Read Only     |
| [Google](https://www.google.com/)         | Google 'Pilot' Log                      | https://ct.googleapis.com/pilot/           | 24 hours | [Chrome 35](https://crrev.com/237785) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert's Certificate Transparency log | https://ct1.digicert-ct.com/log/           | 24 hours | [Chrome 41](https://crrev.com/309831) | Usable        |
| [Google](https://www.google.com/)         | Google 'Rocketeer' Log                  | https://ct.googleapis.com/rocketeer        | 24 hours | [Chrome 43](https://crrev.com/325382) | Usable        |
| [Google](https://www.google.com/)         | Google 'Icarus' Log                     | https://ct.googleapis.com/icarus/          | 24 hours | [Chrome 55](https://crrev.com/429670) | Usable        |
| [Google](https://www.google.com/)         | Google 'Skydiver' Log                   | https://ct.googleapis.com/skydiver/        | 24 hours | [Chrome 55](https://crrev.com/429670) | Usable        |
| [Sectigo](https://sectigo.com/)           | Sectigo 'Mammoth' Log                   | https://mammoth.ct.comodo.com/             | 24 hours | [Chrome 60](https://crrev.com/482145) | Usable        |
| [Sectigo](https://sectigo.com/)           | Sectigo 'Sabre' Log                     | https://sabre.ct.comodo.com/               | 24 hours | [Chrome 60](https://crrev.com/482145) | Usable        |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2020' Log             | https://ct.cloudflare.com/logs/nimbus2020/ | 24 hours | [Chrome 65](https://crrev.com/540254) | Usable        |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2021' Log             | https://ct.cloudflare.com/logs/nimbus2021/ | 24 hours | [Chrome 65](https://crrev.com/540254) | Usable        |
| [Google](https://www.google.com/)         | Google 'Argon2020' Log                  | https://ct.googleapis.com/logs/argon2020/  | 24 hours | [Chrome 65](https://crrev.com/540254) | Usable        |
| [Google](https://www.google.com/)         | Google 'Argon2021' Log                  | https://ct.googleapis.com/logs/argon2021/  | 24 hours | [Chrome 65](https://crrev.com/540254) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2020' Log                 | https://yeti2020.ct.digicert.com/log/      | 24 hours | [Chrome 67](https://crrev.com/559734) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2021' Log                 | https://yeti2021.ct.digicert.com/log/      | 24 hours | [Chrome 67](https://crrev.com/559734) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2022' Log                 | https://yeti2022.ct.digicert.com/log/      | 24 hours | [Chrome 67](https://crrev.com/559734) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2020' Log               | https://nessie2020.ct.digicert.com/log/    | 24 hours | [Chrome 72](https://crrev.com/620903) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2021' Log               | https://nessie2021.ct.digicert.com/log/    | 24 hours | [Chrome 72](https://crrev.com/620903) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2022' Log               | https://nessie2022.ct.digicert.com/log/    | 24 hours | [Chrome 72](https://crrev.com/620903) | Usable        |
| [Google](https://www.google.com/)         | Google 'Xenon2020' Log                  | https://ct.googleapis.com/logs/xenon2020/  | 24 hours | [Chrome 73](https://crrev.com/634940) | Usable        |
| [Google](https://www.google.com/)         | Google 'Xenon2021' Log                  | https://ct.googleapis.com/logs/xenon2021/  | 24 hours | [Chrome 73](https://crrev.com/634940) | Usable        |
| [Google](https://www.google.com/)         | Google 'Xenon2022' Log                  | https://ct.googleapis.com/logs/xenon2022/  | 24 hours | [Chrome 73](https://crrev.com/634940) | Usable        |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2022' Log             | https://ct.cloudflare.com/logs/nimbus2022/ | 24 hours | [Chrome 76](https://crrev.com/666475) | Usable        |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2023' Log             | https://ct.cloudflare.com/logs/nimbus2023/ | 24 hours | [Chrome 76](https://crrev.com/666475) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2023' Log               | https://nessie2023.ct.digicert.com/log/    | 24 hours | [Chrome 76](https://crrev.com/666475) | Usable        |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2023' Log                 | https://yeti2023.ct.digicert.com/log/      | 24 hours | [Chrome 76](https://crrev.com/666475) | Usable        |
| [Google](https://www.google.com/)         | Google 'Xenon2023' Log                  | https://ct.googleapis.com/logs/xenon2023/  | 24 hours | [Chrome 77](https://crrev.com/689620) | Usable        |
| [Google](https://www.google.com/)         | Google 'Argon2022' Log                  | https://ct.googleapis.com/logs/argon2022/  | 24 hours | [Chrome 77](https://crrev.com/689620) | Usable        |
| [Google](https://www.google.com/)         | Google 'Argon2023' Log                  | https://ct.googleapis.com/logs/argon2023/  | 24 hours | [Chrome 77](https://crrev.com/689620) | Usable        |
| [Let's Encrypt](https://letsencrypt.org/) | Let's Encrypt 'Oak2020' Log             | https://oak.ct.letsencrypt.org/2020/       | 24 hours | [Chrome 78](https://crrev.com/703880) | Usable        |
| [Let's Encrypt](https://letsencrypt.org/) | Let's Encrypt 'Oak2021' Log             | https://oak.ct.letsencrypt.org/2021/       | 24 hours | [Chrome 78](https://crrev.com/703880) | Usable        |
| [Let's Encrypt](https://letsencrypt.org/) | Let's Encrypt 'Oak2022' Log             | https://oak.ct.letsencrypt.org/2022/       | 24 hours | [Chrome 78](https://crrev.com/703880) | Usable        |

### Once, but no longer, Qualified Logs

| Log Operator                              | Name                        | Log URL                                    | MMD      | Qualified In                          | Last Accepted SCT            |
| ----------------------------------------- | --------------------------- | ------------------------------------------ | -------- | ------------------------------------- | ---------------------------- |
| [Certly](https://certly.io/)              | Certly.IO Log               | https://log.certly.io                      | 24 hours | [Chrome 43](https://crrev.com/325382) | 15 April 2016 00:00:00 UTC.  |
| [Izenpe](https://www.izenpe.com/)         | Izenpe Log                  | https://ct.izenpe.com                      | 24 hours | [Chrome 44](https://crrev.com/326301) | 30 May 2016 00:00:00 UTC.    |
| [Venafi](https://www.venafi.com/)         | Venafi CT Log Server        | https://ctlog.api.venafi.com/ct/v1         | 24 hours | [Chrome 47](https://crrev.com/349170) | 28 Feb 2017 18:42:26 UTC.    |
| [WoSign](https://www.wosign.com/)         | WoSign Log                  | https://ctlog.wosign.com/                  | 24 hours | [Chrome 54](https://crrev.com/414378) | 12 Feb 2018 23:59:59 UTC.    |
| [StartCom](https://www.startssl.com/)     | StartCom CT Log             | https://ct.startssl.com/                   | 24 hours | [Chrome 54](https://crrev.com/414440) | 12 Feb 2018 23:59:59 UTC.    |
| [CNNIC](https://cnnic.cn/)                | CNNIC CT Log                | https://ctserver.cnnic.cn/                 | 24 hours | [Chrome 53](https://crrev.com/396817) | 18 Sep 2018 00:00:00 UTC.    |
| [DigiCert](https://www.digicert.com/)     | Symantec Log                | https://ct.ws.symantec.com                 | 24 hours | [Chrome 45](https://crrev.com/483625) | 16 Feb 2019 00:00:00 UTC.    |
| [DigiCert](https://www.digicert.com/)     | Symantec 'Vega' Log         | https://vega.ws.symantec.com/              | 24 hours | [Chrome 50](https://crrev.com/376143) | 16 Feb 2019 00:00:00 UTC.    |
| [DigiCert](https://www.digicert.com/)     | Symantec 'Sirius' Log       | https://sirius.ws.symantec.com/            | 24 hours | [Chrome 60](https://crrev.com/481160) | 16 Feb 2019 00:00:00 UTC.    |
| [Google](https://www.google.com/)         | Google 'Argon2018' Log      | https://ct.googleapis.com/logs/argon2018/  | 24 hours | [Chrome 65](https://crrev.com/540254) | Rejected - Shard Expired     |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2018' Log | https://ct.cloudflare.com/logs/nimbus2018/ | 24 hours | [Chrome 65](https://crrev.com/540254) | Rejected - Shard Expired     |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2018' Log     | https://yeti2018.ct.digicert.com/log/      | 24 hours | [Chrome 67](https://crrev.com/559734) | Rejected - Shard Expired     |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2018' Log   | https://nessie2018.ct.digicert.com/log/    | 24 hours | [Chrome 72](https://crrev.com/620903) | Rejected - Shard Expired     |
| [Cloudflare](https://www.cloudflare.com/) | Cloudflare 'Nimbus2019' Log | https://ct.cloudflare.com/logs/nimbus2019/ | 24 hours | [Chrome 65](https://crrev.com/540254) | Rejected - Shard Expired     |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Yeti2019' Log     | https://yeti2019.ct.digicert.com/log/      | 24 hours | [Chrome 67](https://crrev.com/559734) | Rejected - Shard Expired     |
| [DigiCert](https://www.digicert.com/)     | DigiCert 'Nessie2019' Log   | https://nessie2019.ct.digicert.com/log/    | 24 hours | [Chrome 72](https://crrev.com/620903) | Rejected - Shard Expired     |
| [Google](https://www.google.com/)         | Google 'Argon2019' Log      | https://ct.googleapis.com/logs/argon2019/  | 24 hours | [Chrome 65](https://crrev.com/540254) | Rejected - Shard Expired     |
| [Google](https://www.google.com/)         | Google 'Xenon2019' Log      | https://ct.googleapis.com/logs/xenon2019/  | 24 hours | [Chrome 73](https://crrev.com/634940) | Rejected - Shard Expired     |
| [Let's Encrypt](https://letsencrypt.org/) | Let's Encrypt 'Oak2019' Log | https://oak.ct.letsencrypt.org/2019/       | 24 hours | [Chrome 78](https://crrev.com/703880) | Rejected - Shard Expired     |
| [Venafi](https://www.venafi.com/)         | Venafi Gen2 CT log          | https://ctlog-gen2.api.venafi.com/         | 24 hours | [Chrome 59](https://crrev.com/471318) | Rejected - All Certs Expired |
| [DigiCert](https://www.digicert.com/)     | DigiCert Log Server 2       | https://ct2.digicert-ct.com/log/           | 24 hours | [Chrome 60](https://crrev.com/481160) | 04 May 2020 00:00:40 UTC     |
