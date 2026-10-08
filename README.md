# DistilGPT-2 Calculator Agent with STAIR-Inspired Memory Routing
 
## Project Overview
 
This project is the Fall 2026 evolution of the DNU Lab's tool-calling calculator agent. The framework started from a foundational transformer architecture adapted from Professor JMac's COMP 364 course and was first built as a custom nanoGPT model in Spring 2026. This iteration scales that work by fine-tuning a **DistilGPT-2** model to support a hierarchical memory retrieval system inspired by IBM's STAIR methodology.
 
The agent routes dynamically between two behaviors:
 
1. **Generating** a new mathematical tool call.
2. **Retrieving** a previously cached calculation from a Table of Contents (ToC) structure.
## Key Features & Technical Achievements
 
- **End-to-end pipeline:** a custom synthetic dataset generator (`generate.py`) produced 16,000 training examples (10,000 tool-call and 6,000 retrieval), covering four arithmetic operations (`+`, `-`, `*`, `/`) with 1-4 digit operands.
- **STAIR-inspired memory routing:** ToC leaf IDs let the model retrieve cached calculations. It reached 100% accuracy on ToC leaf selection across varied memory layouts and 94% on held-out retrieval wording.
- **AST-parsing backend:** a restricted Abstract Syntax Tree (AST) Python wrapper (`calculator.py`) serves as the backend for safe, reliable expression evaluation.
- **Evaluation benchmarks:** the model reached a 73.8% overall exact-match rate for tool results, and the operand-copy and multi-digit truncation errors that limited earlier architectures were resolved.
## Evaluation Results
 
Latest completed evaluation: `evaluation_results_20261002T035141Z.json`, after 1,500 optimizer steps on 16,000 examples (10,000 tool + 6,000 retrieval).
 
| Metric | Result |
|---|---|
| Overall tool result exact match | 73.8% |
| Overall `+` | 71.2% |
| Overall `-` | 68.8% |
| Overall `*` | 77.5% |
| Overall `/` | 77.5% |
| ToC leaf, varied memory layouts | 100% |
| ToC leaf, held-out retrieval wording | 94% |
 
**Observations:**
 
- Familiar training phrasing performs strongly, often 85-100% per operation and digit band.
- Held-out paraphrases (`evaluate_retrieval.py`) remain the main weakness, at roughly 35-65% on several `-`, `*`, `/`, and some `+` cells. This is expected for a small DistilGPT-2 fine-tune on synthetic templates, and the evaluation separates familiar from held-out wording on purpose.
## Context within Broader Research
 
This is the **v2** architecture of the lab's calculator agent. Moving from the COMP 364 baseline and the Spring 2026 custom nanoGPT model (v1) to a fine-tuned DistilGPT-2 gave the parameter scale and stability needed for complex memory routing.
 
**Future work:**
 
- Expanding the scope of calculator operations.
- Moving toward full STAIR-inspired document retrieval, with persistent hierarchical memory and multi-hop retrieval.
## Tech Stack
 
- Python (AST for safe evaluation, dataset generation scripts)
- DistilGPT-2 architecture (scaled from the COMP 364 baseline and the custom nanoGPT model)
## Authors
 
- Rayyan Faiz Madraswala ([@R1Kexpress](https://github.com/R1Kexpress))
 
