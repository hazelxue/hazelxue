## Hi, I'm Hazel Xue

MS student focused on LLM applications and agent systems. I contribute to open-source AI tooling by finding real bugs the way users hit them: running projects on platforms and dependency versions their CI does not cover, reducing each failure to a minimal reproduction, and sending the fix with a regression test.

### Open source

| Project | Contribution | Status |
|---|---|---|
| [AgenticArXiv-RL](https://github.com/Algorineko/AgenticArXiv-RL) · SFT→DPO→GRPO pipeline for a ReAct tool-use agent | Restored a green `main`: a new test failed on every CPU-only host because TRL's `GRPOConfig` defaults to `bf16` ([#91](https://github.com/Algorineko/AgenticArXiv-RL/pull/91)) · CLI entrypoint unusable from the repo root, fixed with a regression test covering both invocation styles ([#96](https://github.com/Algorineko/AgenticArXiv-RL/pull/96)) · Designed and implemented the Roadmap-P3 bounded self-evolution loop (diagnose → mine bad cases → targeted data synthesis → SHA256-frozen round manifests → no-regression gate), aligned with the maintainer first ([#97](https://github.com/Algorineko/AgenticArXiv-RL/issues/97), [#101](https://github.com/Algorineko/AgenticArXiv-RL/pull/101)) | 2 merged · 1 in review |
| [DSPy](https://github.com/stanfordnlp/dspy) · Stanford NLP | `LocalInterpreter` on Windows: any guest subprocess hung forever and captured stdout carried stray `\r`. Bisected the hang to the worker's blocked stdin read, isolated fd 0, and replaced `taskkill`-based cleanup with a kill-on-close Job Object (shutdown 1.2 s → 15 ms) ([#10571](https://github.com/stanfordnlp/dspy/issues/10571), [#10572](https://github.com/stanfordnlp/dspy/pull/10572)) | in review |
| [cassetter](https://github.com/Kludex/cassetter) · HTTP record/replay for pytest | One crashed xdist worker aborted the whole session with `INTERNALERROR`, hiding every other result; fixed with a pytester regression test ([#143](https://github.com/Kludex/cassetter/issues/143), [#144](https://github.com/Kludex/cassetter/pull/144)) | in review |
| [Pydantic AI](https://github.com/pydantic/pydantic-ai) | Proposal: Windows support for `LocalWorkspace` via a kill-on-close Job Object, with a line-referenced analysis of the POSIX-only paths ([#9873](https://github.com/pydantic/pydantic-ai/issues/9873)) | proposed |

### Interests

Agentic RL (GRPO/DAPO, verifiable rewards), tool-use agents, evaluation and reproducibility.
