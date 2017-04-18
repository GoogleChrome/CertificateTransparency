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
