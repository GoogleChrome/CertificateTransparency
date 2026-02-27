# If your app relies on a 3rd-party CT enforcement library, it will break unless you take action.

Applications that use 3rd-party CT enforcement libraries should **stop using these libraries to avoid breakage**. Android applications should instead rely on [native CT enforcement](https://developer.android.com/privacy-and-security/security-config#CertificateTransparencySummary) in Android 16+ and not enforce CT on earlier versions.

These libraries **no longer offer any security benefit**, and are exclusively adding breakage risk at an unknown future date

Applications and libraries relying on Chrome's CT log list are in violation of Google's [Acceptable Use Policy](/CertificateTransparency/log_lists.html). This reliance has resulted in multiple instances of application breakage when Google pushes required updates to the list. To ensure that Google is able to push updates to Chrome clients safely, Google is taking steps to prevent unauthorized reliance on Chrome’s CT log list.

Applications distributed through the Google Play Store may use Play Console’s [recovery tools](https://support.google.com/googleplay/android-developer/answer/13812041?hl=en) to prompt users running old versions of their application to upgrade their application to your latest version. 

## What's Changing

[Certificate Transparency](https://certificate.transparency.dev) makes it possible to detect HTTPS certificates issued to unauthorized parties by requiring that certificates are made available in public logs. Logs are replaced approximately every 6 months.

Changes in how Google publishes its CT log list will result in 3p CT-enforcement libraries not being made aware of new CT logs. Over time, newly-issued certificates for websites and APIs that reliant applications connect to will only be logged to CT logs that the CT-enforcement libraries do not recognize. This will cause these libraries to prevent connections to those websites and endpoints.

### Temporary breakage

Google is making every effort to contact impacted developers ahead of time to provide the opportunity to take remedial action. As part of that effort, and since Google does not have comprehensive contact mechanisms for all impacted developers, Google will temporarily break impacted apps as an early warning signal to developers that can not otherwise be reached.

Signaling breakage will occur periodically between July 1 and November 1, with no more than one period of breakage every two weeks. Each period of breakage will last no more than 4 hours. While Google will announce the first of such breakages on [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/g/ct-policy/), we may not announce all breakage events ahead of time.

### Permanent breakage

Applications will break progressively depending on when certificates used by the application are renewed. Applications using older versions of CT enforcement libraries **may stop working at any time**. Apps using the most up-to-date libraries **may break as early as May 29th**. All applications using these libraries will be broken before July 1, 2027 if no developer action is taken.

For additional information, including additional technical background and a last resort alternative for applications that cannot be updated, please see the [full announcement](/CertificateTransparency/3p_libraries.html).