# Cyber-Repair-Manual — Live Demo Verbatim Script

Reading conventions: plain text = what you say out loud. `[bracketed lines]` = actions (typing, clicking, waiting). Read the spoken lines in your own voice, don't sound robotic — the wording is a safety net, not a cage.

---

## Transition into the demo

> Now I'd like to walk you through the system running live. I'm going to give it five real user queries, and I want you to pay attention not just to whether it gets the right answer, but to *how* it decides when to answer directly, when to ask a clarifying question, and when to refuse.

---

## Scene 1 — High-Confidence Direct Match

`[Type into the app]:` **flashlight doesn't turn on at all**
`[Click "Start Diagnosis"]`

> Let's start with a straightforward case: "flashlight doesn't turn on at all."

`[Wait for the result to render]`

> The system identifies the device as Flashlight and returns a 94 percent confidence match. From the result, we see it renders the repair steps verbatim from the corpus — nothing here is generated. Every word on this screen was written by a human into our knowledge base.

---

## Scene 2 — Ambiguous Match, Interactive Clarification

`[Type into the app]:` **My rice cooker stays on warm mode and never gets hot enough to actually cook the rice**
`[Click "Start Diagnosis"]`

> Now a trickier case: "My rice cooker stays on warm mode and never gets hot enough to actually cook the rice."

`[Wait for the result to render]`

> Notice this time it doesn't commit to a direct answer. Two candidate faults score almost identically — 91.3 percent and 90.5 percent. From the result, we see the system refuses to guess between two near-tied candidates, and instead asks a clarifying yes-or-no question to disambiguate them.

`[Click "Yes" on the clarifying question]`

> I'll answer yes — and now it commits to the correct diagnosis, with the full repair card.

---

## Scene 3 — Safety-Critical Fault, DIY Suppression

`[Type into the app]:` **Sparks inside the microwave, I saw a blue flash**
`[Click "Start Diagnosis"]`

> This next one is the most important scene in this whole demo: "Sparks inside the microwave, I saw a blue flash."

`[Wait for the result to render]`

> The system is highly confident — 84 percent — that this is a microwave arcing fault, and it correctly flags it as "Requires Professional Service." Now watch closely: from the result, we see all repair steps and tools are withheld. Only the diagnosis and a safety warning are shown.

> This is enforced by a hard-coded circuit breaker in the rendering logic — not a soft instruction we're hoping the system follows. The underlying data actually contains real repair steps for this fault, but the architecture itself refuses to print them once severity is marked as professional-service-only.

---

## Scene 4 — Out-of-Scope Query, Refusal

`[Type into the app]:` **my car engine wont start and makes a clicking sound**
`[Click "Start Diagnosis"]`

> Now let's try something completely outside its domain: "my car engine wont start and makes a clicking sound."

`[Wait for the result to render]`

> From the result, we see the system cannot identify a supported appliance category, and it refuses to answer — rather than forcing a false match onto a query it has no business answering.

---

## Scene 5 — Offline Execution Verification

`[Turn off Wi-Fi, visibly, on camera]`
`[Re-type Scene 1's query]:` **flashlight doesn't turn on at all**
`[Click "Start Diagnosis"]`

> Finally, I want to prove a specific claim from our report: that this system runs fully offline. I'm turning off Wi-Fi right now — and re-running the very first query.

`[Wait for the result to render]`

> From the result, we see identical output, same speed, with zero network activity. There's no API key anywhere in this codebase, because there is nothing to call.

---

## Closing line

> That's the full pipeline in five queries: a confident answer, a clarifying question when it's genuinely unsure, a hard safety refusal when a fault is dangerous, a refusal when the query is out of scope — and all of it running completely offline.
