---
name: yes-no-confidence
description: Evaluates yes/no (Yes/No) questions and appends a calibrated confidence score (0-100) to the answer. Use when answering binary verification, fact checks, or questions expecting a "yes" or "no" answer.
---

# Yes/No Confidence Assessor

When answering a user’s "yes/no" (or "is/are," "right/wrong," "has/have," "will/won't," "whether") judgment or factual question, provide a clear conclusion and attach a confidence score (0-100) for the answer.

## Core Rules

### 1. Trigger Conditions
- Applies to all judgmental or factual questions that can be answered directly as "yes/no," "right/wrong," "has/have," "will/won't," or "whether" (for example: "Is the Earth round?", "Is a Python list thread-safe?")
- If the user asks an open-ended or long-form discussion question (such as "Please introduce...", "How do I write..."), this format is not triggered. However, if such a discussion contains a clear yes/no judgment, only that specific judgment should be handled using this format.

### 2. Response Format
Each yes/no question should follow this structure:
1. Clear judgment: begin the response directly with "Yes" or "No" (or "Right/Wrong," "Will/Will not").
2. Core basis: briefly explain the factual reason or key limiting conditions in 1–2 sentences.
3. Confidence score: append the answer’s confidence at the end in a fixed format.

Score format:
```
Confidence: [0-100]/100
```
or
```
Certainty: [0-100]/100
```

### 3. Confidence Calibration Standards (0–100)

- 100 (absolutely certain): mathematical axioms, objective facts, fixed grammar, or rigorously proven conclusions (for example: `1+1=2`, `The molecular formula of water is H2O`).
- 85–99 (highly certain): widely accepted in academia or industry, with strong evidence; only extremely rare edge cases might differ.
- 60–84 (likely true): valid in most mainstream scenarios, but limited by environment, version, context, or local debate.
- 40–59 (debated or insufficient evidence): both sides have plausible support, or it depends on specific definitions or subjective standards.
- 15–39 (unlikely): tends toward "no," weak evidence, and probably not true.
- 0–14 (completely wrong / false proposition): explicitly disproven, or the premise is self-contradictory.

### 4. Boundary and Special Case Handling

- Premise error: If the question itself contains a false premise (for example: "Did Lu Xun and Zhou Shuren fight each other?"), the answer should directly point out the premise is incorrect ("No. Lu Xun and Zhou Shuren are the same person").
- Conditional answer: If the answer depends on specific circumstances (such as system configuration or language version), first provide the judgment under the default/mainstream condition, then explain the exception and reduce the score appropriately.

## Examples

Example 1 (objective fact):
> Question: Does the Earth revolve around the Sun?
> Answer: Yes. The Earth is one of the planets in the Solar System and orbits the Sun along an elliptical path.
> Confidence: 100/100

Example 2 (technical question):
> Question: Is a Python list thread-safe?
> Answer: No. Although CPython’s GIL makes individual bytecode instructions atomic, list operations are not inherently thread-safe. Composite operations such as "check-then-append" can fail under concurrent modification and require locking or other synchronization.
> Confidence: 95/100

Example 3 (context-dependent case):
> Question: Does using the UDP protocol for data transmission always result in packet loss?
> Answer: No. UDP itself does not guarantee reliable delivery, but in environments with good network quality and sufficient bandwidth—such as a well-functioning local network—packet loss often does not occur.
> Confidence: 85/100
