### Chrome Policies

Chrome has gradually required Certificate Transparency for more and more
publicly-trusted certificates over the past few years.

* [Since 1 January 2015](https://github.com/chromium/ct-policy/blob/master/ct_policy.md),
Chrome has required that all Extended Validation certificates be disclosed via
Certificate Transparency. Certificates that were not properly disclosed would
be [stripped of their EV status](https://news.netcraft.com/archives/2015/08/24/thousands-short-changed-by-ev-certificates-that-dont-display-correctly-in-chrome.html),
but no warnings would be shown to visitors to sites that did not comply.

* [Since 1 June 2016](https://security.googleblog.com/2015/10/sustaining-digital-certificate-security.html),
Chrome has required that all new certificates issued by the set of root
certificates owned by Symantec Corporation are disclosed via Certificate
Transparency. Certificates that were not disclosed, or which were not disclosed
in a way consistent with RFC 6962, would be rejected as untrusted.

* For all new certificates issued after 30 April 2018, [Chrome will require that
the certificate be disclosed via Certificate
Transparency](https://groups.google.com/a/chromium.org/d/msg/ct-policy/wHILiYf31DE/iMFmpMEkAQAJ).
If a certificate is issued after this date and neither the certificate nor
the site supports CT, then these certificates will be rejected as untrusted, and
the connection will be blocked. In the case of a main page load, the user will
see a full page certificate warning page, with the error code
`net::ERR_CERTIFICATE_TRANSPARENCY_REQUIRED`. If you receive this error, this
indicates that your CA has not taken steps to make sure your certificate
supports CT, and you should contact your CA's sales or support team to ensure
you can get a replacement certificate that works.