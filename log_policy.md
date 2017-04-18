# Certificate Transparency Log Policy

To improve trust and security when communicating with secure services,
Chromium-derived products, such as Google Chrome, will require certificates
presented by servers to be publicly audited using Certificate Transparency.
As specified by [RFC 6962](https://tools.ietf.org/html/rfc6962), Certificate
Transparency includes a multi-party protocol for providing
cryptographically-verifiable proofs to audit the issuance and security
practices of Certificate Authorities.

To support such auditing, Chromium-derived products include a list of Logs
that are recognized to be operating in the public interest. This Certificate
Transparency Log Policy ("Policy") sets forth how a Certificate Transparency
Log Operator may have its Log recognized within Chromium, ongoing expectations
of Log Operators, and how Chromium developers may preserve the integrity of
recognized Logs. This policy may be updated by Google from time to time.

When a Log is recognized, Signed Certificate Timestamps (SCT) issued by that
Log will be granted special treatment within the Chromium user interfaces,
such as by indicating that the associated certificate certified by the SCT has
been publicly noted by the Log Operator.

## Application

To apply for a Log to be included within Chromium, the Log Operator must
[file a new bug](https://bugs.chromium.org/p/chromium/issues/entry) on the
Chromium Issue Tracker, and provide:
  * Contact Information for the Log Operator, including:
    * An email or e-mail alias that is continuously monitored by the Log
      Operator
    * A phone number
    * A list of person(s) authorized to represent the Log Operator
  * A public HTTP endpoint that responds to all Log Client Messages indicated
    in RFC 6962, Section 4
  * The Log's public key, attached as a binary file containing the DER
    encoding of the SubjectPublicKeyInfo ASN.1 structure
  * A description of the Log, including applicable policies or requirements
    for logging certificates
  * The Maximum Merge Delay (MMD) of the Log
  * All of the Accepted Root Certificates of the Log

After acceptance, Google will monitor the Log, including random compliance
testing, prior to its inclusion within Chromium. Such compliance testing will
include, but is not limited to, verifying the Log’s conformance to RFC 6962,
and confirming the Log's uptime meets the requirements of this Policy and
confirming the Log is append-only and consistent from every point of view.

To enable monitoring, log operators are asked to include Google's
["Merge Delay Monitor Root"](mmd_monitor_root.crt) in the set of Accepted Root
Certificates of their logs.

## Ongoing Requirements of Included Logs

To remain included within Chromium-derived projects, Log Operators must
operate the Log in accordance with this Policy. Log Operators must:

  * Have no outage that exceeds an MMD of more than 24 hours.
    Outages include, but are not limited to: network level outages, expiration
    of the Log’s SSL certificate, a failure to accept new Certificates to be
    logged, HTTP response status codes other than 200, or responses that
    include data that does not conform to RFC 6962.
  * Conform to RFC 6962, including the implementation of all API endpoints
    defined within Section 4 of RFC 6962
  * Not impose conditions on retrieving or sharing data from the Log
  * Have 99% uptime, with no outage lasting longer than the MMD (as measured
    by Google) 
  * Not present two or more conflicting views of the Merkle Tree at different
    times and/or to different parties.
  * Incorporate a certificate for which an SCT has been issued by the Log
    within the MMD.
  * If requested, accept certificates issued by a test CA run by Google to
    enable Google to monitor the log’s compliance to these policies.
  * Be operated in good faith, including, but not limited to each Log
    Operator:
      * Verifiably logging all certificates within the Log for which SCTs have
        been issued within the MMD
      * Maintaining the append-only property of the of the Log by providing
        consistent views of the Merkle Tree at all times and to all parties.
  * Notify the Chromium developers of any and all changes to information
    gathered during the Log Inclusion by detailing such changes in an update
    to the bug on the [Chromium Issue Tracker](https://bugs.chromium.org/p/chromium/issues/list?q=component%3AInternals%3ENetwork%3ECertTrans)
    in which they requested Log Inclusion.

Google will notify Log Operators, via announcements to the
[Chromium CT Policy Group](https://groups.google.com/a/chromium.org/forum/#!forum/ct-policy),
of changes to these requirements. Log Operators that fail to meet these
requirements will be in violation of the Log Inclusion Policy, which may
result in removal of the Log from the Chromium projects.

## Policy Violations

The Chromium developers include Logs at their sole discretion, to further
public auditability of Certificate Authorities. Upon learning of a Log’s
potential violation of this Policy, the Chromium Authors will review the
information and may take corrective actions to preserve the integrity of its
Log program. The Chromium Authors may remove Logs at any time, and for any
reason.
