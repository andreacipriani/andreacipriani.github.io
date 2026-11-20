---
layout: post
title: The pyramid of AI coding
date: 2026-05-03 00:00:00
description: How to balance AI involvement across tasks — and why your code infrastructure matters more than ever.
giscus_comments: false
---

The testing pyramid gave us a simple mental model for balancing effort across test types. We visualized the cost of E2E tests and agreed as a collective that they should be a minority of the test coverage. The same thinking applies to AI coding — and most teams are getting it wrong.

The two failure modes I see: developers babysitting every AI-generated change as if it were radioactive, or blindly merging everything because "the tests pass." Neither scales. Neither makes you better.

Here's the reframe: **developer time is now the scarce resource, not coding capacity.** The question stops being "can AI do this?" and becomes "where does my judgment add irreplaceable value?"

---

## The pyramid

```
  ▲ hard to verify
  │
  │            /\
  │           /  \
  │          /    \
  │         /      \
  │        / manual \
  │       /──────────\
  │      / you drive  \
  │     /──────────────\
  │    /   AI drives    \
  │   /──────────────────\
  │  /     autopilot      \
  │ /──────────────────────\
  ▼ easy to verify
```

_Axis: verification confidence — how easy it is to confirm the output is correct. Unlike the testing pyramid (where tiers map to speed and cost), here a task sits lower when you can check it without deeply understanding it, and moves up as verification itself requires judgment._

### Autopilot

Boilerplate, adding tests for existing code, renaming, documentation, simple CRUD, linting fixes. This is also where all tooling and non-user-facing code lives — the kind of work AI can not only do but autonomously improve over time. The output is mechanically verifiable: it compiles, tests pass, the diff is bounded and obvious. No review needed. Let it run and ship it.

### AI drives

New features with clear specs, refactors across files, API integrations. AI has high confidence but the blast radius is wider. You're in the passenger seat: a code review is your checkpoint, not because you distrust the AI, but because the cost of a mistake is higher and a second pair of eyes takes minutes.

### You drive

Complex business logic, security-sensitive code, architectural decisions. You're at the keyboard. AI is your copilot — suggesting the next line, flagging the edge case, generating the boilerplate inside the function you're writing. You steer.

### Manual gears

Race conditions. Memory bugs. Performance puzzles that require holding the entire call stack in your head. Subtle product decisions masquerading as bugs. Anything where explaining the problem to AI takes longer than solving it. Just you and the code.

---

The key difference from the testing pyramid: in testing, tier placement is about **speed and cost**. Here it's about **confidence in verification** — a task belongs at the base when you can verify the output without deeply understanding it. It moves up as verification itself starts requiring judgment.

---

## Where does a task belong?

The instinct is to map AI capability to human notions of complexity. That's the wrong lens.

**Complexity for an agent is not the same as complexity for a human.** A large-scale refactor — migrating thousands of lines from a delegate pattern to async/await — feels daunting to a developer. For an agent it's mechanical: a clear rule, applied consistently across files, with a compiler that confirms correctness immediately. That sits at the base of the pyramid. Conversely, a layout bug that only appears on a specific device, in a specific locale, after a specific sequence of taps — a senior engineer might fix it in twenty minutes, but an agent will spiral in circles, because there is no automated signal telling it whether it got closer or further from the answer.

Think of it like medicine. Reading an MRI contains millions of data points and requires years of training to interpret accurately — AI already does it better than most radiologists. But deciding whether a patient with a mild cough needs antibiotics or just rest requires listening, context, and the judgment to recognize that the real prescription is reassurance, not medication. Pattern recognition at scale: machines. Contextual judgment with consequences: humans.

The same division runs through codebases. A deterministic algorithm, a data pipeline, a migration script — these have ground truth. You can run them, diff the output, verify correctness automatically. UI and user interactions are the opposite: subjective, context-dependent, impossible to fully specify. A pixel two points off might be a bug or an intentional design choice. An animation that feels slightly wrong is nearly impossible to write a test for.

Which means different codebases — and different parts of the same codebase — naturally sit at different heights. There is no universal pyramid. You calibrate it by asking two questions about each task:

**1. How confident are we in the output — and can the AI verify it itself?**
The strongest signal is whether the AI can close its own feedback loop: run tests, check types, lint, diff against a spec. High self-verifiability means lower tier. When verification requires a human to *experience* the feature, open the app, or apply judgment that no test captures, the task moves up.

**2. What are the consequences of a wrong implementation?**
A broken linting rule is caught in CI and costs nothing. A wrong calculation in a payment flow ships to users. The blast radius matters as much as the probability of error. High confidence and low consequences: autopilot. Low confidence and high consequences: you drive, or manual gears.

---

## The hidden lever: code infrastructure

Here's the part most articles skip. The more tasks you push to the base of the pyramid — where AI runs freely — the more you need to invest in the guardrails that make that safe.

This isn't new work. It's the same investment in linters, modular architecture, and automated checks you always knew you should make. But AI coding makes the ROI impossible to ignore. Good infrastructure is a multiplier: it lets more tasks live at the base, which frees developer time, which you then spend on the tip where only you can go.

Bad infrastructure forces everything up the pyramid. If AI can generate code that compiles but violates your architecture, you're back to reviewing everything. You've gained a fast typist, not a collaborator.

### What this looks like in practice

**Enforce layer boundaries at the compiler level.** In a modular iOS codebase, your domain layer shouldn't know UIKit exists. Instead of relying on code review to catch it, encode it as a rule. With SwiftLint:

```yaml
custom_rules:
  no_uikit_in_domain:
    name: "No UIKit in Domain"
    regex: "^import UIKit"
    included: ".*/Domain/.*\\.swift"
    message: "Domain layer must not import UIKit."
    severity: error
```

Now AI can generate as much domain code as it wants. It literally cannot put UI logic in the wrong place.

**Forbid direct dependencies between modules.** In a feature-modular architecture, you don't want AI-generated code in a `ProfileFeature` module reaching directly into `PaymentsFeature`. Define the rule explicitly:

```yaml
custom_rules:
  no_cross_feature_imports:
    name: "No direct cross-feature imports"
    regex: "^import (Payments|Auth|Settings)Feature"
    included: ".*/Profile/.*\\.swift"
    message: "Features must communicate through shared interfaces, not direct imports."
    severity: error
```

The AI follows your architecture not because it understands it, but because violating it causes a build error.

The principle generalizes: every architectural constraint you leave implicit is a constraint the AI will eventually violate. Make them explicit and mechanical. The investment pays back the moment you stop reviewing things that a linter could have caught.

---

AI coding doesn't make architecture less important. It makes it the most important thing you do.
