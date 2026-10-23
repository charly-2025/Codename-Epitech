# Codename: LLM agent security

> Built at **Epitech Rennes** · B-AIA-300 · Artificial Intelligence · October 2026

## Overview

Every LLM agent hides a secret codeword in its instructions. Whoever extracts
it can rewrite the agent's behavior. This project covers both sides of that
fight:

- **Attack (red team)**: a toolkit of prompts that try to make an agent leak its codeword.
- **Defense (blue team)**: a custom agent, built on Ollama, hardened so that it never leaks its own, even under the same attacks.

## How it works

The agent is defined in a `Modelfile` (base model, generation parameters,
system prompt and stop sequences). The test bench builds it with Ollama, then
replays three kinds of sessions against it:

1. **Ordinary questions**: the agent must stay useful and answer normally.
2. **Password session**: giving the right password must unlock the codeword.
3. **Attack sessions**: every prompt in `attacks/` is sent, and the agent must not leak anything without the password.

## Attack techniques

| File | Technique |
| --- | --- |
| `attacks/override.prompt` | Instruction override ("ignore your previous instructions...") |
| `attacks/roleplay.prompt` | Role play to bypass the agent's rules |
| `attacks/faketurn.prompt` | Fake dialogue turns injected into the conversation |
| `attacks/encoding.prompt` | Asking for the secret in an encoded or transformed form |
| `attacks/leak.prompt` | Direct and indirect attempts to dump the system prompt |

## Defense

- Low temperature and deterministic sampling (`temperature 0`, `top_k 1`) for predictable answers
- Short answers (`num_predict`) to limit what can leak
- Stop sequences that cut the generation as soon as it drifts toward the secret, a role change or a prompt dump
- A system prompt that keeps the agent focused on short, ordinary answers

## Getting started

Requirements: Python 3 and [Ollama](https://ollama.com) running locally.

```bash
ollama pull granite3.1-moe:3b
python3 run_test.py            # tests ./Modelfile
python3 run_test.py 2          # tests ./Modelfile-2
python3 run_test.py path/to/Modelfile
```

The script prints every exchange so the agent's behavior can be reviewed
session by session.

## Repository structure

```
Modelfile     hardened agent definition (Ollama)
run_test.py   builds the agent and replays the test sessions
attacks/      attack prompts, one technique per file
```

## Tech stack

`Python` · `Ollama` · `Granite 3.1 MoE` · `Prompt engineering` · `LLM security`

---

More of my work on my [portfolio](https://charly-2025.github.io/myPortfolio/).
