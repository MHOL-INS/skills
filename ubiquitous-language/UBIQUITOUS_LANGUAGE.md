# Ubiquitous Language

This glossary defines shared domain language for Advisor, DocFix, and adjacent teams.
Use the canonical term exactly as written to reduce handoff friction and reporting ambiguity.

## Incident and Support Flow

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Incident** | A customer- or service-impacting event that requires coordinated investigation, ownership, and tracked resolution. | issue, case, sag, problematik |
| **Alert** | A monitoring signal that may indicate an incident and must be correlated before incident-level decisions are made. | alarm row, warning line, advarsel |
| **Ticket** | A tracked support work item in Zendesk used to coordinate work, communication, and status for an incident context. | zendesk case, support sag, billet |
| **Service Window** | The approved time period where remediation may be executed with agreed risk. | maintenance slot, driftvindue, vindue |

## Monitoring and Detection

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Signal Source** | The monitoring system that produced an alert or metric used in diagnosis. | feed, source system, kilde system |
| **Failure Pattern** | A repeatable sequence of failures with shared triggers, timing, or error signature. | recurring bug, gentagen fejl, monster |
| **Severity** | The standardized impact level used to prioritize response and communication urgency. | priority only, hast, alvorlighed niveau |
| **Noise** | Alert activity that does not require action because it has no meaningful operational impact. | false alarm, stoej, ignorerbar fejl |

## Data Platform Delivery

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Data Product** | A governed dataset or model delivered for a defined business consumer and SLA. | report data, data output, datasat |
| **Pipeline Run** | A single execution instance of a data pipeline with traceable status and timing. | job, koersel, pipeline job |
| **Data Contract** | The agreed schema, semantics, and quality rules between producer and consumer. | format expectation, aftale om felter, schema wish |
| **Data Freshness** | The measured age of delivered data against the expected update cadence. | latency only, data alder, forsinkelse |

## Integration Platform Messaging

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Message Envelope** | The transport-level metadata and payload wrapper used for routing and processing rules. | message body only, pakke, beskedramme |
| **Dead-letter Message** | A message moved out of normal flow after failed processing or policy violations. | poison only, deadletter item, doedbrev |
| **Retry Policy** | The configured rules that govern automatic reprocessing attempts after transient failure. | retry loop, genforsoeg logik, resend script |
| **Idempotent Processing** | Processing behavior that produces the same business outcome when the same message is reprocessed. | duplicate-safe-ish, sikker nok, engangskorrektion |

## Advisory and Optimization

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Finding** | A validated and evidence-backed observation that may require action, monitoring, or communication across both Advisor and DocFix. | Advisor finding, DocFix finding, fund, iagttagelse |
| **Recommendation** | A proposed change linked to a finding with expected benefit and trade-offs. | suggestion, forslag, ide |
| **Savings Estimate** | A quantified projection of cost reduction based on explicit assumptions and scope. | rough saving, besparelse cirka, gut feel |
| **Risk Exposure** | The documented likelihood and impact of negative outcomes if no change is made. | risk note, risiko kommentar, fare |

## Scanning and Diagnostics

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Scan Scope** | The explicit boundaries of tenants, subscriptions, resources, and time window included in a scan. | full scan-ish, scan area, omfang |
| **Collector** | A specialized diagnostic component that gathers one domain-specific dataset. | script, scanner thing, indsamler script |
| **Diagnostic Snapshot** | A time-stamped state capture used for analysis, comparison, and reproducibility. | dump, udtraek, quick export |
| **Coverage Gap** | A known missing area where expected diagnostic data is absent or incomplete. | missing data, hul, blind spot |

## Patching and Remediation

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Remediation Action** | A concrete technical change executed to reduce or remove a confirmed risk or failure cause. | fix, patch task, rettelse |
| **Patching Session** | A planned execution window that bundles one or more remediation actions with pre-checks, verification, and communication. | patching only, patch run, patch forloeb |
| **Rollback Plan** | A predefined and testable sequence to return to prior state if remediation fails. | undo idea, fallback thought, tilbage plan |
| **Verification Check** | A post-change validation proving both intended effect and no critical regression. | smoke only, test ping, kontrol punkt |
| **Residual Risk** | The risk that remains after remediation and must be accepted, monitored, or further reduced. | remaining issue, rest risiko, efter risiko |

## Troubleshooting and RCA

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Hypothesis** | A testable explanation for observed behavior used to guide evidence collection. | guess, antagelse, mavefornemmelse |
| **Evidence** | Verifiable data points that support or refute a troubleshooting hypothesis. | notes, indtryk, observation only |
| **Root Cause** | The primary causal condition that, if removed, prevents recurrence of the incident pattern. | trigger only, symptom cause, rodfejl |
| **Contributing Factor** | A secondary condition that increases likelihood or impact but is not the root cause. | side cause, medvirkende ting, ekstra fejl |

## Documentation and Knowledge

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Runbook** | An operational guide with ordered steps, decision points, and verification outcomes. | wiki page, guide note, drejebog note |
| **Knowledge Article** | Reusable documentation focused on diagnosis, resolution patterns, and context. | doc, artikel note, tekst |
| **Session Log** | A chronological record of actions, decisions, and evidence produced during a work session. | transcript, chat history, referat |
| **Change Record** | A formal summary of what changed, why, when, and how it was verified. | commit note, aendrings note, aendringstekst |

## Communication with Customers and Colleagues

| Term | Definition | Aliases to avoid |
|---|---|---|
| **Customer Update** | A concise status message focused on impact, current state, next step, and expected timing. | quick ping, statusmail only, kunde note |
| **Internal Note** | A technical team-facing update that can include detailed diagnostics and operational detail. | customer text draft, intern kommentar only |
| **Action Owner** | The explicitly named role or person accountable for completing the next agreed action. | someone, vi, teamet |
| **ETA** | The best current estimate for completion time including uncertainty where relevant. | asap, soon, hurtigst muligt |

## Relationships

- One **Incident** can be detected by `0..n` **Alerts**, and each **Alert** should map to `0..1` active **Incident** at a time.
- One **Alert** may create `0..1` **Ticket**, while one **Ticket** should track exactly one primary **Incident**.
- One **Ticket** can include `1..n` **Findings**, and each **Finding** should be linked to `1..n` **Evidence** points.
- One **Finding** can drive `0..n` **Recommendations**, and each **Recommendation** should reference exactly one originating **Finding**.
- One **Recommendation** can be implemented by `0..n` **Remediation Actions**, and each **Remediation Action** can be grouped into `0..1` **Patching Session**.
- One **Remediation Action** must include `1..n` **Verification Checks**, and unresolved outcomes should be captured as **Residual Risk**.
- One **Root Cause** can explain `1..n` **Incidents** within the same **Failure Pattern**, while **Contributing Factors** provide additional context only.
- One **Runbook** can standardize many **Remediation Actions** and **Verification Checks** for repeatable execution.
- One **Customer Update** should reference at least one confirmed **Finding**, the next **Action Owner**, and an **ETA**.

## Example dialogue

1. Support Engineer: "We have one **Incident** with related **Alerts** from ADF and Service Bus; I am opening one **Ticket** for coordinated tracking."
2. Platform Engineer: "My **Hypothesis** is lock expiry, and current **Evidence** is lock-lost exceptions plus increasing delivery count on dead-lettered messages."
3. Advisory Engineer: "I added a **Finding** about under-sized lock duration and a second **Finding** on rising **Risk Exposure** from repeated retries."
4. Operations Lead: "Execute a **Remediation Action** in the approved **Service Window** inside today\'s **Patching Session**, and run all **Verification Checks** from the **Runbook**."
5. Cost Analyst: "I attached a **Savings Estimate** and a **Recommendation** for right-sizing follow-up after stability is confirmed."
6. Support Engineer: "I will send a **Customer Update** with impact, ETA, and the named **Action Owner**, and keep detailed diagnostics in an **Internal Note**."

## Flagged ambiguities

| Ambiguity | Why it is risky | Recommendation |
|---|---|---|
| Finding vs Recommendation | Teams may report proposals as facts, causing premature commitments and noisy reporting. | Use a two-step rule: create **Finding** only after linked **Evidence**, then create **Recommendation** if action is proposed. |
| Incident vs Alert | Parallel workstreams appear when each alert is treated as a separate incident. | Triage by correlation key (time, service, customer impact) and keep one **Incident** until separation is proven. |
| Remediation Action vs Patching Session | Teams can mark patch windows complete even when individual changes remain unverified. | Track completion at both levels: each **Remediation Action** needs verification, and the **Patching Session** closes only when all actions are verified or deferred with risk. |
| Remediation Action vs Verification Check | Changes may be marked complete without measurable outcome. | Require `expected outcome`, `actual result`, and `timestamp` for every **Verification Check** linked to the action. |
| Root Cause vs Contributing Factor | RCA quality drops when secondary conditions are labeled as primary cause. | Record exactly one primary **Root Cause** statement and capture additional conditions as **Contributing Factors** with evidence references. |
| Customer Update vs Internal Note | Technical detail can leak externally or customer-impact detail can be omitted internally. | Use a fixed template: **Customer Update** = impact, status, next step, ETA; **Internal Note** = diagnostics, commands, evidence, decision log. |
| Runbook vs Knowledge Article | Teams can execute narrative guidance that lacks safe decision points. | Require operational steps from a **Runbook** during incidents and update **Knowledge Article** only after incident closure. |
