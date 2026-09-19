# Requirements for Software Security Engineering — Team 3 (Keycloak)

**Due:** Tue Sep 29, 2026, 11:59 PM · **Points:** 100 (counts for the whole group)
**Submission:** Link to this markdown file in our GitHub repo, submitted on Canvas.
**Tool:** [draw.io / app.diagrams.net](https://app.diagrams.net/) — instructor provided sample shape files on the Canvas assignment page (Use Case Sample.drawio, Use-Misuse Case Sample.drawio).

**Rubric:** Part 1 misuse case notation & quality (50) · Part 1 reflection (10) · Part 2 doc review (20) · Planning & reflection / project board (20)

---

## How this works

Part 1 requires **five essential interactions** between Keycloak and its environment, ideally spread across *different* external interactors (humans or systems). Each team member claims **one** interaction below and owns the full pipeline for it: use case diagram → misuse case analysis → security requirements → alignment check against Keycloak's actual features.

Part 2 does **not** split into five cases — it's a single team review of Keycloak's security-related documentation (see Part 2 section below).

### Claim board

Put your name next to one interaction. These are suggested candidates (biased toward our authorization/credential scope) — confirm or swap at the Friday meeting. Rule of thumb: five *different* interactor types, not five things one actor does.

| # | External interactor | Candidate interaction / feature | Claimed by | Status |
|---|---|---|---|---|
| 1 | End user (human) | Login / authentication via browser (password + OTP) |@Sewhenu-Ayeni | Not started |
| 2 | Realm administrator (human) | Manage user credentials & password policies via Admin Console | [@AyRidd03](https://github.com/AyRidd03) | Not started |
| 3 | Client application (system) | Obtain tokens via OIDC authorization code flow | [@JBoogieman](https://github.com/JBoogieman) | Not started |
| 4 | External identity provider (system) | Identity brokering / federated login (SAML or OIDC IdP) | | Not started |
| 5 | Directory service (system) | User federation with LDAP / Active Directory | | Not started |

Other candidates if we swap: Admin REST API automation, service accounts (client credentials grant), user self-service account console, token introspection by a resource server.

---

## Part 1 — Per-person checklist (do this for YOUR claimed interaction)

Copy this checklist under your section below and work through it in order.

- [ ] **1. Define the interaction.** One sentence: who the actor is, and the *critical feature* of Keycloak they use. Tie it back to the enabling systems in our proposal's systems engineering view.
- [ ] **2. Draw the use case diagram** in draw.io. Use cases = features Keycloak supports (not user goals in the abstract). Keep it simple at first — actor, 2–4 use cases, `<<include>>` dependencies where real (e.g., Login includes Password Hashing).
- [ ] **3. Add misuse cases.** Pick a misuser contextualized to our environment — the *name* should convey motive, resources, attack of choice, and access (e.g., "Credential-stuffing botnet operator with breached password lists," not "Hacker"). Start from the threats in our proposal.
- [ ] **4. Iterate.** Go back and forth: misuse case threatens a use case → add a security use case that mitigates it → ask what threatens *that* → repeat until you hit specific functional security requirements Keycloak could implement. **Prioritize mitigations implemented in Keycloak itself, not the environment.** Every misuse case must be addressed by some use case.
- [ ] **5. Use proper notation** (class materials): white ovals = use cases, black/shaded ovals = misuse cases, `<<threatens>>` and `<<mitigates>>` arrows, misusers on the opposite side. Arrange to reduce clutter.
- [ ] **6. Optionally run your diagram description through an AI prompt** to find missed misuse cases (instructor's sample prompt is on the Canvas page). Save the prompt you used — we need one team example plus a reflection on whether it helped.
- [ ] **7. List your derived security requirements** — numbered, specific, functional ("Keycloak shall lock an account after N failed attempts," not "the system should be secure").
- [ ] **8. Alignment check:** for each requirement, does Keycloak actually advertise/implement it? Cite Keycloak docs or code (links). Note gaps.
- [ ] **9. Export your final diagram** (PNG + keep the .drawio source in the repo) and embed it in your section.
- [ ] **10. Log your tasks** on the GitHub Project Board and write your **individual reflection** (what did you learn, what was most useful).

---

### Interaction 1: <title> — <name>

**Interaction description:**
*(1–2 sentences: actor, feature, why it's essential)*

**Use/misuse case diagram:**
`![Diagram](images/usecase-1.png)`

**Misuser profile:** *(name, motive, resources, attack of choice, access)*

**Iteration narrative:** *(brief: misuse case → countermeasure → next misuse case → …)*

**Derived security requirements:**

| ID | Requirement | Addresses misuse case | Implemented in Keycloak? (doc/code link) |
|---|---|---|---|
| SR-1.1 | | | |
| SR-1.2 | | | |

**Alignment observations:** *(sufficiency of Keycloak's features vs. what the analysis expects)*

---

### Interaction 2: <title> — <name>
*(same structure as above)*

### Interaction 3: <title> — <name>
*(same structure)*

### Interaction 4: <title> — <name>
*(same structure)*

### Interaction 5: <title> — <name>
*(same structure)*

---

## Part 1 — Team-level items (shared, assign at meeting)

| Task | Owner | Status |
|---|---|---|
| Confirm the 5 interactions cover different interactor types (no overlap) | Team — Friday mtg | |
| AI prompt example + reflection on its usefulness for improving diagrams | | |
| Summary of alignment findings across all 5 cases (sufficiency of Keycloak's security features vs. misuse case expectations) | | |
| Compile individual reflections into one team reflection | | |
| GitHub Project Board up to date + link in report: `<link here>` | | |
| Final assembly/formatting of this file + Canvas submission | | |

## Team Reflection (Part 1)

*(Compiled from individual reflections — each member answers: What did you learn? What did you find most useful?)*

---

## Part 2 — OSS documentation review (20 pts, team-level)

This part is **not** split into five cases. It's one deliverable: review Keycloak's **security-related configuration and installation documentation** and summarize what's missing or could be improved. The instructor's angle: docs contributions are an easy on-ramp to the open-source community.

Suggested split if we want everyone touching it — each person reviews one doc area for their claimed interaction's feature (e.g., #1 reviews authentication/OTP config docs, #3 reviews client/OIDC setup docs, #5 reviews LDAP federation docs), then one person merges observations.

**What to produce:**

| Doc area reviewed | Reviewer | Observations (missing / unclear / could improve) |
|---|---|---|
| Server installation & hardening guide | | |
| Authentication / credential configuration | | |
| Client & token configuration | | |
| Federation / brokering configuration | | |
| Other: | | |

**Summary of observations:** *(what could be improved or is missing, overall)*

*(Optional stretch: note whether any finding is worth an actual docs issue/PR to the Keycloak project.)*

---

## Submission checklist (before Sep 29)

- [ ] All 5 interaction sections complete with embedded diagrams
- [ ] Every misuse case is mitigated by a use case in its diagram
- [ ] AI prompt + reflection included
- [ ] Team reflection compiled
- [ ] Part 2 summary complete
- [ ] Project board link works and shows task assignments
- [ ] Canvas submission: link to this file in the repo
