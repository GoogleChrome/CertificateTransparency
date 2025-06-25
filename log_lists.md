# Chrome's CT Log Lists

Google publishes what CT logs are known and trusted by the Chrome browser
(collectively the "CT Log Lists"), predominately in JSON format. There are two
varieties of these lists published:

 * [`log_list.json`](https://www.gstatic.com/ct/log_list/v3/log_list.json)
   contains logs that are `Qualified`, `Usable`, or `Retired` as of when the
   list was generated.
 * [`all_logs_list.json`](https://www.gstatic.com/ct/log_list/v3/all_logs_list.json)
   contains the logs in `log_list.json`, alongside logs that may be `Pending`,
   `Retired`, or but have never applied for inclusion in Chrome's log list.

Both of these lists follow a published log list
[schema](https://www.gstatic.com/ct/log_list/v3/log_list_schema.json). Chrome
also signs these lists
([`log_list`](https://www.gstatic.com/ct/log_list/v3/log_list.sig)/[`all_logs_list`](https://www.gstatic.com/ct/log_list/v3/all_logs_list.sig))
to facilitate offline verification of the
contents using a published [public
key](https://www.gstatic.com/ct/log_list/v3/log_list_pubkey.pem).
`log_list.json` and its signature are also available bundled as a [zip
file](https://www.gstatic.com/ct/log_list/v3/log_list.zip).

## Log list changes
Chrome's CT Log Lists are updated daily. Most changes to log states included in
the CT Log Lists, and all schema or URL changes, are announced on
[ct-policy@](https://groups.google.com/a/chromium.org/g/ct-policy/). Users of
the log list should subscribe to and follow
[ct-policy@](https://groups.google.com/a/chromium.org/g/ct-policy/) to ensure
they stay apprised of any changes that may affect them.

## Availability, and SLAs
Chrome's CT Log Lists are offered without SLA or availability guarantee. Google
endeavors to ensure that the CT Log Lists are consistently available to enable
authorized uses, however, consumers are encouraged to cache recent versions of
the CT Log Lists to account for downtime or other issues in the published Lists.

## Acceptable Use Policy
Google Chrome makes its CT Log Lists available for the purposes of certificate
submitters (such as certification authorities) and CT monitors and auditors
wishing to remain compatible with, or investigate the contents of, the CT and
WebPKI ecosystems.

**Chrome's CT Log Lists may not be used to facilitate CT enforcement in TLS
clients other than Chrome without explicit written permission from Chrome's CT
team.**

Unauthorized reliance on Chrome's CT Log Lists endangers not just your users,
but Chrome users and the CT ecosystem as a whole. If you are exploring adding CT
enforcement into your user agent, the Chrome CT team is happy to talk to you
about how to do that in a way that is safe and compatible with the broader CT
ecosystem.

Using Chrome's CT Log List out of line with this policy is done at your own
risk, and may result in breakage of your application. Google must be able to
make changes to the CT Log Lists in response to incidents in the CT ecosystem so
as to maintain the safety and security of Chrome users. Google may take steps to
ensure that third-party dependencies on the CT Log Lists do not risk Google's
ability to respond to such incidents, including unannounced changes to the log
list to disrupt unauthorized use.

