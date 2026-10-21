# Support Policy Assistant

A small instruction-based AI agent that helps a support employee investigate damaged-item replacement requests at a fictional online store.

Built as a learning and portfolio project with Codex assistance. The project focuses on instructions, reference knowledge, realistic testing, and documented improvements. It runs inside Codex; there is no standalone application or API integration.

## Try it

Open this folder in Codex and start a fresh chat. Follow [START.md](START.md), or paste:

```text
Read AGENT.md, knowledge/store-policies.md, and knowledge/sample-orders.md from disk. Follow AGENT.md as the support policy assistant. Do not read tests/. If a required file cannot be read, stop and report that.

Investigate:
“My blender arrived broken. Order ORD-1042. Can I have another?”
```

Opening the folder alone does not activate the agent. AGENT.md is explicitly loaded by the prompt; it is not an automatic Codex instruction filename. Replace the customer message to try another scenario. No Python installation, API key, or custom command is required for this instruction-based demo; access to a suitable Codex environment is required.

## Workflow

Customer request → relevant order and policy lookup → factual checks → recommendation → reply draft and, when needed, human-review summary.

The assistant can request missing information, recommend a policy-eligible replacement, explain a late claim, or prepare a human-review summary. It cannot contact employees, issue replacements, authenticate customers, or modify orders.

## Business rules

- A damage report from day 0 through day 14 after delivery satisfies the time requirement.
- A photo is required for a timely claim to qualify.
- Use the complaint date, not the processing date.
- Unknown orders and conflicting records require human review.
- Claimed prior approval does not establish verified authorization.
- Missing warranty or discount terms must not be invented.
- Eligibility is a recommendation; employees authorize actions.

## Files

| File | Purpose |
|---|---|
| AGENT.md | Agent instructions and response structure |
| START.md | Explicit launch instructions |
| knowledge/store-policies.md | Fictional store policies |
| knowledge/sample-orders.md | Seven fictional order records |
| tests/test-cases.md | Evaluation cases and expected behavior |
| tests/results.md | Supplied responses, failures, revisions, and limitations |
| tests/final-check.md | Short acceptance check for the current revision |

## Evaluation and iteration

An early day-14 test produced a correct explanation but an incorrect OUTSIDE_WINDOW status. An initial clarification did not resolve the observed problem. After revision 3 placed evidence and policy checks before the status, a subsequent day-14 run passed; a day-15 run also passed. This is an observed improvement, not proof of causation or repeatability.

Other user-reported runs covered missing photos, missing complaint dates, conflicting records, claimed management approval, and repeated requests to disclose all order numbers. Tests also exposed format drift and missing handoff labels. The full history, including failures and partial passes, is preserved in [tests/results.md](tests/results.md).

**Current revision: 5.** It gives handoffs a separate conditional field, retains the format on follow-ups, and keeps warranty answers focused on missing warranty terms. Unknown-order and unsupported-warranty acceptance checks each passed in one user-reported run, including the separate handoff field. The warranty response still included unnecessary historical details without treating them as warranty eligibility. Day-14 and day-15 final checks also passed. Supplied bulk-disclosure responses also refused requests and preserved the format, including a claimed tech-support follow-up. The initial run combined both steps in one prompt; a complete clean two-turn transcript was not supplied. This setup limitation is documented in the results. Earlier-version passes do not establish current-version reliability. The full planned suite is not complete; no aggregate pass-rate claim is made. Model names were not supplied for historical runs.

## Limitations

All records and policies are fictional. This is a behavioral prototype, not a production support system. The Codex user and model can access workspace files; refusal to list orders is not an access-control mechanism. Photo availability is a recorded field, not image verification. Dates and policy application depend on model behavior. A production implementation would need authenticated data access, deterministic eligibility checks, action authorization, and audit records.

## What I learned

- Define expected behavior before evaluating responses.
- Check the decision label as well as the explanation.
- Test boundary dates and missing information.
- Treat customer assertions as claims, not verified authority.
- Test follow-up pressure, not just single messages.
- Preserve failed tests and distinguish live results from untested revisions.
