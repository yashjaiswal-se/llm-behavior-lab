# llm-behavior-lab
Empirical experiments exploring inference-time behavior of large language models, with a focus on sampling dynamics, stability, and failure modes.



This repository is a research and experimentation lab focused on **inference-time behavior of Large Language Models**.  
It studies how sampling parameters, instruction hierarchy, and uncertainty interact to produce real-world failure modes such as repetition, hallucination, soft refusals, and fake compliance.



---

## Core Mental Model

LLMs do **constraint satisfaction**, not instruction execution.

They do not:
- “follow the last instruction”
- “become creative with higher temperature”
- “hallucinate randomly”

They **optimize output within allowed probability mass and constraints**.

Once you understand that, their behavior becomes predictable.

---

## What This Repo Covers

### 1. Sampling Dynamics (Temperature, Top-p, Top-k)

You will find experiments and notes that establish the **non-negotiable order of operations**:

1. **Temperature** reshapes the probability distribution  
2. **Top-p / Top-k** truncate the distribution  
3. **Sampling** selects among survivors  

Key truths explored:
- Temperature controls *confidence enforcement*, not creativity
- Top-p is probability-aware and adaptive
- Top-k is a hard cap on chaos, not intelligence
- Collapse is usually token starvation, not “low temperature”
- Most diversity is decided in the **first 10–30 tokens**

> Sampling controls which thoughts escape the model — not what the model thinks.

---

### 2. Instruction Hierarchy & Constraint Strength

The lab formalizes instruction hierarchy as a **constraint dominance system**, not a rule ladder.

**Authority order (highest → lowest):**
- System / Safety
- Developer
- User
- Tool / Context (facts only, no authority)

Key ideas tested:
- Authority beats recency
- Hard constraints override, soft constraints blend
- Partial compliance is more common than refusal
- “Weird” outputs are diagnostic signals, not bugs

You’ll see controlled experiments that surface:
- Instruction shadowing
- Fake compliance
- Over-constraint collapse
- Policy language leakage

---

### 3. Hallucination Triggers & Control

Hallucination is treated correctly as:

> A **confidence calibration failure under uncertainty**, not randomness or missing knowledge.

The notebooks distinguish between:
- **Fabrication** (inventing atomic facts)
- **Confabulation** (filling plausible schemas)

Critical insight validated:
- Hallucinations only occur when the task is **structurally plausible**
- Disclaimers reduce tone, not truthfulness
- The strongest suppression mechanism is **dependency on external evidence**, not “don’t guess”

---

### 4. Compliance vs Refusal Boundaries

This repo maps the **full compliance spectrum**:

Hard Refusal → Soft Refusal → Safe Alternative → Partial Answer → Full Answer → Over-Compliance

Key findings:
- Most failures live between soft refusal and partial compliance
- Academic framing dramatically softens boundaries
- Third-person analysis leaks more than direct intent
- Polite lying is a failure mode, not a safety feature

---

## Repository Structure

- `sampling_*.ipynb`  
  Experiments on temperature, top-p, top-k, collapse, drift, and diversity

- `instruction_*_experiments.ipynb`  
  Hierarchy conflicts, override attempts, blending, and shadowing

- `hallucination_*.ipynb`  
  Structural plausibility tests, fabrication vs confabulation

- `compliance_*_experiments.ipynb`  
  Boundary probing, soft refusals, partial compliance analysis

Each notebook is designed as:
**Hypothesis → Prompt Design → Prediction → Observation → Post-mortem**

---



There is no universal best setting.
Only **stable regions** and **predictable trade-offs**.

---


## Core Rule

> You don’t control models by overpowering them.  
> You control them by designing within constraints you understand.

---

## Status

Ongoing experimental lab.  
Expect refactors, new notebooks, and deeper failure-mode isolation over time.
