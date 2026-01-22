# Upcoming changes for applications using Chrome's CT Log Lists

As outlined in our [Acceptable Use
Policy](/CertificateTransparency/log_lists.html), use of Chrome's Certificate
Transparency (CT) log list to enable CT enforcement in applications other than
Chrome is not permitted. Unauthorized use of the log list for enforcing CT has
resulted in several instances of severe breakage when Google has pushed required
updates to Chrome's log list. To ensure that Google is able to push updates to
Chrome clients safely, Google is taking steps to ensure that prominent 3rd-party
CT enforcement libraries ("CT libraries") no longer rely on Chrome's CT log
list.

**Apps relying on 3rd-party CT enforcement libraries using Google's log list
will break if application developers take no action. Developers should stop
using such libraries. Google is providing tools to allow impacted developers to
avoid breakage as a last resort for non-updateable applications.**

Applications relying on Chrome's log list for other purposes (e.g. for CT log
monitoring) will be unaffected.

To avoid breakage, developers of applications relying on 3rd-party CT libraries
should immediately remove CT libraries from their applications and take steps to
ensure that their users update to the latest version of their application.

Developers should undertake these steps immediately. The remainder of this doc
provides additional information about when to expect breakage for applications
that still rely on impacted CT libraries.

## Background
If you are not familiar with how CT works, we recommend
[these](https://certificate.transparency.dev/howctworks/)
[overviews](https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Certificate_Transparency).
This document assumes a basic understanding of CT fundamentals.

Google publishes CT log lists so that CT monitors and certificate submitters
know what logs are currently recognized by Chrome. Google presently publishes
two versions of these lists, v2 and v3. Depending on the CT library used,
impacted applications may be reliant on either or both versions, and required
remediation timelines differ by log list version. Applications using CT
libraries updated since mid-2023 likely use the v3 log list. Applications that
have not updated their dependencies, or clients that have not updated their
applications, may be reliant on the prior version of the list.

Individual logs recognized by Chrome only contain certificates that expire in a
given time range (i.e. they are "[temporally
sharded](/CertificateTransparency/log_policy.html#temporal-sharding)"). Once
this time range has passed, these logs are removed from the log list, and the
log may be shut down.  Thus log lists change as logs age out and new logs take
their place.

## Freezing log lists and adding mimic logs
To prevent CT libraries from relying on Chrome's log list, Google is not adding
any additional CT logs to the log lists served to CT libraries. Google has no
plans to stop serving these frozen log lists to clients. As logs naturally
expire, developers wishing to provide SCTs that satisfy the CT library
requirements will need to take action to find certificates and SCTs compatible
with these frozen log lists.

Logs contained in these frozen log lists will go offline over time, either due
to log malfunction or the natural lifecycle of CT logs. Assuming all logs
continue through their anticipated lifetimes, it will not be possible to acquire
a set of SCTs from logs included in the v2 log list for any certificate that
expires on or after 2027-01-01. Similarly, it will not be possible to acquire
SCTs from logs in the v3 log list for any certificate expiring on or after
2027-07-01.

As a last resort for out-of-date clients whose applications will not update
before the cut-off date, Google is supplementing the existing v2 and v3 log
lists served to CT libraries with two new CT log "mimics". These mimics will not
be included in the log list used by Chrome, and these mimics do not log
certificates. We expect to update the log lists served to CT libraries with
these new mimics in the next few weeks.

Private keys for these log mimics are available for download
([mimic1.pem](/CertificateTransparency/mimics/mimic1.pem),
[mimic2.pem](/CertificateTransparency/mimics/mimic2.pem)). Developers of
applications using CT libraries must ensure that any certificates their
applications rely on are served alongside one SCT from each mimic to ensure
ongoing conformance with CT library requirements. Developers can use tools
[available on GitHub](http://github.com/jdeblasio/sct-generator) to generate
SCTs from these mimics, and provide those SCTs to applications via the SCT TLS
extension. Developers may also be able to have mimic SCTs be embedded in their
certificates with the cooperation of the certificate's CA.

Please note that clients using these frozen log lists will not benefit from CT’s
security and transparency guarantees. The inclusion of two mimics whose keys are
freely available means that any certificate can be made to pass CT enforcement
checks without being logged to the CT log ecosystem.

## Upcoming temporary breakage
Google is making every effort to contact impacted developers ahead of time such
that developers have time to take necessary actions. As part of that effort, and
since Google does not have comprehensive contact mechanisms, Google will also
take steps to temporarily break impacted apps as an early warning signal to
impacted developers we can not otherwise reach.

Starting on or after 2026-07-01, Google will undertake a series of short-term
breakages in which we will reduce the set of logs included in the log lists
served to CT libraries to include only log mimics. Developers that ensure that
their connections provide SCTs from the mimics will not be affected by this
breakage.

Signaling breakage will occur periodically between July 1 and November 1, with
no more than one period of breakage every two weeks. Each signalling event will
last no more than 4 hours. While Google will announce the first of such
breakages on
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/g/ct-policy/),
we may not announce all breakage events ahead of time.

## FAQ

### My app has clients that will not update in time and I can't use the mimics. What should I do?
Applications distributed through the Google Play Store are encouraged to utilize
Play Console's [recovery
tools](https://support.google.com/googleplay/android-developer/answer/13812041?hl=en)
to prompt users to upgrade their application to your latest version.

### I really want to enforce CT in my app. What should I do?
Enforcing CT safely requires keeping up with the evolving CT ecosystem.
3rd-party CT enforcement libraries have not demonstrated that they can keep up
with these changes, nor are they implementing standard industry best practices
to minimize application breakage.

Developers should rely on native platform support. **If you are developing an
Android application, you should rely on native platform support available in
Android 16+ and not enforce CT on earlier versions.** Apple app developers
automatically have CT enforced for all TLS connections without any developer
action required.

If you still choose to enforce CT in your application without relying on
platform support, you must ensure that your application does **NOT** fetch
Chrome's or Android's log lists directly from Google, nor rely on Google's log
list signing keys. Enforcing CT is done at your own risk, and Google will take
no action to mitigate breakage that any action we take causes your application.

### When will Google stop serving the log lists (e.g. by making them return HTTP 404)
We have no identified timeline to stop serving the frozen versions of Chrome's
CT log list to CT-enforcing libraries. We are committing to serving the frozen
version of the log list until at least 2027-07-01. When we decide on a timeline,
we will announce it ahead of time on the
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/g/ct-policy/)
mailing list.

### Can Google make the log lists return HTTP 404 instead of freezing the list?
No. In our original attempt at turning down the v2 version of the log list, many
apps
[indicated](https://groups.google.com/a/chromium.org/g/ct-policy/c/zejEtWAJtEA/m/Y2sW344QBQAJ)
that taking down the log list resulted in significant breakage. We thus believe
it is safer to freeze the log list than to make requests to them return HTTP
404.

### I have additional questions
Please search the archives of the
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/g/ct-policy/)
mailing list to see if your question has been answered. If you still have
questions, feel free to reach out to that public list.

