# Diagram guide — Assurance Cases

Start every diagram from the instructor's `Assurance Case.drawio` (Canvas assignment page) so notation stays consistent.

**File naming:** `assurance-case-claim-N.drawio` (source) + `assurance-case-claim-N.png` (export embedded in the report). Commit your own files so your contribution shows in history.

## Notation

| Element | Shape | Wording rule | Needed? |
|---|---|---|---|
| **Claim** (top / sub) | Rectangle | Outcome predicate: *entity + critical property + value/uncertainty*. Not a mechanism. | Required |
| **Rebuttal** | Note shape | "Unless …" — short | Required |
| **Evidence** | Circle | **Noun phrase only**, tangible and measurable. No verbs. | Required, every branch ends here |
| **Context** | Rounded rectangle | Scopes a term in the claim | As needed |
| **Undermine** | Note shape on evidence | "Unless …" doubt about the evidence | As needed |
| **Inference rule / Undercut** | Blue process shape / note | "If … then …" / "Unless …" | Optional (instructor: advanced) |

**IDs:** prefix with your claim number so the five diagrams never collide: `C1`, `C1.1`, `R1.1`, `CT1.1`, `E1.1`, `UM1.1`.

## Wording

| | Example | Why |
|---|---|---|
| ❌ Claim | "The system uses AES encryption." | Technology (means), not an assured outcome |
| ✅ Claim | "The system minimizes information disclosure during communication." | Outcome + property |
| ❌ Evidence | "Tests show passwords are hashed" | Verb phrase, which makes it a claim |
| ✅ Evidence | "Physical test report", "Lab procedures" | Noun phrase, tangible |

## Argument shape (instructor's sample, simplified)

Claim → "Unless" rebuttal → sub-claim that eliminates the doubt → … → evidence.

```mermaid
flowchart TD
    C1["Top-Claim C1<br/>Tweety can fly"]
    CT1("Context CT1<br/>Tweety is an animal")
    R1>"Rebuttal R1<br/>Unless Tweety is not a bird"]
    C2["Sub-Claim C2<br/>Tweety is a winged bird"]
    R2>"Rebuttal R2<br/>Unless Tweety is handicapped"]
    R3>"Rebuttal R3<br/>Unless Tweety is a penguin"]
    C3["Sub-Claim C3<br/>Tweety is physically able"]
    C4["Sub-Claim C4<br/>Tweety is a member of a flying bird species"]
    E1(("Evidence E1<br/>Physical test report"))
    E2(("Evidence E2<br/>Flying Tweety sightings"))
    E3(("Evidence E3<br/>Tweety's DNA test results"))
    UM1>"Undermine UM1<br/>Unless the DNA test was contaminated"]
    C5["Sub-Claim C5<br/>The DNA sample has no cross-contamination"]
    E4(("Evidence E4<br/>Lab procedures"))

    C1 --- CT1
    C1 --- R1 --- C2
    C2 --- R2 --- C3
    C2 --- R3 --- C4
    C3 --- E1
    C3 --- E2
    C4 --- E3 --- UM1 --- C5 --- E4

    classDef claim fill:#ffffff,stroke:#333,color:#000
    classDef defeater fill:#fff4c2,stroke:#b59b00,color:#000
    classDef evidence fill:#e6f2ff,stroke:#2b6cb0,color:#000
    classDef context fill:#f0f0f0,stroke:#666,color:#000
    class C1,C2,C3,C4,C5 claim
    class R1,R2,R3,UM1 defeater
    class E1,E2,E3,E4 evidence
    class CT1 context
```
