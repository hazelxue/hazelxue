## Hi, I'm Hazel Xue

I build LLM agents and the machinery that makes them trustworthy: post-training loops, data synthesis, evaluation gates, and the sandboxing that lets an agent run code safely. MS student, open to **ML Engineer / AI Engineer internships** working on LLM agents, post-training, or evaluation.

**What I have shipped**

- **Agent post-training.** Designed and landed a bounded self-evolution loop for an SFT → DPO → GRPO ReAct tool-use agent: diagnose weak task families from eval traces, mine bad cases, synthesize targeted training data from train-only parents, freeze every round behind SHA256 manifests, and accept the new policy only if a no-regression gate passes on frozen held-out splits. Agreed with the maintainer before writing code; merged.
- **Verified generation.** Built a Claude Code skill where the model emits a typed spec instead of final output, every factual claim is an executable check against the data, and a gate blocks compilation on failure. Ran an ablation with real model calls: measuring first raised first-draft acceptance from 0% to 100% and halved cost.
- **Agent-framework reliability.** Found and fixed subprocess, sandbox and test-isolation bugs in DSPy, LiteLLM, Pydantic AI and cassetter by running their suites where their CI does not (Windows, newest dependencies), bisecting to a root cause, and shipping a regression test with each fix.

### Open source

| Project | Contribution | Status |
|---|---|---|
| [AgenticArXiv-RL](https://github.com/Algorineko/AgenticArXiv-RL) · SFT→DPO→GRPO pipeline for a ReAct tool-use agent | Designed and implemented the Roadmap-P3 bounded self-evolution loop (diagnose → mine bad cases → targeted data synthesis → SHA256-frozen round manifests → no-regression gate), aligned with the maintainer first ([#97](https://github.com/Algorineko/AgenticArXiv-RL/issues/97), [#101](https://github.com/Algorineko/AgenticArXiv-RL/pull/101)) · Made the documented SFT data pipeline runnable again on `main`: stale split default and hard-coded row counts broke it end to end ([#102](https://github.com/Algorineko/AgenticArXiv-RL/issues/102), [#103](https://github.com/Algorineko/AgenticArXiv-RL/pull/103)) · Full-precision trainers crashed on every pre-Ampere GPU: torch's `is_bf16_supported()` counts emulation, so the trainer picked bf16 on a T4 and the model loaded in bf16; fixed the precision probe and the weight dtype with tests ([#105](https://github.com/Algorineko/AgenticArXiv-RL/issues/105), [#106](https://github.com/Algorineko/AgenticArXiv-RL/pull/106)) · Restored a green `main`: a new test failed on every CPU-only host because TRL's `GRPOConfig` defaults to `bf16` ([#91](https://github.com/Algorineko/AgenticArXiv-RL/pull/91)) · CLI entrypoint unusable from the repo root, fixed with a regression test covering both invocation styles ([#96](https://github.com/Algorineko/AgenticArXiv-RL/pull/96)) | 5 merged |
| [DSPy](https://github.com/stanfordnlp/dspy) · Stanford NLP | `LocalInterpreter` on Windows: any guest subprocess hung forever and captured stdout carried stray `\r`. Bisected the hang to the worker's blocked stdin read, isolated fd 0, and replaced `taskkill`-based cleanup with a kill-on-close Job Object (shutdown 1.2 s → 15 ms) ([#10571](https://github.com/stanfordnlp/dspy/issues/10571), [#10572](https://github.com/stanfordnlp/dspy/pull/10572)) | in review |
| [LiteLLM](https://github.com/BerriAI/litellm) · BerriAI | The unit-test host-environment isolation deleted `SYSTEMROOT` on Windows, so every test that spawned a Python child failed with `WinError 10106`. Kept the Windows system variables through a dependency-free allowlist module, with an in-process regression test plus a Windows-only child-interpreter check ([#44767](https://github.com/BerriAI/litellm/pull/44767)) | in review · CI green |
| [cassetter](https://github.com/Kludex/cassetter) · HTTP record/replay for pytest | One crashed xdist worker aborted the whole session with `INTERNALERROR`, hiding every other result; fixed with a pytester regression test ([#143](https://github.com/Kludex/cassetter/issues/143), [#144](https://github.com/Kludex/cassetter/pull/144)) | in review |
| [Pydantic AI](https://github.com/pydantic/pydantic-ai) | Proposal: Windows support for `LocalWorkspace` via a kill-on-close Job Object, with a line-referenced analysis of the POSIX-only paths and a Windows spike verifying the Job Object teardown and `anyio` creation flags ([#9873](https://github.com/pydantic/pydantic-ai/issues/9873)) | triaged · under maintainer discussion |

### Projects

- [storymap-gen](https://github.com/hazelxue/storymap-gen) · a Claude Code skill plus Python pipeline that turns a topic and GIS data into an ArcGIS StoryMap. The model only emits a typed spec (pydantic); every claim about the data is an executable check against the layer (street-vs-grid bearing, layer statistics), and a quality gate refuses to compile a story with a failing claim. Ablation with real model calls: handing the writer measured facts before drafting raised first-draft acceptance from 0% to 100% and halved cost per story. 26 tests; all three layouts load in the live StoryMaps Builder.

### Interests

- **Agentic RL and post-training**: GRPO / DAPO, RL with verifiable rewards, SFT → preference → RL curricula, reward design for tool use.
- **Data engines**: targeted synthesis from failure analysis, parametric task derivation, leakage control between train and held-out splits.
- **Evaluation**: pass@k / pass³ on frozen splits, LLM-as-judge with blind rubrics, bad-case libraries that only grow, deterministic offline replay of tool calls.
- **Agent runtimes**: ReAct tool-use loops, code sandboxes and process isolation (Job Objects, process groups), structured outputs as the contract between model and code.
- **Reproducibility**: SHA256-frozen data manifests, recipe pinning, honest Before/After reporting, including when the gate says no.

### Stack

Python, PyTorch, TRL / PEFT, Hugging Face Transformers, pydantic, pytest; DSPy, LiteLLM, Pydantic AI from the inside.
