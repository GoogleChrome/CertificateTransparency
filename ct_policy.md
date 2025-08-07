# Chrome Certificate Transparency Policy
_Please direct any questions about this Policy to the CT Policy forum:
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy)_

When a website’s TLS certificate is validated in modern versions of Chrome, it
is evaluated for compliance against the Chrome CT Policy, except in rare
circumstances where
[certain](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForCas)
[enterprise](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForLegacyCas)
[policies](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForUrls)
are set by an administrator. Certificates that are accompanied by SCTs that
satisfy this Policy are said to be *CT Compliant*.

CT Compliance is achieved by a certificate and set of accompanying SCTs by
meeting a set of technical requirements enforced by the Chrome browser during
certificate validation, which are defined in this Policy. The issuance of
certificates that are not CT compliant is **not** considered mis-issuance or a
violation of Chrome’s root program; such certificates will simply fail to
validate in CT-enforcing versions of Chrome.

---

## CT Log States
CT Compliance in Chrome is determined by evaluating SCTs from CT Logs and
ensuring that these Logs are in the correct state(s) at time of check. The set
of possible states a CT Log can be in is: 
* `Pending`,
* `Qualified`,
* `Usable`,
* `ReadOnly`, 
* `Retired`, and
* `Rejected` 

In order to assist with understanding the requirements for CT compliance in
Chrome, the definition of these states, the requirements of Logs in each state,
as well as how these states impact Chrome behavior are described in detail in
the [CT Log Lifecycle Explainer](log_states.md). 

---

## CT Compliant Certificates
A TLS certificate is *CT Compliant* if it is accompanied by a set of SCTs that
satisfies at least one of the criteria defined below. In CT-enforcing versions
of Chrome, all publicly-trusted TLS certificates are required to be CT Compliant
to successfully validate.

When evaluating a certificate for CT Compliance, Chrome considers several
factors including how many SCTs are present, who operates the CT Log that issued
the SCT, and what state the CT Log that issued the SCT was in, both at the time
the certificate is being validated, and at the time the SCT was created by the
CT Log.

Depending on how the SCTs are presented to Chrome, CT compliance can be achieved
by meeting one of the following criteria:

**Embedded SCTs:**
1. At least one Embedded SCT from a CT Log that was `Qualified,` `Usable,` or
   `ReadOnly` at the time of check; and
2. There are Embedded SCTs from at least N distinct CT Logs that were
   `Qualified`, `Usable`, `ReadOnly`, or `Retired` at the time of check, where N
   is defined in the following table; and
3. Among the SCTs satisfying requirement 2, at least two SCTs must be issued
   from distinct CT Log Operators as recognized by Chrome; and
4. Among the SCTs satisfying requirement 2, at least one SCT must be issued from
   a log recognized by Chrome as being RFC6962-compliant.

| Certificate Lifetime | Number of SCTs from distinct CT Logs |
|:---:|:---:|
| <= 180 days | 2 |
| > 180 days | 3 |

**SCTs delivered via OCSP or TLS:**
1. At least two SCTs from a CT Log that was `Qualified`, `Usable`, or `ReadOnly`
   at the time of check; and
2. Among the SCTs satisfying requirement 1, at least two SCTs must be issued
   from distinct CT Log Operators as recognized by Chrome; and
3. Among the SCTs satisfying requirement 1, at least one SCT must be issued from
   a CT log recognized by Chrome as being RFC6962-compliant.

For both embedded SCTs and those delivered via OCSP or TLS, Log Operator
uniqueness is defined as having separate entries within the `operators` section
of [log_list.json](log_lists.md). In the rare situation that a CT Log changes
operators during its lifetime, CT logs in the [v3 log list
schema](https://www.gstatic.com/ct/log_list/v3/log_list_schema.json) optionally
contain an list of `previous_operators`, accompanied by the final timestamp that
this log was operated by the previous operator. To prevent log operator changes
from breaking existing certificates, each SCT’s log operator is determined to be
the operator at the time of SCT issuance, by comparing the SCT timestamp against
the `previous_operators` timestamps, if present.

### Important Notes
So long as one of the above CT Compliance criteria is met by some combination of
SCTs presented in the handshake, additional SCTs, regardless of the status of
the SCT, will not affect a certificate’s CT Compliance status positively or
negatively.

In order to contribute to a certificate’s CT Compliance, an SCT must have been
issued before the Log’s `Retired` timestamp, if one exists. Chrome uses the
earliest SCT among all SCTs presented to evaluate CT compliance against CT Log
`Retired` timestamps. This accounts for edge cases in which a CT Log becomes
`Retired` during the process of submitting certificate logging requests.

"Embedded SCT" means an SCT delivered via the SignedCertificateTimestampList
X.509v3 extension within the certificate itself. Most TLS servers do not support
OCSP Stapling or the TLS extension, so CAs should be prepared to embed SCTs into
issued certificates to ensure successful validation and/or EV treatment in
Chrome.

---

## How CT Logs are added to Chrome
The criteria for how CT Logs can become `Qualified`, as well as what
circumstances can cause them to become `Retired`, can be found in the [Chrome CT
Log Policy](log_policy.md).

---

## CT Enforcement Timeout
Every day, Google publishes a new [CT Log list](log_lists.md) that contains a
fresh `log_list_timestamp`. These updated log lists are included in all
updates to Chrome's software, as well as delivered separately to Chrome clients
daily. Chrome will enforce CT so long as the `log_list_timestamp` of the
freshest version of the log list Chrome stores is within the past 70 days (10
weeks), and uses a log list format that Chrome understands.

If the installed version of Chrome has not applied security updates and has been
unable to obtain an updated CT log list from the Component Updater for 70 days
or more, then CT enforcement will be disabled. This timeout provides a critical
assurance to the CT ecosystem that new CT Logs are able to safely transition to
`Usable` within a fixed amount of time after becoming `Qualified`. All
CT-enforcing user agents are strongly encouraged to implement a similar
enforcement timeout to maximize compatibility with the existing ecosystem.
