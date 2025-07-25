# Certificate Transparency Log Policy
Certificate Transparency includes a multi-party protocol for providing cryptographically-verifiable proofs to audit the issuance and security practices of Certificate Authorities.

To support such auditing, Chrome includes a list of Logs that have passed an application process and are recognized to be operating in the public interest. This Certificate Transparency Log Policy ("Policy") sets forth how a Certificate Transparency Log Operator may have its Log recognized within Chrome as well as the ongoing expectations of these Log Operators. This policy may be updated by Google from time to time.

---

## Application Process
Before applying for their first CT Logs to be added to Chrome, new CT Log Operators should first read and fully comprehend the ongoing requirements for CT Logs specified in this Policy. Once a Log Operator is confident they can meet these requirements and has deployed a set of temporally-sharded CT Logs ready for application, they should follow the below process for adding these Logs to Chrome.

### New CT Log Operators
New CT Log Operators should begin their application process by first [filing a new CT Log Operator bug](https://issues.chromium.org/issues/new?component=1456813&template=0) on the Chromium Issue Tracker, and provide contact Information for the Log Operator, including:
 * An email or e-mail alias that is continuously monitored by the Log Operator, and
 * a list of person(s) authorized to represent the Log Operator when communicating with the Chrome team.

This bug will be used to track all CT Logs operated by this Log Operator for as long as any Logs operated by this organization are `Pending`, `Qualified`, `Usable`, `ReadOnly`, or `Retired`. By creating a new CT Log Operator bug, applicants are asserting they are organizationally independent from all existing CT Log Operators, which can be observed in the [log lists](log_lists.md) hosted by Google. If an organizational change occurs that alters this independence, CT Log Operators are required to notify Chrome at chrome-certificate-transparency@google.com as soon as possible.

### Existing CT Log Operators
Once the Chrome team has confirmed the Log Operator's contact information, or if an existing Log Operator is applying for additional CT Logs to be added to Chrome,  the CT Log Operator must next provide the following information about the new CT Logs in their existing CT Log Operator bug:
* A description of the Logs, including applicable policies or requirements for logging certificates, and whether these Logs are compliant with RFC6962 or static-ct-api v1.0.0.
* A JSON object (one per log) containing:
    * a public HTTP endpoint that responds to all Log Client Messages indicated in RFC 6962, Section 4, or HTTP endpoints responding to Submission and Monitoring APIs specified in [c2sp.org/static-ct-api@v1.0.0](https://c2sp.org/static-ct-api@v1.0.0), as appropriate,
    * the Log's public key, provided as a DER-encoded ASN.1 SubjectPublicKeyInfo structure, base64-encoded,
    * the SHA-256 hash of the Log's public key, base64-encoded (i.e. the LogID provided in SCTs issued by the log),
    * the Maximum Merge Delay (MMD) of the Log, and
    * the expiry range of the Log.
* The initial set of Accepted Root Certificates of the Logs.
* Whether the Logs will reject logging submissions for expired or revoked certificates.
* A description of any rate limiting policies applied to the Logs.

The JSON objects must conform to the [provided schema](inclusion_request_schema.json) and may be provided either directly in the log inclusion bug or via per-log URLs.

Note that certificate expiry ranges for a set of Logs must be contiguous, with no gaps, and each log's expiry range should be between 3 and 12 months.

After acceptance, Google will monitor the Logs, including via random compliance testing, prior to its inclusion within Chrome. Such compliance testing will include, but is not limited to, verifying the Logs' conformance to RFC 6962 or static-ct-api v1.0.0 (as appropriate), confirming the Logs' availability meets the requirements of this Policy, and confirming the Logs are append-only and consistent from every point of view.

To enable compliance monitoring, Log Operators must include Google's Merge Delay Monitor Root certificate in the set of accepted root certificates of their Logs. Log operators should expect ongoing querying of their logs from Google's compliance monitoring infrastructure throughout the lifetime of the log.

---

## Log API Specification Requirements
Prior to April 1st, 2025, all logs applying for inclusion in Chrome's log list must conform with RFC 6962. Starting April 1st, 2025, operators may additionally submit logs for inclusion that conform instead to the static-ct-api v1.0.0 C2SP specification. Insofar as is possible, Chrome's requirements are equivalent between static-ct-api and RFC 6962 logs, however:
 1. Static-ct-api logs must not specify a MMD greater than 1 minute.
 2. During the validation phase, existing operators of RFC 6962 logs included in Chrome's log list should continue to operate those logs (or RFC 6962 logs covering the same set of certificates).

---

## Ongoing Requirements of Included Logs
In order for their Logs to remain included within Chrome after first becoming `Qualified`, Log Operators must continue to operate these Logs in accordance with this Policy. Log Operators must:
* Monitor the [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy) group for relevant updates to policy or requirements for CT Log Operators.
* Incorporate a certificate for which an SCT has been issued by the Log within the MMD.
	* When Logs receive a logging submission for an already-incorporated certificate, Logs must either return an existing SCT or, if creating a new one, add another certificate entry within the MMD such that the new SCT can be verified using the Log's CT APIs
* Maintain Log availability of 99% or above.
	* Log availability is measured on a per-endpoint basis over a 90-day rolling average from all requests made to the log by the Chrome team's compliance monitoring infrastructure. The log's overall availability is represented by the minimum of all per-endpoint availabilities.
	* Behavior that results in reduced availability includes, but is not limited to: network level outages, expiration of the Log's SSL certificate, a failure to accept new Certificates to be logged (with the exception of the conditions defined in the Logging Submission Acceptance section below), HTTP response status codes other than 200, or responses that include data that does not conform to the log's corresponding API specification.
* Ensure their Logs conform to the totality of the API specification indicated in the Log's application.
* Not impose conditions on retrieving or sharing data from the Logs.
* Not present two or more conflicting views of the Merkle Tree at different times and/or to different parties.
* Accept certificates issued by Google's Merge Delay Monitor Root to enable Google to monitor the Log's compliance to these policies.
* Operate their Logs in good faith, including, but not limited to each Log Operator:
	* Verifiably incorporating all certificates into the Log for which SCTs have been issued, within the Log's MMD.
	* Maintaining the append-only property of the Log by providing consistent views of the Merkle Tree at all times and to all parties.
* Notify the Chrome team of any and all changes to information gathered during the Log Inclusion by detailing such changes in an update to the CT Log Operator bug on the [Chromium Issue Tracker](https://issues.chromium.org/issues?q=status:open%20componentid:1456813) in which they requested Log Inclusion.

Google will notify Log Operators of changes to these requirements as well as effective dates for those changes via announcements to the [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy).

---

## Incident Detection and Response
Log operators should implement proactive monitoring to detect log conditions that could lead to a policy violation or incident. In the event that a log policy violation occurs, Log Operators are expected to work to mitigate and correct those issues in a timely fashion, ensuring [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy) is kept apprised of findings and actions.
 * Incidents reported to [ct-policy@chromium.org](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy) should be acknowledged within 24 hours and followed up with the results of the subsequent investigation and mitigation measures.
 * In some circumstances, such as responding to an incident, log operators may be forced to make a decision that favors compliance with one requirement over another. To ensure that SCTs remain a strong indicator that a certificate was issued transparently, Log Operators are encouraged to implement mechanisms in their Logs that prioritize the timely inclusion and availability of log entries over the continued availability of `add-chain` and `add-pre-chain` APIs.

---

## Logging Submission Policy
### Accepted Root Certificates
In order to maintain broad utility to Chrome and its users, CT Logs are expected to accept logging submissions from CAs that are trusted by default in Chrome across all its supported platforms, including ChromeOS, Android, Linux, Windows, macOS, iOS. If a Log Operator plans to restrict the set of Accepted Root Certificates, this should be clearly stated in the CT Log Operator Application as well as the rationale for this restriction. **Note:** This restriction may prevent a CT Log from being accepted by Chrome for inclusion.

### Rejecting Logging Submissions
CT Logs are permitted to reject logging submissions for certificates that meet certain conditions, such as being expired or revoked at the time the submission was made. A logging rejection means that the CT Log will not incorporate a given certificate entry into the Merkle Tree even if the certificate chains to an Accepted Root Certificate. Rejected logging submissions **must not** be issued an SCT by the CT Log.

If specified within the Application, a Log may reject submission to log certificates that chain up to an Accepted Root Certificate based on one or more of the following conditions: 
* **Certificate Revoked:** If the Log determines that a certificate has been revoked by the issuing CA, it may reject the logging submission. If the Log is unable to determine revocation status, it must accept the logging submission and incorporate the entry into the Merkle Tree within the Log's MMD.
* **Certificate Expired:** If a logging submission includes a certificate whose notAfter timestamp represents a point in time before the logging submission was made, the Log may refuse to log the certificate entry. This criteria may be used even by legacy non-sharded CT Logs that do not set certificate expiry ranges.
* **TLS Server Auth EKU:** The Log may reject logging submissions for certificates that do not contain the `id-kp-serverAuth` Extended Key Usage (EKU).
  
The primary purpose of allowing rejection of certain logging submissions is to provide Log Operators with greater control over the growth and operation of their Logs while still performing their core function. Additionally, these criteria allow Logs to be shielded from certain types of Denial of Service such as being spammed with the corpus of all expired certificates and being unable to respond to legitimate logging submissions.

### Temporal Sharding
In order to provide ecosystem agility and to control the growth of CT Log sizes, new CT Logs must be *temporally sharded*, defining a *certificate expiry range* denoted in the form of two dates: [rangeBegin, rangeEnd). The certificate expiry range allows a Log to reject otherwise valid logging submissions for certificates that expire before or after this defined range, thus partitioning the set of publicly-trusted certificates that each Log will accept. 

In order to have their Logs accepted for inclusion, Log Operators should deploy and operate their Logs according to the following:
* The certificate expiry ranges for CT Logs must be no longer than one calendar year and should be no shorter than six months
* CT Logs must reject logging submissions for certificates whose notAfter timestamp falls outside the certificate expiry range
* Log Operators should deploy enough sharded CT Logs so that their certificate expiry ranges cover a contiguous period of time, spanning from the current time to 3-4 years in the future
	* Many Log Operators find it convenient to define these ranges on the calendar year, so an application in 2020 would include e.g. Log2020, Log2021, Log2022, Log2023.
* CT Logs will be removed from Chrome once their certificate expiry range has passed. When Log Operators in good standing have one of their Logs removed in this manner, they should stand up a new CT Log whose expiry range extends the set of contiguous expiry ranges 
	* Following the example from above, when Log2020 is removed in early 2021, the Log Operator should stand up Log2024 and apply for its inclusion, following the Application Process defined above.

### Rate Limiting
Rate limiting is a form of reduced log availability, and log operators are expected to ensure that their logs operate without hitting rate limiting whenever possible. Operators whose logs require rate limiting during normal operation (i.e. not during a DoS attack or other acute issue) should investigate adding caching or other techniques to ensure adequate capacity such that the logs do not rely on rate limiting.

If rate limiting is necessary, operators should prefer per-IP rate limiting (or other forms of per-client limiting) over shared global rate limits.

Log data availability is of paramount importance. All rate limits must be set to ensure that all well-behaved clients can reliably retrieve log entries at a rate greater than the growth rate of the log. For instance, if the log's typical growth rate is `X` entries/second, and `get-entries` are limited to `Y` entries per request, per-client limits should be no less than `ceil(X/Y)` requests/sec. Operators must also ensure that well-behaved clients retrieving entries have a sufficient opportunity to catch up with growth that occurred during periods of global rate limiting. Operators are encouraged to ensure sufficiently high limits such that clients can catch up in a reasonable period of time.

If a log is unable to provide sufficient `get-entries` capacity to ensure these requirements, operators should apply rate limiting to `add-chain` and `add-pre-chain` log endpoints to reduce overall load on the log. Operators should work to ensure that the impact of reduced log availability is minimized on time-sensitive certificate issuance, such as by specifically prioritizing `add-pre-chain` over `add-chain` endpoints, or by more aggressively limiting submissions of certificates with `notBefore` dates significantly in the past.

The log operator's chromium bug should be kept up to date with a description of all rate limiting policies applied to the log.

Logs that are only able to operate with rate limits that prevent typical usage of the log by certificate submitters or monitors may be removed from Chrome's log list for failure to provide an adequate level of service.

---

## Policy Violations
Upon learning of a Log's potential violation of this Policy, the Chrome team will review all information available, including the log operator's response, and may take corrective actions to preserve the integrity of its CT Log program and the CT ecosystem broadly.

The Chrome team includes CT Logs at their sole discretion to further public auditability of Certificate Authorities. CT Logs may be removed from Chrome at any time, and for any reason.
