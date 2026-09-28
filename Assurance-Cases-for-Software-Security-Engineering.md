### Claim board
 
Put your name next to one row. The "starting point" column is just a suggestion carried over from the SSE interactions (five different entities) — confirm or swap at the Monday meeting.
 
| # | Starting point (suggested, from SSE) | Top-level claim | Owner | Status |
|---|---|---|---|---|
| 1 | End user — browser login + OTP | | | Not started |
| 2 | Realm administrator — credential & password policy management | | | Not started |
| 3 | Client application — OIDC authorization code flow / tokens | | | Not started |
| 4 | External identity provider — identity brokering | | | Not started |
| 5 | Directory service — LDAP / AD user federation | | | Not started |
 
---

## Part 1 — Per-person checklist (do this for YOUR claim)
 
Copy this checklist into your GitHub issue and work through it in order.
 
- [ ] **1. Draft your top-level claim.** Outcome, not mechanism. Check it against the instructor's good-claim checklist: (1) entity relevant to the argument, (2) critical property of that entity, (3) value for the property and related uncertainty. Add it to the claim board.
- [ ] **2. Start your diagram** in draw.io from `Assurance Case.drawio`. Top claim at the top; add a context element if a term needs scoping.
- [ ] **3. Add rebuttals** ("Unless …") — reasons a stakeholder would doubt the claim. Our SSE misuse cases and proposal threats are the obvious source.
- [ ] **4. Eliminate each rebuttal** with a sub-claim (or evidence), and repeat until every branch ends in evidence.
- [ ] **5. Check every evidence node** — noun phrase only, something tangible/measurable (a report, a test result, a config, a log, a scan). Add an undermine where the evidence itself could be doubted.
- [ ] **6. Proofread** every element for wording, notation, and typos (graded).
- [ ] **7. Export** — keep the source at `diagrams/assurance-case-claim-N.drawio`, export `diagrams/assurance-case-claim-N.png`, embed it in your section below.
- [ ] **8. Fill your Part 2 table** — for each evidence node in your diagram, mark whether Keycloak has it, can make it available, or needs extra effort, and note the gap.
- [ ] **9. Log your tasks** on the GitHub Project Board and add your **individual reflection** (issue linked below).
---
 
### Claim 1: `<top-level claim>` — `<@owner>`
 
**Top-level claim:**
 
**Assurance case diagram:**
![Claim 1 Assurance Case](diagrams/assurance-case-claim-1.png)
 
---
 
### Claim 2: `<top-level claim>` — `<@owner>`
 
**Top-level claim:**
 
**Assurance case diagram:**
![Claim 2 Assurance Case](diagrams/assurance-case-claim-2.png)
 
---
 
### Claim 3: `<top-level claim>` — `<@owner>`
 
**Top-level claim:**
 
**Assurance case diagram:**
![Claim 3 Assurance Case](diagrams/assurance-case-claim-3.png)
 
---
 
### Claim 4: `<top-level claim>` — `<@owner>`
 
**Top-level claim:**
 
**Assurance case diagram:**
![Claim 4 Assurance Case](diagrams/assurance-case-claim-4.png)
 
---
 
### Claim 5: `<top-level claim>` — `<@owner>`
 
**Top-level claim:**
 
**Assurance case diagram:**
![Claim 5 Assurance Case](diagrams/assurance-case-claim-5.png)
 
---

## Part 1 — AI-assisted improvement (team-level)
 
The assignment asks for **one** prompt the team used to improve our assurance case, plus a reflection on its usefulness. The instructor's sample prompts (claim-phrasing and rebuttal brainstorming) are on the Canvas page — fine to start from those.
 
**Prompt used:**
 
```text
<paste the prompt>
```
 
**Reflection on usefulness:**
 
---
