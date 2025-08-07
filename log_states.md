# Certificate Transparency Log Lifecycle
## Introduction
Certificate Transparency (CT) is a technology and an ecosystem designed to
ensure that TLS certificates issued by publicly-trusted Certification
Authorities (CAs) are detectable by website operators shortly after they are
first able to validate in CT-enforcing user agents, such as Chrome. In order to
achieve this goal, user agents rely on organizations called Log Operators to
stand up and operate infrastructure called CT Logs and apply for inclusion to be
recognized by these user agents.

The purpose of this document is to describe the lifecycle of a CT Log,
represented by a set of states and state transitions, and explain what these
states mean for Log Operators, CAs, CT Monitors, Site Operators, and Chrome.

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

In the above state machine, the nodes represent all possible CT Log states and
the directional edges represent possible state transitions. The remainder of
this document describes how CT Logs transition into and out of these states,
what is expected of CT Logs in these states, and finally, how the CT Log states
map to Chrome behavior.

---

## `Pending`
When a Log Operator requests for a CT Log to be added to Chrome, the CT Log is
first placed into the `Pending` state. While the Log undergoes its initial
compliance monitoring period, it remains in the `Pending` state until it is
either added to Chrome or a determination is made to reject the application.

**How `Pending` CT Logs transition to other states:**
* `Pending` CT Logs transition to `Qualified` when they are first added to
  Chrome after a successful compliance monitoring period.
* `Pending` CT Logs transition to `Rejected` if serious or sustained violations
  of the log's applicable API specification or the [CT Log
  Policy](log_policy.md) are detected during the application process, or if the
  Log Operator indicates they are withdrawing the application for inclusion in
  Chrome.

**Expected Log Behavior:**

While in the `Pending` state, CT Logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to Log Operation.

**Chrome Behavior:**

`Pending` Logs are not included in the CT Log List in Chrome. When evaluated in
CT-enforcing versions of Chrome, SCTs from CT Logs in the `Pending` state at
time of check do not contribute towards CT Compliance for either the Embedded
SCT or the OCSP/TLS SCT criteria.

---

## `Qualified`
CT Logs that successfully pass the initial compliance monitoring period are
placed in the `Qualified` state if there are no major issues observed during
this period. `Qualified` CT Logs are added to the list checked into Chromium and
get included in a future version of Chrome. `Qualified` CT Logs must meet an
ongoing set of compliance and availability requirements in order to remain
included in Chrome.

**How `Qualified` CT Logs transition to other states:**
* `Qualified` CT Logs transition to `Usable` within a fixed period of time after
  becoming `Qualified`, so long as they continue to comply with the [CT Log
  Policy](log_policy.md).
* `Qualified` CT Logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the Log Operator ceases operation of their CT Log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT Log
  being `Retired`.
* `Qualified` CT Logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their Chromium CT Log application. Notably, the `Qualified` to
  `Rejected` transition is not used as a more severe response to a CT Log’s
  compliance issues.

**Expected Log Behavior:**

While in the `Qualified` state, CT Logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to Log Operation.

**Chrome Behavior:**

`Qualified` CT Logs are periodically imported to the list of CT Logs recognized
by Chrome. When evaluated in CT-enforcing versions of Chrome, SCTs from CT Logs
in the `Qualified` state at time of check contribute towards CT Compliance for
both the Embedded SCT and the OCSP/TLS SCT criteria.

---

## `Usable`
Once a CT Log becomes `Qualified`, there will be a period of time in which older
versions of Chrome are still enforcing CT but are not yet aware of this newly
`Qualified` CT Log. Certificates accompanied by SCTs from such a
newly-`Qualified` CT Log would fail validation in these non-updated clients, so
the `Qualified` Log state is insufficient on its own to indicate safeness for
production CT Logging. The `Usable` Log state captures this notion of safety by
indicating to CAs and site operators that all CT-enforcing versions of Chrome
now recognize a given newly-`Qualified` CT Log.

Newly-`Qualified` CT Logs become `Usable` when they have been added to the CT
Log List for all CT-enforcing versions of Chrome. This is achieved either by
Chrome clients updating to a version in which this CT Log has been added or by
older clients becoming 10 or more weeks out-of-date and thus disabling CT
enforcement. Rather than being a distinct state recognized by any given Chrome
client, the `Usable` state can be thought of as a signal to the CT ecosystem,
representing the distributed state of all CT-enforcing user agents now
recognizing these CT Logs.

**How `Usable` CT Logs transition to other states:**
* `Usable` CT Logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the Log Operator ceases operation of their CT Log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT Log
  being `Retired`.
* `Usable` CT Logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT Log application. Notably, the `Usable` to `Rejected`
  transition is not used as a more severe response to a CT Log’s compliance
  issues.

**Expected Log Behavior:**

While in the `Usable` state, CT Logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to Log Operation.

**Chrome Behavior:**

The `Usable` state is not a state that is specifically recognized by Chrome
clients and is functionally equivalent to `Qualified` and `ReadOnly` in terms of
SCTs from such Logs contributing towards CT compliance.

`Usable` CT Logs are imported to the list of CT Logs recognized by Chrome,
usually from when they first became `Qualified`. When evaluated in CT-enforcing
versions of Chrome, SCTs from CT Logs in the `Usable` state at time of check
contribute towards CT Compliance for both the Embedded SCT and the OCSP/TLS SCT
criteria.

---

## `ReadOnly`
If a Log Operator wishes to cease accepting certificate logging requests, they
may request that their `Qualified` or `Usable` CT Log(s) be placed in the
`ReadOnly` state. CT Logs that become `ReadOnly` mode are making an assertion
that they will stop issuing new SCTs, but will continue to operate the CT Log in
accordance with the [Certificate Transparency Log Policy](log_policy.md).

When a Log becomes `ReadOnly`, the final tree size is published to the
Google-hosted [CT Log List](log_lists.md) to signal that this Log should not
grow past this point. To help ensure this behavior, CT Monitors should continue
monitoring `ReadOnly` Logs until they become `Retired` or `Rejected`.

**How `ReadOnly` CT Logs transition to other states:**
* `ReadOnly` CT Logs transition to `Retired` if they demonstrate a serious or
  sustained pattern of CT Policy or API specification compliance issues, or if
  the Log Operator ceases operation of their CT Log(s). Due to the inability for
  Chrome to distinguish between intentional and accidental non-compliance, such
  issues are treated as highest possible severity, which results in the CT Log
  being `Retired`.
* `ReadOnly` CT Logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT Log application. Notably, the `ReadOnly` to `Rejected`
  transition is not used as a more severe response to a CT Log’s compliance
  issues.

**Expected Log Behavior:**

While in the `ReadOnly` state, CT Logs are expected to abide by all ongoing
requirements defined in the [Certificate Transparency Log
Policy](log_policy.md), including availability requirements, API specification
compliance, and timely notification of changes to Log Operation.

**Chrome Behavior:**

The `ReadOnly` state is not a state that is directly recognized by Chrome
clients, but rather is treated as functionally equivalent to `Qualified` and
`Usable` in terms of CT enforcement.

`ReadOnly` CT Logs are imported to the list of CT Logs recognized by Chrome,
usually from when they first became `Qualified`. When evaluated in CT-enforcing
versions of Chrome, SCTs from CT Logs in the `ReadOnly` state at time of check
contribute towards CT Compliance for both the Embedded SCT and the OCSP/TLS SCT
criteria.

---

## `Retired`
A `Retired` Log is one that was at one point `Qualified`, but has stopped being
relied upon for the creation of new SCTs. CT Logs usually enter the `Retired`
state due to a failure to adhere to the ongoing requirements outlined in the
[Certificate Transparency Log Policy](log_policy.md).

To increase the CT ecosystem’s resilience against CT Log failure, existing
certificates relying on embedded SCTs that were issued before a Log’s Retirement
timestamp can still contribute to CT Compliance for certificates using Embedded
SCTs. However, since they can be modified without certificate re-issuance, SCTs
delivered via OCSP or TLS must come from CT Logs that are `Qualified`, `Usable`,
or `ReadOnly` at time of check.

**How `Retired` CT Logs transition to other states:**
* `ReadOnly` CT Logs transition to `Rejected` if all certificates contained
  therein are expired or if it is past the end of their certificate expiry range
  specified in their CT Log application. Notably, the `ReadOnly` to `Rejected`
  transition is not used as a more severe response to a CT Log’s compliance
  issues.

**Expected Log Behavior:**

Once a CT Log becomes `Retired`, there are no longer any expectations that it
continues operation. Log Operators are encouraged to turn down `Retired` CT Logs
and securely delete the Log key.

**Chrome Behavior:**

`Retired` Logs are included in the [CT Log List](log_lists.md) that is shipped
in Chrome, but include both an indicator that the Log is now `Retired` as well
as the corresponding Retirement timestamp.

Embedded SCTs from `Retired` Logs count towards certain requirements for CT
compliance; however, as outlined in [Chrome CT Policy](ct_policy.md), in order
for a certificate to be CT Compliant, SCTs from `Retired` Logs must be
accompanied by at least one SCT from a Log that was `Qualified`, `Usable`, or
`ReadOnly` at time of check.

SCTs from `Retired` Logs that are delivered via OCSP or TLS do not contribute
towards CT Compliance, and failure to include sufficient SCTs from `Qualified`,
`Usable`, or `ReadOnly` CT Logs at time of check will result in certificate
validation failure in CT-enforcing versions of Chrome.

---

## `Rejected`
When all certificates contained in a CT Log have expired and the CT Log is no
longer issuing new SCTs in response to logging requests, it will transition into
the `Rejected` state. Additionally, if a CT Log fails its initial compliance
monitoring period, it will skip straight to the `Rejected` state, since there
should be no still-valid certificates relying on SCTs from this Log.

SCTs from `Rejected` CT Logs do not contribute in any way towards CT Compliance
and should not be embedded in new certificates or delivered via OCSP or TLS.

Despite the fact that `Rejected` CT Logs are not included in either the CT Log
List shipped in Chrome or the Log List hosted by Google, they are tracked
internally to ensure that keys are not reused in future CT Logs applying for
inclusion.

**How `Rejected` CT Logs transition to other states:**
* The `Rejected` state is the terminal state of the CT Log Lifecycle state
  machine. Once a CT Log enters the `Rejected` state, it can no longer
  transition to any of the other defined states.

**Expected Log Behavior:**

Once a CT Log becomes `Rejected`, there are no longer any expectations that it
continues operation. Log Operators are encouraged to turn down `Rejected` CT
Logs and securely delete the Log key.

**Chrome Behavior:**

`Rejected` Logs are not included in the CT Log List in Chrome. When evaluated in
CT-enforcing versions of Chrome, SCTs from CT Logs in the `Rejected` state at
time of check do not contribute towards CT Compliance for either the Embedded
SCT or the OCSP/TLS SCT criteria.

---

## Considerations for Chromium Embedders and other CT User Agents
With these high-level Log state descriptions in mind, each CT-enforcing user
agent may wish to further specify additional context for any of these states;
however, it is important that user agent CT Policies remain compatible with one
another to ensure CAs and site operators can continue to issue and serve
certificates that will successfully validate across multiple user agents. We
welcome discussion and feedback about CT Log state definitions in the
ct-policy@chromium.org discussion forum.
