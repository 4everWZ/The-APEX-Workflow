# 🏔️ The APEX Workflow 
**Autonomous, Pyramid-structured, Evidence-based eXecution**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> Transform your AI coding assistant from a passive "ticket transcriber" into an equal, rigorous, and autonomous research co-author.

## Executive Summary

**The APEX Workflow** is a system instruction framework designed for advanced AI agents (like Cursor, AutoGPT, or custom LangChain setups). It fundamentally changes how AI interacts with your codebase. 

Instead of blindly following flawed pseudocode and leaving you with idealized but non-runnable shells, APEX enforces a ruthless, continuous engineering pipeline. It marries the **McKinsey Pyramid Principle** (top-down, conclusion-first logic) with **Goal-Driven Autonomy** (script-verifiable closed-loop execution). 

**The Golden Rule:** Scientific defensibility and autonomous, runnable execution take absolute precedence over mechanical compliance to the original prompt.

---

## 🏛️ Core Philosophy: The Fusion of Two Paradigms

This framework is built on two foundational pillars:

### 1. The McKinsey Pyramid Principle (Structural Rigor)
* **Conclusion First:** The AI must define the exact verifiable success criteria before writing any code.
* **Logical Defensibility:** Every architectural tradeoff, unviable requirement, or rejected user idea is explicitly documented (`implementation_objections_and_tradeoffs.md`). 
* **High Information Density:** No vague apologies or filler text. Communication is structured, adversarial (like "Reviewer #2"), and purely evidence-based.

### 2. Goal-Driven Execution (Autonomous Loops)
* **Dual-Persona Execution:** The AI acts as both the *Master Agent* (a strict evaluator running the tests) and the *Subagent* (the tireless engineer fixing the code).
* **Verifiable Criteria:** "Implement a model" is not a goal. "Pass all 50 local PyTorch tests and output a 0-diff benchmark" is a goal.
* **No Premature Exits:** The AI is instructed not to stop at the first traceback. It must autonomously read logs, debug the local environment, and continuously retry until the verifiable criteria are met or a hard physical limit is reached.

---

## 🚀 The Pipeline

When a specification is fed into an APEX-configured AI, it strictly follows this pipeline:

1. **Goal & Criteria:** Extracts the intent and enforces absolute, script-verifiable success criteria.
2. **Critical Review:** Audits the spec for non-differentiable logic, vague metrics, or engineering costs that outweigh scientific value.
3. **Autonomous Verification Loop:** Enters the Master/Subagent loop. Writes code $\rightarrow$ runs local tests $\rightarrow$ reads tracebacks $\rightarrow$ iterates.
4. **Documented Output:** Delivers the runnable code alongside a rigid comparison table and a tradeoff record.

---

## 🎯 Ideal Use Cases

This instruction set shines in environments where "almost working" or "plausible-sounding code" is catastrophic. It is highly recommended for:

* **Deep Learning & Computer Vision Research:** Where tensor shapes, memory constraints, and complex PyTorch architectural implementations must be mathematically and computationally sound.
* **Complex Systems Engineering:** Where rigorous local testing and dependency management are required.
* **Algorithm Implementations:** Where success can be strictly defined by pass/fail benchmark scripts.

---

## 🛠️ Quick Start

1. Copy the `instruction.md` (or `PROJECT_GLOBAL_INSTRUCTIONS.md`) from this repository.
2. Paste it into your AI agent's "System Prompt", "Rules for AI", or drop it directly into your project root for context-aware IDEs like Cursor (`.cursorrules`).
3. Provide your spec to the AI and watch it critique your design, set up automated tests, and fight tracebacks until the code actually runs.

---

## 📂 Required Deliverables

By default, an APEX agent will always generate the following files upon task completion to prevent silent failures and hidden technical debt:

* `[Your Source Code]`
* `doc/feature_implementation_comparison.md`
* `doc/implementation_objections_and_tradeoffs.md`

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
