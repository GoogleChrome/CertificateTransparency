All certificates issued by publicly-trusted CAs must be disclosed to Certificate
Transparency logs in order to be trusted in Chrome.

This policy was rolled out gradually over many years:

* Starting 1 January 2015, Chrome required that all **Extended Validation**
  certificates be disclosed via Certificate Transparency. Certificates that were
  not properly disclosed would be [stripped of their EV
  status](https://news.netcraft.com/archives/2015/08/24/thousands-short-changed-by-ev-certificates-that-dont-display-correctly-in-chrome.html),
  but no warnings would be shown to visitors to sites that did not comply.

* [Starting 1 June
  2016](https://security.googleblog.com/2015/10/sustaining-digital-certificate-security.html),
  Chrome required that all new certificates issued by the set of root
  certificates owned by Symantec Corporation were disclosed via Certificate
  Transparency. Certificates that were not disclosed, or which were not
  disclosed in a way consistent with RFC 6962, would be rejected as untrusted.

* Starting from certificates issued after 30 April 2018, [Chrome required that
  the certificate be disclosed via Certificate
  Transparency](https://groups.google.com/a/chromium.org/d/msg/ct-policy/wHILiYf31DE/iMFmpMEkAQAJ).
  If a certificate issued after that date did not provide adequate
  [proof](ct_policy.md) of being disclosed to CT, the certificate is rejected as
  untrusted, and the connection is blocked. In the case of a main page load, the
  user sees a full page certificate warning page, with the error code
  `net::ERR_CERTIFICATE_TRANSPARENCY_REQUIRED`. If you receive this error, this
  indicates that your CA, CDN, or hosting provider has a misconfiguration, and
  you should contact their support teams to ensure you can get a replacement
  certificate that works.