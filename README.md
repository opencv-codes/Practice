# Day 1 Per-Exercise Notebooks: Clinical Reporting Workflows

This directory contains standalone, self-contained Jupyter notebooks designed for **Program 5 · Day 1: Advanced Agentic Workflows** at Khalifa University.

Each notebook is fully self-contained with complete background context, step-by-step guidance, embedded high-resolution architectural infographics (`images/`), dataflow schemas, and reflection checkpoints. Participants can run and complete all exercises independently using local Ollama without external dependencies.

---

## 📚 Curriculum & Architecture Overview

| Notebook File | Companion Python Script | Core Orchestration Paradigm | Key Architectural Features | Estimated Time |
|---|---|---|---|---|
| **[`exercise1_plain_python.ipynb`](./exercise1_plain_python.ipynb)** | `patient_report.py` | Explicit procedural functions & validated JSON | Three explicit roles (Extractor, Writer, Reviewer), cross-pipeline JSON schema validation table, deliberate error injection | 40 min |
| **[`exercise2_crewai.ipynb`](./exercise2_crewai.ipynb)** | `patient_crewai.py` | Declarative role-based agents & Task DAG | `Agent(role, goal, backstory)`, `allow_delegation=False`, DAG chaining with `context=[...]`, dual authority review, execution lifecycle matrix | 40 min |
| **[`exercise3_autogen.ipynb`](./exercise3_autogen.ipynb)** | `patient_autogen.py` | Conversational agents & async message passing | `AssistantAgent` paired with shared `OllamaChatCompletionClient`, explicit coroutine handoffs, session cleanup in `finally`, 9-dimension Tri-Framework Comparison Matrix | 40 min |
| **[`exercise4_revision.ipynb`](./exercise4_revision.ipynb)** | `patient_revision.py` | Bounded reflection loop & self-correction | Code-level stopping rule (`Has Revised?` guard), mandatory recheck review, infinite-loop prevention, JSON audit logs | 30 min |
| **[`exercise5_manager.ipynb`](./exercise5_manager.ipynb)** | `patient_manager.py` | Dynamic LLM manager, state machine & tool safety | 7-stage dynamic cycle (`Manager LLM -> State Inspection -> Allowed Actions Filter -> Dispatcher -> Tool Execution -> State Update -> Invalidation rules`), step budget countdown matrix (`MAX_STEPS = 10`), comprehensive 5-architecture synthesis table | 45–60 min |

---

## 🚀 Environment Setup

### 1. Start Ollama and Download the Model
Ensure Ollama is active on your machine:
```bash
ollama serve
```

Verify or pull the workshop models:
```bash
# Recommended models:
ollama pull qwen3.5:4b
ollama pull qwen3:4b-instruct
ollama pull qwen2.5:7b
ollama pull qwen2.5:3b
```

> **Smart Model Detection:** Each notebook automatically probes your local Ollama server during the preflight check. It detects installed models and seamlessly auto-configures without crashing.

### 2. Python Packages
Install the required libraries for the exercises:
```bash
# Core Ollama client (Exercises 1, 4, 5)
pip install ollama

# CrewAI framework (Exercise 2)
pip install "crewai[litellm]"

# Microsoft AutoGen framework (Exercise 3)
pip install autogen-agentchat "autogen-ext[ollama]"
```

---

## 🔬 Visual & Architectural Highlights in Each Notebook

Each notebook incorporates high-resolution architectural infographics (`images/`) and structured matrices to replace text-heavy reading with at-a-glance comprehension:

1. **Exercise 1 (Plain Python):**
   - **Architectural Infographic (`images/exercise1_pipeline_flow.jpg`):** Clean 3-stage pipeline showing Extractor -> Structured Facts (JSON) -> Writer -> Candidate Draft -> Reviewer -> PASS / REVISE decision.
   - **Cross-Pipeline Data Contract Comparison:** Side-by-side comparative table detailing inputs, schema keys, output format, missing value policies, and validation rules across all three roles.

2. **Exercise 2 (CrewAI):**
   - **Architectural Infographic (`images/exercise2_crewai_flow.jpg`):** Two-tier declarative architecture showing specialized Agents (`allow_delegation=False`) wired to Tasks via `context=[...]` and ground-truth source note injection.
   - **Agent Configuration Matrix:** Compares roles, goals, and backstories for Extractor, Writer, and Reviewer.
   - **Task Lifecycle Matrix:** Traces input sources, context forwarding, produced artifacts, and termination rules across all 4 execution phases.

3. **Exercise 3 (AutoGen):**
   - **Architectural Infographic (`images/exercise3_autogen_flow.jpg`):** Asynchronous message passing flow connecting three `AssistantAgent`s to a shared `OllamaChatCompletionClient` within a safe `try...finally` teardown lifecycle.
   - **Tri-Framework Comparison Matrix:** 9-dimension comparative analysis across Plain Python, CrewAI, and AutoGen.

4. **Exercise 4 (Bounded Revision Loop):**
   - **Architectural Infographic (`images/exercise4_revision_flow.jpg`):** Complete state machine flowchart showing the code-enforced stopping guard: `revisions == 0` triggers revision; `revisions >= 1` triggers a hard stop escalation to instructor.
   - **Stopping Rule Decision Tree:** Visualizes how hardcoded Python logic guarantees termination in at most 1 revision, preventing runaway token expenditure.

5. **Exercise 5 (LLM Manager):**
   - **Architectural Infographic (`images/exercise5_manager_flow.jpg`):** Dynamic multi-agent state machine featuring the Manager LLM planner, the `allowed_actions(state)` safety gatekeeper, step budget countdown (`MAX_STEPS = 10`), locked `save_report` tool, and stale review invalidation rules.
   - **State Machine Transition Rules & Prerequisite Matrix:** Complete matrix defining allowed vs. blocked actions for every state condition.
   - **Comprehensive 5-Architecture Synthesis Matrix:** 8-dimension comparative synthesis of all five workshop architectures.
