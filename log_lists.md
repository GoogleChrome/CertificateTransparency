# Chrome's CT Log Lists

The Chrome team publishes known CT logs (collectively the "CT Log
Lists") for public consumption via two lists, each with distinct semantics:

 * [log_list.json](https://www.gstatic.com/ct/log_list/v3/log_list.json)
   contains logs that are `Qualified`, `Usable`, or `Retired` as of when the
   list was generated. These logs are those included in the Chrome browser for
   evaluating compliance with Chrome's [CT Policy](ct_policy.md).
 * [all_logs_list.json](https://www.gstatic.com/ct/log_list/v3/all_logs_list.json)
   contains all logs known to and tracked by the Chrome team, including the logs
   in `log_list.json`, logs that are `Pending` or `Retired`, as well as
   additional logs that have not applied for inclusion in Chrome's log list.

Both of these lists follow a published log list
[schema](https://www.gstatic.com/ct/log_list/v3/log_list_schema.json). Chrome
also signs these lists
([log_list](https://www.gstatic.com/ct/log_list/v3/log_list.sig)/[all_logs_list](https://www.gstatic.com/ct/log_list/v3/all_logs_list.sig))
to facilitate offline verification of the
contents using a published [public
key](https://www.gstatic.com/ct/log_list/v3/log_list_pubkey.pem).
`log_list.json` and its signature are also available bundled as a [zip
file](https://www.gstatic.com/ct/log_list/v3/log_list.zip).

## Log list changes
Chrome's log lists are updated daily. Changes to the log lists' schema or URL
are announced on
[ct-policy@](https://groups.google.com/a/chromium.org/g/ct-policy/). Users of
the log list should subscribe to and follow
[ct-policy@](https://groups.google.com/a/chromium.org/g/ct-policy/) to ensure
they stay apprised of any changes that may affect them.

## Availability, and SLAs
Chrome's CT log lists are offered without SLA or availability guarantee. Google
endeavors to ensure that the CT log lists are consistently available to enable
authorized uses, however, consumers are encouraged to cache recent versions of
the CT log lists to account for downtime or other issues in the published Lists.

## Acceptable Use Policy
Google Chrome makes its CT log lists available for the purposes of certificate
submitters (such as certification authorities) and CT monitors and auditors
wishing to remain compatible with, or investigate the contents of, the CT and
WebPKI ecosystems.

**Chrome's CT log lists may not be used to facilitate CT enforcement in TLS
clients other than Chrome without explicit written permission from Chrome's CT
team.**

Unauthorized reliance on Chrome's CT log lists endangers not just your users,
but Chrome users and the CT ecosystem as a whole. If you are exploring adding CT
enforcement into your user agent, the Chrome CT team is happy to talk to you
about how to do that in a way that is safe and compatible with the broader CT
ecosystem.

Using Chrome's CT log lists out of line with this policy is done at your own
risk, and is likely to result in the breakage of your application. Google must
be able to make changes to the CT log lists in response to incidents in the CT
ecosystem so as to maintain the safety and security of Chrome users, so Google
may take steps to ensure that third-party dependencies on the CT log lists do
not risk Google's ability to respond to such incidents, including unannounced
changes to the log list to disrupt unauthorized use.

