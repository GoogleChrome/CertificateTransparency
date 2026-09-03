# 3p CT enforcement libraries will break

Applications that use 3rd-party CT enforcement libraries should **stop using
these libraries to avoid breakage**. Android applications should instead rely on
[native CT enforcement](https://developer.android.com/privacy-and-security/security-config#CertificateTransparencySummary)
in Android 16+ and not enforce CT on earlier versions.

Libraries that rely on Chrome's CT log lists are in violation of
Google's [Acceptable Use Policy](/CertificateTransparency/log_lists.html), and
**no longer offer any security benefit**. Attackers can trivially bypass these
library's CT enforcement protections, and Google is taking steps to prevent
unauthorized reliance on Chrome’s CT log list to ensure that Google is will
keeps Chrome's users safe.

Once updated to no longer use the library, applications distributed through the
Google Play Store should use Play Console’s [recovery
tools](https://support.google.com/googleplay/android-developer/answer/13812041?hl=en)
to prompt users running old versions of the application to upgrade to the latest
version.

## What's Changing

[Certificate Transparency](https://certificate.transparency.dev) makes it
possible to find all HTTPS certificates issued to a domain by requiring that
certificates are published in public logs. Google publishes a list of logs
trusted by Chrome so that websites and HTTPS Certificate Authorities can ensure
compatibility with Chrome users.

Upcoming changes to Google's lists will result in 3p CT-enforcement libraries
that rely on Google's list without authorization will no longer be able to
access those lists. As a result, some or all HTTPS connections from an
application using an impacted library may break.

### Temporary breakage

To assess impact and get the attention of impacted developers, Google will
repeatedly block access to Google's log lists for a few hours or days at a time.

These tests will start around 2026-07-01 and may occur at any time thereafter.

### Permanent breakage

Applications using unauthorized CT enforcement libraries **may stop working at
any time**. The precise timeline will be determined based on the results of the
temporary breakage, and may happen as early as 1 September, 2026.

For additional information, including additional technical background and a last
resort alternative for applications that cannot be updated, please see the [full
announcement](/CertificateTransparency/3p_libraries.html).
