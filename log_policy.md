# Certificate Transparency Log Policy
Certificate Transparency includes a multi-party protocol for providing
cryptographically-verifiable proofs to audit the issuance and security practices
of Certification Authorities (CAs).

To support such auditing, Chrome includes a [list of logs](log_lists.md) that
have passed an application process and are recognized to be operating in the
public interest.  This Certificate Transparency Log Policy ("Policy") sets forth
how a Certificate Transparency log operator may have its log recognized within
Chrome for the purposes of certificates satisfying Chrome's [CT
policy](ct_policy.md), as well as the ongoing expectations of these log
operators. This policy may be updated from time to time.

While CT logs are critical infrastructure for the web, many organizations with
experience operating web services at scale have the prerequisites necessary to
operate CT logs successfully. If you might be interested in operating logs,
please reach out to the Chrome team at
chrome-certificate-transparency@google.com. Chrome is keen to work with
potential and current log operators to ensure those operators are successful.

---

## Application Process
Before applying for their first CT logs to be added to Chrome, new CT log
operators should first read and fully comprehend the ongoing requirements for CT
logs specified in this policy. Once a log operator is confident they can meet
these requirements and has deployed a set of temporally-sharded CT logs ready
for application, they should follow the below process for adding these logs to
Chrome.

### New CT Log Operators
New CT log operators should begin their application process by first [filing a
new CT log operator
bug](https://issues.chromium.org/issues/new?component=1861494&template=2214603) on the
Chromium Issue Tracker, and provide contact Information for the log operator,
including:
 * An email address that is continuously monitored by the log operator, and
 * a list of people authorized to represent the log operator when communicating
   with the Chrome team.

This bug will be used to track all CT logs operated by this log operator for as
long as any logs operated by this organization are `Pending`, `Qualified`,
`Usable`, `ReadOnly`, or `Retired`. By creating a new CT log operator bug,
applicants are asserting they are organizationally independent from all existing
CT log operators, which can be observed in the [log lists](log_lists.md) hosted
by Google. If an organizational change occurs that alters this independence, CT
log operators are required to notify Chrome at
chrome-certificate-transparency@google.com as soon as possible.

### Existing CT Log Operators
Once the Chrome team has confirmed the log operator's contact information, or if
an existing log operator is applying for additional CT logs to be added to
Chrome, the CT log operator must next provide the following information about
the new CT logs in their existing CT log operator bug:
* A description of the logs, including applicable policies or requirements for
  logging certificates, and whether these logs are compliant with RFC6962 or
  static-ct-api v1.0.0.
* A JSON object (one per log), conforming to the [provided
  schema](inclusion_request_schema.json), either provided directly in the log
  inclusion bug or via per-log URLs, containing:
    * a public HTTP endpoint that responds to all log client messages indicated
      in RFC 6962, Section 4, or HTTP endpoints responding to Submission and
      Monitoring APIs specified in
      [c2sp.org/static-ct-api@v1.0.0](https://c2sp.org/static-ct-api@v1.0.0), as
      appropriate,
    * the log's public key, provided as a DER-encoded ASN.1 SubjectPublicKeyInfo
      structure, base64-encoded,
    * the SHA-256 hash of the log's public key, base64-encoded (i.e. the LogID
      provided in SCTs issued by the log),
    * the Maximum Merge Delay (MMD) of the log, and
    * the expiry range of the log.
* The initial set of Accepted Root Certificates of the logs.
* Whether the logs will reject submissions for expired or revoked certificates.
* A description of any rate limiting policies applied to the logs.

Note that certificate expiry ranges for a set of logs must be contiguous, with
no gaps, and each log's expiry range should be between 3 and 12 months.

After acceptance, Google will monitor the logs, including via random compliance
testing, prior to its inclusion within Chrome. Such compliance testing will
include, but is not limited to, verifying the logs' conformance to RFC 6962 or
static-ct-api v1.0.0 (as appropriate), confirming the logs' availability meets
the requirements of this policy, and confirming the logs are append-only and
consistent from every point of view.

To enable compliance monitoring, log operators must include Google's Merge Delay
Monitor Root certificate in the set of accepted root certificates of their logs.
Log operators should expect ongoing querying of their logs from Google's
compliance monitoring infrastructure throughout the lifetime of the log.

---

## Log API Specification Requirements
All logs applying for inclusion in Chrome's log list must conform with either
RFC 6962 or to the static-ct-api v1.0.0 C2SP specification. Insofar as is
possible, Chrome's requirements are equivalent between static-ct-api and RFC
6962 logs, however:
 1. Static-ct-api logs must not specify a MMD greater than 1 minute.
 2. During the initial phase of static-ct-api log acceptance, existing operators
    of RFC 6962 logs included in Chrome's log list should continue to operate
    those logs (or RFC 6962 logs covering the same set of certificates).

---

## Ongoing Requirements of Included Logs
In order for their logs to remain included within Chrome after first becoming
`Qualified`, log operators must continue to operate these logs in accordance
with this policy. Log operators must:
* Monitor the
  [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy)
  group for relevant updates to policy or requirements for CT log operators.
* Incorporate a certificate for which an SCT has been issued by the log within
  the MMD.
    * When logs receive a logging submission for an already-incorporated
      certificate, logs must either return an existing SCT or, if creating a new
      one, add another certificate entry within the MMD such that the new SCT
      can be verified using the log's CT APIs
* Maintain log availability of 99% or above.
    * Log availability is measured on a per-endpoint basis over a 90-day rolling
      average from all requests made to the log by the Chrome team's compliance
      monitoring infrastructure. The log's overall availability is represented
      by the minimum of all per-endpoint availabilities.
    * Behavior that results in reduced availability includes, but is not limited
      to: network level outages, expiration of the log's SSL certificate, a
      failure to accept new Certificates to be logged (with the exception of the
      conditions defined in the Logging Submission Policy section below),
      HTTP response status codes other than 200, or responses that include data
      that does not conform to the log's corresponding API specification.
* Ensure their logs conform to the totality of the API specification indicated
  in the log's application.
* Maintain the append-only property of the log by providing consistent views of
  the Merkle Tree at all times and to all parties.
* Not impose conditions on retrieving or sharing data from the logs.
* Not present two or more conflicting views of the Merkle Tree at different
  times and/or to different parties.
* Accept certificates issued by Google's Merge Delay Monitor Root to enable
  Google to monitor the log's compliance to these policies.
* Notify the Chrome team of any and all changes to information gathered during
  the log inclusion process by detailing such changes in an update to the CT log
  operator bug on the [Chromium Issue
  Tracker](https://issues.chromium.org/issues?q=status:open%20componentid:1456813)
  in which they requested log Inclusion.

Google will notify log operators of changes to these requirements as well as
effective dates for those changes via announcements to the
[ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy) ("ct-policy@") mailing list.

---

## Incident Detection and Response
Log operators are strongly encouraged to implement proactive alerting to detect
log conditions that could lead to a policy violation or incident before an
incident occurs. Even when incidents can not be avoided, we believe that log
operators detecting issues with their own logs yields the quickest resolution.
In particular, good candidates for alerting may include the logs' merge delay
(if the log does not include entries synchronously), frequency of non-200 HTTP
status codes, [Chrome's per-endpoint availability
monitoring](https://www.gstatic.com/ct/compliance/endpoint_uptime.csv), and resource usage
metrics. When log operators do not detect incidents on their own, incidents may
be reported by the Chrome team or other members of the CT community, via the log
operator's log inclusion bug, via email, or via
[ct-policy@](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy).

We expect all log incidents to be investigated and remediated by log operators
promptly, regardless of how they were detected. Log operators should ensure
adequate communication with the broader community and the Chrome team while logs
are not meeting expectations by regularly emailing
[ct-policy@](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy).
This includes acknowledgement of the incident within one business day of
becoming aware of the problem, regular updates on progress and remediation
timeline while the incident is ongoing (typically no less than weekly), and a
comprehensive postmortem once the incident is resolved.

In some circumstances, log operators may be forced to make a decision that
favors compliance with one requirement over another. To ensure that SCTs remain
a strong indicator that a certificate was issued transparently, log operators
are encouraged to implement mechanisms in their logs that prioritize the timely
inclusion and availability of log entries over the continued availability of
`add-chain` and `add-pre-chain` APIs.

---

## Chrome's Response to Incidents and Policy Violations
Log incidents may result in the removal of the logs from Chrome's [log
list](log_lists.md). The decision to remove logs is made at the Chrome team's
discretion based on all information available. This typically includes the root
cause of the incidents, the log operator’s response, and the impact Chrome's
decision may have on the health of the broader CT ecosystem.

The Chrome CT Program acknowledges that many log incidents are transient. In
these cases, removal of the log from Chrome's log list may not be best outcome
for Chrome, Chrome's users, or the CT ecosystem. As a result, transient
incidents where the log operator takes steps to ensure similar incidents do not
recur typically do not result in log log removal.

Some common examples of incidents that typically do not result in removal
include:
 * Log downtime caused by a maintenance window preannounced to
   [ct-policy@](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy).
 * A log violating the MMD due to an unpredictable spike in load, subsequently
   resolved by providing additional resources or adjusting rate limits.
 * A temporary log outage caused by an outage of a 3rd-party dependency (e.g. a
   cloud provider).

In addition to incidents that prevent the log from being cryptographically
verified (e.g. signing inconsistent STHs, bit flips included in the merkle tree
structure), incidents such as the following will typically result in log
removal:
 * Logs failing to include a certificate for which the log has issued an SCT,
   even after several days.
 * Logs experiencing extended availability issues, such as when the log's
   availability over any 90 day window drops below 95%, or the log has an
   ongoing/intermittent availability issue lasting two or more weeks.

Regardless of incident severity, log operators should take steps to prevent
their logs from experiencing similar incidents in the future.

When logs are removed from Chrome's log list due to an incident, log operators
are typically encouraged to submit a replacement log (covering the same
certificate expiry window) for inclusion in Chrome's log list as soon as they're
able. This helps to ensure adequate capacity in the CT ecosystem.

Logs that are removed from Chrome's log list are typically transitioned to the
`Retired` [state](log_states.md). The Chrome team may also consider
transitioning the log to `ReadOnly` if the log operator is interested and
removing write traffic to the log is expected to return the log to a fully
healthy state.

---

## Logging Submission Policy
### Accepted Root Certificates
In order to maintain broad utility to Chrome and its users, CT logs are expected
to accept logging submissions from CAs that are trusted by default in Chrome
across all its supported platforms, including ChromeOS, Android, Linux, Windows,
macOS, iOS. If a log operator plans to restrict the set of Accepted Root
Certificates, this should be clearly stated in the CT log operator application
as well as the rationale for this restriction. **Note:** This restriction may
prevent a CT log from being accepted by Chrome for inclusion.

The CCADB offers [a
report](https://ccadb.my.salesforce-sites.com/ccadb/RootCACertificatesIncludedByRSReportCSV)
that lists all root certificates included in any of Apple's, Chrome's,
Microsoft's, or Mozilla's root stores. Logs are strongly encouraged to accept
submissions from any of these roots. Operators should also consider configuring
logs to accept submissions from roots with CAs currently under consideration for
inclusion in any of those root stores, available via a [separate CCADB
report](https://ccadb.my.salesforce-sites.com/ccadb/RootCACertificatesInclusionReportCSV).

So long as the CT log operator bug indicates which logs ingest which CCADB
reports, operators that automatically add accepted roots to reflect updates to
these reports may do so without updating their CT log operator bug on each
update.  Log operators should not automatically remove roots from logs as a
result of their removal from CCADB reports so as to avoid availability,
reliability, or accuracy issues in the CCADB report compromising the
availability of dependent logs.

### Rejecting Logging Submissions
CT logs are permitted to reject logging submissions for certificates that meet
certain conditions, such as being expired or revoked at the time the submission
was made. A logging rejection means that the CT log will not incorporate a given
certificate entry into the Merkle Tree even if the certificate chains to an
Accepted Root Certificate. Rejected logging submissions **must not** be issued
an SCT by the CT log.

If specified within the Application, a log may reject submission to log
certificates that chain up to an Accepted Root Certificate based on one or more
of the following conditions:
* **Certificate Revoked:** If the log determines that a certificate has been
  revoked by the issuing CA, it may reject the logging submission. If the log is
  unable to determine revocation status, it must accept the logging submission
  and incorporate the entry into the Merkle Tree within the log's MMD.
* **Certificate Expired:** If a logging submission includes a certificate whose
  notAfter timestamp represents a point in time before the logging submission
  was made, the log may refuse to log the certificate entry. This criteria may
  be used even by legacy non-sharded CT logs that do not set certificate expiry
  ranges.
* **TLS Server Auth EKU:** The log may reject logging submissions for
  certificates that do not contain the `id-kp-serverAuth` Extended Key Usage
  (EKU).

The primary purpose of allowing rejection of certain logging submissions is to
provide log operators with greater control over the growth and operation of
their logs while still performing their core function. Additionally, these
criteria allow logs to be shielded from certain types of Denial of Service such
as being spammed with the corpus of all expired certificates and being unable to
respond to legitimate logging submissions.

### Temporal Sharding
In order to provide ecosystem agility and to control the growth of CT log sizes,
new CT logs must be *temporally sharded*, defining a *certificate expiry range*
denoted in the form of two dates: [rangeBegin, rangeEnd). The certificate expiry
range allows a log to reject otherwise valid logging submissions for
certificates that expire before or after this defined range, thus partitioning
the set of publicly-trusted certificates that each log will accept.

In order to have their logs accepted for inclusion, log operators should deploy
and operate their logs according to the following:
* The certificate expiry ranges for CT logs must be no longer than one calendar
  year and should be no shorter than six months.
* CT logs must reject logging submissions for certificates whose notAfter
  timestamp falls outside the certificate expiry range.
* Log operators should deploy enough sharded CT logs so that their certificate
  expiry ranges cover a contiguous period of time, spanning from the current.
  time to 3-4 years in the future.
    * Many log operators find it convenient to define these ranges on the
      calendar year, so an application in 2020 would include e.g. Log2020,
      Log2021, Log2022, Log2023.
* CT logs will be removed from Chrome once their certificate expiry range has
  passed. When log operators in good standing have one of their logs removed in
  this manner, they should stand up a new CT log whose expiry range extends the
  set of contiguous expiry ranges.
    * Following the example from above, when Log2020 is removed in early 2021,
      the log operator should stand up Log2024 and apply for its inclusion,
      following the Application Process defined above.

### Rate Limiting
Rate limiting is a form of reduced log availability, and log operators are
expected to ensure that their logs operate without hitting rate limiting
whenever possible. Operators whose logs require rate limiting during normal
operation (i.e. not during a DoS attack or other acute issue) should investigate
adding caching or other techniques to ensure adequate capacity such that the
logs do not rely on rate limiting.

If rate limiting is necessary, operators should prefer per-IP rate limiting (or
other forms of per-client limiting) over shared global rate limits.

Log data availability is of paramount importance. All rate limits must be set to
ensure that all well-behaved clients can reliably retrieve log entries at a rate
greater than the growth rate of the log. For instance, if the log's typical
growth rate is `X` entries/second, and `get-entries` are limited to `Y` entries
per request, per-client limits should be no less than `ceil(X/Y)` requests/sec.
Operators must also ensure that well-behaved clients retrieving entries have a
sufficient opportunity to catch up with growth that occurred during periods of
global rate limiting. Operators are encouraged to ensure sufficiently high
limits such that clients can catch up in a reasonable period of time.

If a log is unable to provide sufficient `get-entries` capacity to ensure these
requirements, operators should apply rate limiting to `add-chain` and
`add-pre-chain` log endpoints to reduce overall load on the log. Operators
should work to ensure that the impact of reduced log availability is minimized
on time-sensitive certificate issuance, such as by specifically prioritizing
`add-pre-chain` over `add-chain` endpoints, or by more aggressively limiting
submissions of certificates with `notBefore` dates significantly in the past.

The CT log operator's bug should be kept up to date with a description of all
rate limiting policies applied to the log.

Logs that are only able to operate with rate limits that prevent typical usage
of the log by certificate submitters or monitors may be removed from Chrome's
log list for failure to provide an adequate level of service.

