# Chromium Certificate Transparency Policy

This repository contains documents related Chromium's Certificate Transparency
policies, such as the [Certificate Transparency Log Policy](log_policy.md).

Their contents can be discussed in the
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy)
forum.

## For Certificate Authorities

In order to help protect users of the Chromium Projects, CAs are expected to
support Certificate Transparency. This allows users, the Chromium Authors, and
the public to verifiably audit that CAs are conforming to the policies set out
in Chromium's [Root Certificate Policy](https://www.chromium.org/Home/chromium-security/root-ca-policy).

Currently, Chromium does not enforce that all Root CAs support Certificate
Transparency for all certificates. However, it is required for the certificates
issued by some CAs, and in order to have a certificate recognized as an Extended
Validation certificate, that such certificates **MUST** be CT Qualified. For
more details, see the [Certificate Transparency in Chrome Policy](ct_policy.md).

## For Log Operators

In order for a Log to be included within Chromium, it must meet the
requirements of the [Certificate Transparency Log Policy](log_policy.md). The
Log Policy describes the steps for Log Operators to submit Logs for inclusion
within Chromium.

## Recognized Logs

The following table includes information about the Certificate Transparency Logs
that are recognized by Chromium. It includes information about who operates the
log, the name the log has been given, and the URL that can be used for logging
certificates or inspecting the certificates that have been logged.

**_Note: The authoritative list is maintained in the [Chromium code base](https://cs.chromium.org/chromium/src/net/data/ssl/certificate_transparency/log_list.json). This is merely informational._**

### Qualified Logs

| Log Operator | Name | Log URL | Maximum Merge Delay | Included Since |
| ------------ | ---- | ------- | ------------------- | -------------- |
|[Google](https://www.google.com)|Google 'Pilot' Log|https://ct.googleapis.com/pilot|24 hours|*Revision:* https://crrev.com/237785 <br/> Chrome: 35|
|[Google](https://www.google.com)|Google 'Aviator' Log|https://ct.googleapis.com/aviator|24 hours|*Revision:* https://crrev.com/237785 <br/> Chrome: 35 <br/> Note: Frozen (not accepting new certificates)|
|[DigiCert](https://www.digicert.com)|DigiCert's Certificate Transparency log|https://ct1.digicert-ct.com/log/|24 hours|*Revision:* https://crrev.com/309831 <br/> Chrome: 41|
|[Google](https://www.google.com)|Google 'Rocketeer' Log|https://ct.googleapis.com/rocketeer|24 hours|*Revision:* https://crrev.com/325382 <br/> Chrome: 43|
|[DigiCert](https://www.digicert.com)|Symantec Log|https://ct.ws.symantec.com|24 hours|*Revision:* https://crrev.com/483625 <br/> Chrome: 45|
|[DigiCert](https://www.digicert.com)|Symantec 'Vega' Log|https://vega.ws.symantec.com/|24 hours|*Revision:* https://crrev.com/376143 <br/> Chrome: 50|
|[CNNIC](https://cnnic.cn)|CNNIC CT Log|https://ctserver.cnnic.cn/|24 hours|*Revision:* https://crrev.com/396817 <br/> Chrome: 53|
|[Google](https://www.google.com)|Google 'Skydiver' Log|https://ct.googleapis.com/skydiver/|24 hours|*Revision:* https://crrev.com/429670 <br/> Chrome: 55|
|[Google](https://www.google.com)|Google 'Icarus' Log|https://ct.googleapis.com/icarus/|24 hours|*Revision:* https://crrev.com/429670 <br/> Chrome: 55|
|[Venafi](https://www.venafi.com)|Venafi Gen2 CT log|https://ctlog-gen2.api.venafi.com/|24 hours|*Revision:* https://crrev.com/471318 <br/> Chrome: 59|
|[Comodo](https://www.comodo.com)|Comodo 'Sabre' Log|https://sabre.ct.comodo.com/|24 hours|*Revision:* https://crrev.com/482145 <br/> Chrome: 60|
|[Comodo](https://www.comodo.com)|Comodo 'Mammoth' Log|https://mammoth.ct.comodo.com/|24 hours|*Revision:* https://crrev.com/482145 <br/> Chrome: 60|
|[DigiCert](https://www.digicert.com)|DigiCert Log Server 2|https://ct2.digicert-ct.com/log/|24 hours|*Revision:* https://crrev.com/481160 <br/> Chrome: 60|
|[DigiCert](https://www.digicert.com)|Symantec 'Sirius' Log|https://sirius.ws.symantec.com/|24 hours|*Revision:* https://crrev.com/481160 <br/> Chrome: 60|
|[Google](https://www.google.com)|Google 'Argon2018' Log|https://ct.googleapis.com/logs/argon2018/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Google](https://www.google.com)|Google 'Argon2019' Log|https://ct.googleapis.com/logs/argon2019/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Google](https://www.google.com)|Google 'Argon2020' Log|https://ct.googleapis.com/logs/argon2020/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Google](https://www.google.com)|Google 'Argon2021' Log|https://ct.googleapis.com/logs/argon2021/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Cloudflare](https://www.cloudflare.com)|Cloudflare 'Nimbus2018' Log|https://ct.cloudflare.com/logs/nimbus2018/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Cloudflare](https://www.cloudflare.com)|Cloudflare 'Nimbus2019' Log|https://ct.cloudflare.com/logs/nimbus2019/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Cloudflare](https://www.cloudflare.com)|Cloudflare 'Nimbus2020' Log|https://ct.cloudflare.com/logs/nimbus2020/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[Cloudflare](https://www.cloudflare.com)|Cloudflare 'Nimbus2021' Log|https://ct.cloudflare.com/logs/nimbus2021/|24 hours|*Revision:* https://crrev.com/540254 <br/> Chrome: 65|
|[DigiCert](https://www.digicert.com)|DigiCert 'Yeti2018' Log|https://yeti2018.ct.digicert.com/log|24 hours|*Revision:* https://crrev.com/559734 <br/> Chrome: 67|
|[DigiCert](https://www.digicert.com)|DigiCert 'Yeti2019' Log|https://yeti2019.ct.digicert.com/log|24 hours|*Revision:* https://crrev.com/559734 <br/> Chrome: 67|
|[DigiCert](https://www.digicert.com)|DigiCert 'Yeti2020' Log|https://yeti2020.ct.digicert.com/log|24 hours|*Revision:* https://crrev.com/559734 <br/> Chrome: 67|
|[DigiCert](https://www.digicert.com)|DigiCert 'Yeti2021' Log|https://yeti2021.ct.digicert.com/log|24 hours|*Revision:* https://crrev.com/559734 <br/> Chrome: 67|
|[DigiCert](https://www.digicert.com)|DigiCert 'Yeti2022' Log|https://yeti2022.ct.digicert.com/log|24 hours|*Revision:* https://crrev.com/559734 <br/> Chrome: 67|

### Once, but no longer, Qualified Logs

| Log Operator | Name | Log URL | Maximum Merge Delay | Included Since | Last Accepted SCT |
| ------------ | ---- | ------- | ------------------- | -------------- | ----------------- |
|[Certly](https://certly.io)|Certly.IO Log|https://log.certly.io|24 hours|*Revision:* https://crrev.com/325382 <br/> Chrome: 43 | 15 April 2016 00:00:00 UTC.|
|[Izenpe](https://www.izenpe.com)|Izenpe Log|https://ct.izenpe.com|24 hours|*Revision:* https://crrev.com/326301 <br/> Chrome: 44 | 30 May 2016 00:00:00 UTC.|
|[Venafi](https://www.venafi.com)|Venafi CT Log Server|https://ctlog.api.venafi.com/ct/v1|24 hours|*Revision:* https://crrev.com/349170 <br/> Chrome: 47 | Last Accepted SCT: 28 Feb 2017 18:42:26 UTC.|
|[WoSign](https://www.wosign.com/)|WoSign Log|https://ctlog.wosign.com/|24 hours|*Revision:* https://crrev.com/414378 <br/> Chrome: 54 | 12 Feb 2018 23:59:59 UTC.|
|[StartCom](https://www.startssl.com/)|StartCom CT Log|https://ct.startssl.com/|24 hours|*Revision:* https://crrev.com/414440 <br/> Chrome: 54 | 12 Feb 2018 23:59:59 UTC.|

## Policy Version
Chromium Certificate Transparency Policy Version 1.0
