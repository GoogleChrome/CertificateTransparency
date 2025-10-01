# Certificate Transparency Log Lifecycle
## Introduction
Certificate Transparency (CT) is a technology and an ecosystem designed to
ensure that TLS certificates issued by publicly-trusted Certification
Authorities (CAs) are detectable by website operators shortly after they are
first able to validate in CT-enforcing user agents, such as Chrome. In order to
achieve this goal, user agents rely on organizations called log operators to
stand up and operate infrastructure called CT logs and apply for inclusion to be
recognized by these user agents.

The purpose of this document is to describe the lifecycle of a CT log,
represented by a set of states and state transitions, and explain what these
states mean for log operators, CAs, CT monitors, site operators, and Chrome.

---

## CT Log State Machine

```
                 +------------------------+
                 |                        |
                 |                        V
PENDING ---> QUALIFIED ---> USABLE ---> READONLY----+
   |           |   |        |   |         |         |
   |           |   |        |   |         V         |
   |           |   +--------|---+----> RETIRED      |
   |           |            |             |         V
   +-----------+------------+-------------+----> REJECTED
```

In the above state machine, the nodes represent all possible CT log states and
the directional edges represent possible state transitions. The remainder of
this document describes how CT logs transition into and out of these states,
what is expected of CT logs in these states, and finally, how the CT log states
map to Chrome behavior.

---

## `Pending`
When a log operator requests for a CT log to be added to Chrome, the CT log is
first placed into the `Pending` state. While the log undergoes its initial
compliance monitoring period, it remains in the `Pending` state until it is
either added to Chrome or a determination is made to reject the application.

**How `Pending` CT Logs transition to other states:**
* `Pending` CT logs transition to `Qualified` when they are first added to
  Chrome after a successful compliance monitoring period.
* `Pending` CT logs transition to `Rejected` if serious or sustained violations
  of the log's applicable API specification or the [CT Log
  Policy](log_policy.md) are detected during the application process, or if the
  log operator indicates they are withdrawing the application for inclusion in
  Chrome.

**Expected Log Behavior:**

While in the `Pending` state, CT logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to log Operation.

**Chrome Behavior:**

`Pending` logs are not included in the CT log list in Chrome. When evaluated in
CT-enforcing versions of Chrome, SCTs from CT logs in the `Pending` state at
time of check do not contribute towards CT Compliance for either the Embedded
SCT or the OCSP/TLS SCT criteria.

---

## `Qualified`
CT logs that successfully pass the initial compliance monitoring period are
placed in the `Qualified` state if there are no major issues observed during
this period. `Qualified` CT logs are added to the list checked into Chromium and
get included in a future version of Chrome. `Qualified` CT logs must meet an
ongoing set of compliance and availability requirements in order to remain
included in Chrome.

**How `Qualified` CT Logs transition to other states:**
* `Qualified` CT logs transition to `Usable` within a fixed period of time after
  becoming `Qualified`, so long as they continue to comply with the [CT Log
  Policy](log_policy.md).
* `Qualified` CT logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the log operator ceases operation of their CT log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT log
  being `Retired`.
* `Qualified` CT logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their Chromium CT log application. Notably, the `Qualified` to
  `Rejected` transition is not used as a more severe response to a CT log’s
  compliance issues.

**Expected Log Behavior:**

While in the `Qualified` state, CT logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to log operation.

**Chrome Behavior:**

`Qualified` CT logs are periodically imported to the list of CT logs recognized
by Chrome. When evaluated in CT-enforcing versions of Chrome, SCTs from CT logs
in the `Qualified` state at time of check contribute towards CT Compliance for
both the Embedded SCT and the OCSP/TLS SCT criteria.

---

## `Usable`
Once a CT log becomes `Qualified`, there will be a period of time in which older
versions of Chrome are still enforcing CT but are not yet aware of this newly
`Qualified` CT log. Certificates accompanied by SCTs from such a
newly-`Qualified` CT log would fail validation in these non-updated clients, so
the `Qualified` log state is insufficient on its own to indicate safeness for
production CT logging. The `Usable` log state captures this notion of safety by
indicating to CAs and site operators that all CT-enforcing versions of Chrome
now recognize a given newly-`Qualified` CT log.

Newly-`Qualified` CT logs become `Usable` when they have been added to the CT
log list for all CT-enforcing versions of Chrome. This is achieved either by
Chrome clients updating to a version in which this CT log has been added or by
older clients becoming 10 or more weeks out-of-date and thus disabling CT
enforcement. Rather than being a distinct state recognized by any given Chrome
client, the `Usable` state can be thought of as a signal to the CT ecosystem,
representing the distributed state of all CT-enforcing user agents now
recognizing these CT logs.

**How `Usable` CT Logs transition to other states:**
* `Usable` CT logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the log operator ceases operation of their CT log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT log
  being `Retired`.
* `Usable` CT logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT log application. Notably, the `Usable` to `Rejected`
  transition is not used as a more severe response to a CT log’s compliance
  issues.

**Expected Log Behavior:**

While in the `Usable` state, CT logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to log operation.

**Chrome Behavior:**

The `Usable` state is not a state that is specifically recognized by Chrome
clients and is functionally equivalent to `Qualified` and `ReadOnly` in terms of
SCTs from such logs contributing towards CT compliance.

`Usable` CT logs are imported to the list of CT logs recognized by Chrome,
usually from when they first became `Qualified`. When evaluated in CT-enforcing
versions of Chrome, SCTs from CT logs in the `Usable` state at time of check
contribute towards CT Compliance for both the Embedded SCT and the OCSP/TLS SCT
criteria.

---

## `ReadOnly`
If a log operator wishes to cease accepting certificate logging requests, they
may request that their `Qualified` or `Usable` CT log(s) be placed in the
`ReadOnly` state. CT logs that become `ReadOnly` mode are making an assertion
that they will stop issuing new SCTs, but will continue to operate the CT log in
accordance with the [Certificate Transparency Log Policy](log_policy.md).

When a log becomes `ReadOnly`, the final tree size is published to the
Google-hosted [CT Log List](log_lists.md) to signal that this log should not
grow past this point. To help ensure this behavior, CT monitors should continue
monitoring `ReadOnly` logs until they become `Retired` or `Rejected`.

**How `ReadOnly` CT Logs transition to other states:**
* `ReadOnly` CT logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the log operator ceases operation of their CT log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT log
  being `Retired`.
* `ReadOnly` CT logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT log application. Notably, the `ReadOnly` to `Rejected`
  transition is not used as a more severe response to a CT log’s compliance
  issues.

**Expected Log Behavior:**

While in the `ReadOnly` state, CT logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to log Operation.

**Chrome Behavior:**

The `ReadOnly` state is not a state that is directly recognized by Chrome
clients, but rather is treated as functionally equivalent to `Qualified` and
`Usable` in terms of CT enforcement.

`ReadOnly` CT logs are imported to the list of CT logs recognized by Chrome,
usually from when they first became `Qualified`. When evaluated in CT-enforcing
versions of Chrome, SCTs from CT logs in the `ReadOnly` state at time of check
contribute towards CT Compliance for both the Embedded SCT and the OCSP/TLS SCT
criteria.

---

## `Retired`
A `Retired` log is one that was at one point `Qualified`, but has stopped being
relied upon for the creation of new SCTs. CT logs usually enter the `Retired`
state due to a failure to adhere to the ongoing requirements outlined in the
[Certificate Transparency Log Policy](log_policy.md).

To increase the CT ecosystem’s resilience against CT log failure, existing
certificates relying on embedded SCTs that were issued before a log’s Retirement
timestamp can still contribute to CT Compliance for certificates using Embedded
SCTs. However, since they can be modified without certificate re-issuance, SCTs
delivered via OCSP or TLS must come from CT logs that are `Qualified`, `Usable`,
or `ReadOnly` at time of check.

**How `Retired` CT Logs transition to other states:**
* `Retired` CT logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT log application.

**Expected Log Behavior:**

Once a CT log becomes `Retired`, there are no longer any expectations that it
continues operation. Log operators are encouraged, but not required, to keep
`Retired` CT logs running for a time sufficient for log monitors to fully ingest
the log.

**Chrome Behavior:**

`Retired` logs are included in the [CT Log List](log_lists.md) that is shipped
in Chrome, but include both an indicator that the log is now `Retired` as well
as the corresponding Retirement timestamp.

Embedded SCTs from `Retired` logs count towards certain requirements for CT
compliance; however, as outlined in [Chrome CT Policy](ct_policy.md), in order
for a certificate to be CT Compliant, SCTs from `Retired` logs must be
accompanied by at least one SCT from a log that was `Qualified`, `Usable`, or
`ReadOnly` at time of check.

SCTs from `Retired` logs that are delivered via OCSP or TLS do not contribute
towards CT Compliance, and failure to include sufficient SCTs from `Qualified`,
`Usable`, or `ReadOnly` CT logs at time of check will result in certificate
validation failure in CT-enforcing versions of Chrome.

---

## `Rejected`
When all certificates contained in a CT log have expired and the CT log is no
longer issuing new SCTs in response to logging requests, it will transition into
the `Rejected` state. Additionally, if a CT log fails its initial compliance
monitoring period, it will skip straight to the `Rejected` state, since there
should be no still-valid certificates relying on SCTs from this log.

SCTs from `Rejected` CT logs do not contribute in any way towards CT Compliance
and should not be embedded in new certificates or delivered via OCSP or TLS.

Though `Rejected` CT logs are not included in Chrome's published [CT log
lists](log_lists.md), they are tracked internally to ensure that keys are not
reused in future CT logs applying for inclusion.

**How `Rejected` CT logs transition to other states:**
* The `Rejected` state is the terminal state of the CT log lifecycle state
  machine. Once a CT log enters the `Rejected` state, it can no longer
  transition to any of the other defined states.

**Expected Log Behavior:**

Once a CT log becomes `Rejected`, there are no longer any expectations that it
continues operation. Log operators are encouraged to turn down `Rejected` CT
logs and securely delete the log key.

**Chrome Behavior:**

`Rejected` logs are not included in the CT Log List in Chrome. When evaluated in
CT-enforcing versions of Chrome, SCTs from CT logs in the `Rejected` state at
time of check do not contribute towards CT Compliance for either the Embedded
SCT or the OCSP/TLS SCT criteria.

---

## Considerations for Chromium Embedders and other CT User Agents
With these high-level log state descriptions in mind, each CT-enforcing user
agent may wish to further specify additional context for any of these states;
however, it is important that user agent CT Policies remain compatible with one
another to ensure CAs and site operators can continue to issue and serve
certificates that will successfully validate across multiple user agents. We
welcome discussion and feedback about CT log state definitions in the
ct-policy@chromium.org discussion forum.
