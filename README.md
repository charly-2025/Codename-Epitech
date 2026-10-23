# Codename: LLM agent security

> Built at **Epitech Rennes** · B-AIA-300 · Artificial Intelligence · October 2026

## Overview

Two sides of LLM security. **Attack**: a set of prompts that try to make an agent reveal its secret codeword (instruction override, fake dialogue turns, role play, encoding...). **Defense**: a custom Ollama agent configured and hardened so that it never leaks its own, plus an automated test bench.

## Features

- `attacks/`: attack prompts (override, roleplay, faketurn, encoding, leak)
- `Modelfile`: hardened Ollama agent (system prompt, parameters, stop sequences)
- `run_test.py`: builds the agent and replays sessions of normal questions and attacks

## Tech stack

`Python` · `Ollama` · `LLM` · `Prompt engineering`

---

More of my work on my [portfolio](https://charly-2025.github.io/myPortfolio/).
