# Certificate Transparency in Chrome

Chrome maintains three policies for Certificate Transparency:
* The [Chrome CT Policy](https://goo.gl/chrome/ct-policy) outlines the criteria
  for certificates to be deemed _CT Compliant_ in CT-enforcing versions of
  Chrome.
* The [Chrome CT Log Policy](https://goo.gl/chrome/ct-log-policy) describes what
  requirements Chrome places on current and prospective CT Log Operators.
* The [Chrome CT Log List Policy](log_lists.md) describes what requirements
  Chrome places on users of Chrome's published CT Log Lists.

## Overview of Certificate Transparency

Certificate Transparency (CT) is a protocol designed to fix several structural
flaws in the SSL/TLS certificate ecosystem. Described in
[RFC 6962](https://tools.ietf.org/html/rfc6962), and expanded by
[static-ct-api](https://c2sp.org/static-ct-api), it provides a public,
append-only data structure that can log certificates that are issued by
[certificate authorities](https://en.wikipedia.org/wiki/Certificate_authority) (CAs).

By logging certificates, it becomes possible for the public to see what
certificates have been issued by a given CA. This allows site operators to
detect when a certificate has been issued for their domains, allowing them to
check for unauthorized issuance. It also allows browsers and root stores, and
the broader community, to examine the certificates a CA has issued and ensure
that the CA is complying with their expected or disclosed practices.

For more information about how Certificate Transparency works and its role in
supporting the web PKI, you can find a helpful introduction to CT at
[https://certificate.transparency.dev](https://certificate.transparency.dev/).

Chrome requires all publicly-trusted TLS certificates issued after April 30,
2018 to support CT in order to be recognized as valid. This site provides
details on what is required. Any questions should be directed to the
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy)
list.
