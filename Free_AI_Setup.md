# StellarX Philippines: Free AI Setup Guide
## Using Free and Open AI Tools for Building Faster

**Prepared for: StellarX Philippines**  
**Date: 2026**

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Best Open Models for Coding](#2-best-open-models-for-coding)
3. [How to Use a Local Model with Claude Code](#3-how-to-use-a-local-model-with-claude-code)
4. [Running Your Model on a VPS](#4-running-your-model-on-a-vps)
5. [Free Cloud AI Alternatives](#5-free-cloud-ai-alternatives)
6. [About Stella: Stellar's AI Assistant](#6-about-stella-stellars-ai-assistant)
7. [Quick Recommendations](#7-quick-recommendations)

---

## 1. Introduction

If you're building in StellarX Philippines, you do **not** need a paid AI subscription to move fast.

You have several options for AI-assisted development:

- **Paid plans**: If you already use Claude, ChatGPT, GitHub Copilot, Cursor, or another paid AI tool, you can keep using it.
- **Open-source local models**: You can run a coding model on your own machine for free, with no subscription and no code leaving your laptop.
- **GPU VPS**: If your laptop is not strong enough, you can rent a GPU server for a few dollars and run the model there.
- **Free cloud APIs**: Several providers offer strong free models or free daily usage limits.
- **Free IDE tools**: Cursor, GitHub Copilot Free, Google AI Studio, and others are enough for many hackathon builds.

This guide is built to help StellarX Philippines teams get working quickly, especially if they are:
- building wallets
- building payment or remittance flows
- integrating Stellar, Soroban, anchors, or DeFi
- trying to shorten the path from idea to demo-ready prototype

The goal is simple: remove cost and setup friction so every builder has a fair shot.

---

## 2. Best Open Models for Coding

Below are the most useful open models for coding, ranked by practical usefulness for most builders.

---

### Model 1: Qwen2.5-Coder

**What it is**  
A family of code-specialized open models trained for programming tasks across many languages.

**What it is good for**
- code generation
- debugging
- refactoring
- explanation
- fast iteration in TypeScript, JavaScript, Rust, Python, Solidity, and other developer workflows relevant to Stellar builds

**Best versions**
| Model | Best For | Notes |
|---|---|---|
| `qwen2.5-coder:1.5b` | Very weak hardware | Fast but limited |
| `qwen2.5-coder:7b` | Most builders | Best balance |
| `qwen2.5-coder:32b` | Strong machine or GPU VPS | Higher quality |

**System Requirements**
| Model Size | Minimum VRAM (GPU) | Recommended RAM (CPU-only) |
|---|---:|---:|
| 1.5B | 4 GB | 8 GB |
| 7B | 8–10 GB | 16 GB |
| 32B | 24 GB | 64 GB |

**Install with Ollama**
```bash
ollama pull qwen2.5-coder:7b
ollama run qwen2.5-coder:7b
```

---

### Model 2: Llama 3.1 / 3.3

**What it is**  
A general-purpose open model family that performs strongly on coding and reasoning tasks.

**What it is good for**
- project planning
- reasoning through architecture
- writing and debugging code
- tool-calling compatibility with Claude Code workflows

**Best versions**
| Model | Best For | Notes |
|---|---|---|
| `llama3.2:3b` | Very light setups | Fast, limited |
| `llama3.1:8b` | Everyday hackathon coding | Strong default |
| `llama3.3:70b` | GPU VPS / premium quality | Strongest option |

**System Requirements**
| Model | Minimum VRAM | CPU-only RAM |
|---|---:|---:|
| 3B | 4 GB | 8 GB |
| 8B | 10 GB | 16 GB |
| 70B | 48 GB | 128 GB |

**Install with Ollama**
```bash
ollama pull llama3.1:8b
ollama run llama3.1:8b
```

---

### Model 3: Phi-4

**What it is**  
A smaller model that performs surprisingly well for coding and reasoning given its size.

**What it is good for**
- low-end hardware
- fast responses
- lightweight coding assistance
- situations where bigger models are too slow

**System Requirements**
| Configuration | Requirement |
|---|---:|
| Minimum VRAM | 8 GB |
| Recommended VRAM | 12–16 GB |
| CPU-only RAM | 16 GB |

**Install with Ollama**
```bash
ollama pull phi4
ollama run phi4
```

---

### Model 4: DeepSeek-Coder-V2-Lite

**What it is**  
A stronger coding-focused option if you have a more capable machine or GPU server.

**What it is good for**
- algorithms
- complex coding tasks
- deeper multi-file understanding

**System Requirements**
| Model | Minimum VRAM | Notes |
|---|---:|---|
| Lite | 16–24 GB | Strong local/VPS option |

**Install with Ollama**
```bash
ollama pull deepseek-coder-v2
ollama run deepseek-coder-v2
```

---

### Model 5: Codestral

**What it is**  
A code-focused model from Mistral, useful for generation and inline-style coding workflows.

**What it is good for**
- code completion
- generating mid-function code
- coding-heavy sessions with larger context

**System Requirements**
| Configuration | Requirement |
|---|---:|
| Recommended VRAM (quantized) | 16–24 GB |
| CPU-only RAM | 32–64 GB |

**Install with Ollama**
```bash
ollama pull codestral
ollama run codestral
```

---

### Model 6: StarCoder2

**What it is**  
An open coding model family useful for broad language support and more open-source-oriented workflows.

**What it is good for**
- code generation
- explanation
- broad language support
- builders who want an open-source friendly option

**Best versions**
| Model | Best For |
|---|---|
| `starcoder2:3b` | Very light setups |
| `starcoder2:7b` | Mid-range use |
| `starcoder2:15b` | Stronger local/VPS setups |

**Install with Ollama**
```bash
ollama pull starcoder2:7b
ollama run starcoder2:7b
```

---

### Quick Comparison

| Model | Best For | Minimum VRAM |
|---|---|---:|
| Qwen2.5-Coder-7B | Best all-round coding model | 8 GB |
| Llama 3.1 8B | Best Claude Code compatibility | 10 GB |
| Phi-4 | Lower-end hardware | 8 GB |
| DeepSeek-Coder-V2-Lite | Stronger coding quality | 16 GB |
| Codestral | Long-context coding | 16 GB |
| StarCoder2-7B | Broad open-source option | 14 GB |

---

## 3. How to Use a Local Model with Claude Code

Claude Code can be pointed to a locally running open model instead of a paid cloud model.

The easiest way to do this is with **Ollama**.

---

### Step 1: Install Ollama

**macOS**
```bash
brew install ollama
```

Or download from: https://ollama.com/download

**Linux**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows**  
Download from: https://ollama.com/download/windows

---

### Step 2: Start the Ollama Server

```bash
ollama serve
```

This starts the local model server on port `11434`.

---

### Step 3: Pull a Model

Recommended starting options:

```bash
# Strong default for most builders
ollama pull qwen2.5-coder:7b

# Strong default for Claude Code tool-calling compatibility
ollama pull llama3.1:8b

# Lightweight fallback
ollama pull phi4
```

Check installed models:
```bash
ollama list
```

---

### Step 4: Install Claude Code

If Claude Code is not already installed:

```bash
npm install -g @anthropic-ai/claude-code
```

---

### Step 5: Point Claude Code to Ollama

**macOS / Linux**
```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
```

**Windows (Command Prompt)**
```cmd
set ANTHROPIC_BASE_URL=http://localhost:11434
set ANTHROPIC_AUTH_TOKEN=ollama
set ANTHROPIC_API_KEY=
```

**Windows (PowerShell)**
```powershell
$env:ANTHROPIC_BASE_URL = "http://localhost:11434"
$env:ANTHROPIC_AUTH_TOKEN = "ollama"
$env:ANTHROPIC_API_KEY = ""
```

---

### Step 6: Launch Claude Code with Your Local Model

```bash
claude --model qwen2.5-coder:7b
```

Or:

```bash
claude --model llama3.1:8b
```

---

### Step 7: Increase the Context Window

For better multi-file reasoning, give the model more context.

```bash
OLLAMA_NUM_CTX=64000 ollama run qwen2.5-coder:7b
```

Or create a custom model:

```bash
cat > Modelfile << 'EOF'
FROM qwen2.5-coder:7b
PARAMETER num_ctx 65536
EOF

ollama create my-coder -f Modelfile
claude --model my-coder
```

---

### Step 8: Make It Permanent (Optional)

Add the Ollama config to your shell profile.

**macOS / Linux**
Add to `~/.zshrc` or `~/.bashrc`:

```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
```

Then reload:

```bash
source ~/.zshrc
```

---

### Tips for Best Results

- Start with a **7B or 8B** model unless you know you need something larger.
- If tool calling behaves strangely, try **Llama 3.1 8B**.
- Quantized models are usually good enough for hackathon work and use much less memory.
- Close heavy apps when running local models on limited hardware.
- Use local models when you care about privacy or do not want your code sent to a cloud provider.

---

## 4. Running Your Model on a VPS

If your laptop is too weak, you can rent a GPU VPS for a few dollars.

This is often the best option for:
- bigger models
- faster inference
- multi-file work on large codebases
- teams sharing a single AI setup

---

### Recommended Providers

| Provider | Starting Price | Best For | URL |
|---|---:|---|---|
| RunPod | ~$0.20/hr | Best overall value | https://runpod.io |
| Vast.ai | ~$0.15/hr | Cheapest option | https://vast.ai |
| Lambda Labs | ~$1.10/hr | More premium / stable | https://lambdalabs.com |
| Paperspace | ~$0.45/hr | Simple setup | https://paperspace.com |

---

### Step-by-Step: RunPod Example

#### Step 1: Create an account
Sign up at https://runpod.io and add a payment method.

#### Step 2: Deploy a pod
Choose a GPU:
- **RTX 4090 / 3090** for most coding models
- **A100** only if you need very large models

Use a template such as:
- PyTorch image
- or anything suitable for a basic Linux environment

Set disk storage to at least **50 GB**.

#### Step 3: Connect over SSH
Run the provided SSH command from your local machine.

#### Step 4: Install Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama serve &
```

#### Step 5: Pull a model
```bash
ollama pull qwen2.5-coder:7b
```

#### Step 6: Forward port 11434 to your local machine
On your **local** machine:

```bash
ssh -L 11434:localhost:11434 root@<your-pod-ip> -p <port>
```

Now your local Claude Code setup can talk to the VPS-hosted model as if it were local.

#### Step 7: Launch Claude Code
```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
claude --model qwen2.5-coder:7b
```

#### Step 8: Stop the pod when done
Always stop or terminate the pod when not using it.

---

### GPU Guide

| GPU | VRAM | Models it can run | Approx. Cost |
|---|---:|---|---:|
| RTX 3060 / 4060 | 12 GB | Up to 7B | ~$0.10–0.20/hr |
| RTX 3090 / 4090 | 24 GB | Up to 32B (quantized) | ~$0.20–0.50/hr |
| A100 40 GB | 40 GB | Larger quantized models | ~$1.00–1.50/hr |
| A100 80 GB | 80 GB | Very large models | ~$1.50–2.50/hr |

---

## 5. Free Cloud AI Alternatives

If you do not want to run local models or rent a VPS, there are several strong free cloud options.

---

### 5a. Best Free Cloud Option: OpenRouter Free Models

A very strong default setup is using free models through OpenRouter.

This is often the easiest zero-setup option for builders who want:
- strong reasoning
- coding quality
- large context windows
- no local install hassle

General pattern:

```bash
export ANTHROPIC_BASE_URL="https://openrouter.ai/api/v1"
export ANTHROPIC_API_KEY="your-openrouter-key"
claude --model <model-id>
```

Examples of useful free models may change over time, so always check OpenRouter’s current free model list.

Best use case:
- fastest setup
- no GPU required
- strong enough for most hackathon work

> Privacy note: free cloud providers may log prompts and completions. Do not use them for sensitive or proprietary code.

---

### 5b. Other Free Cloud APIs

Useful providers include:
- **Groq**
- **Google AI Studio**
- **Mistral**
- **Cerebras**
- **GitHub Models**

These are useful if you want:
- fast free inference
- low-friction setup
- quick coding assistance
- a backup when local models are too slow

---

### Example: Groq

```bash
export ANTHROPIC_BASE_URL="https://api.groq.com/openai/v1"
export ANTHROPIC_API_KEY="your-groq-key"
claude --model llama-3.3-70b-versatile
```

---

### Example: Google AI Studio

```bash
export ANTHROPIC_BASE_URL="https://generativelanguage.googleapis.com/v1beta/openai/"
export ANTHROPIC_API_KEY="your-gemini-key"
claude --model gemini-2.0-flash
```

---

### Example: Mistral

```bash
export ANTHROPIC_BASE_URL="https://api.mistral.ai/v1"
export ANTHROPIC_API_KEY="your-mistral-key"
claude --model codestral-latest
```

---

### 5c. Free Trial Credits

Some providers offer signup credits that are enough for a hackathon weekend.

Examples include:
- SambaNova
- Scaleway
- Nebius
- Hyperbolic
- Fireworks

These are useful if:
- you want a better model than a small local model
- you want minimal setup
- you can tolerate limited credits

---

### 5d. Free IDE Tools

#### Cursor
Useful if you want an IDE with AI built in.

Free tier usually gives enough:
- completions
- light chat usage
- quick prototyping help

#### GitHub Copilot Free
Useful if you want:
- inline completions
- lightweight assistance inside VS Code

#### Google AI Studio
Useful for:
- long-context prompts
- explanation-heavy sessions
- planning or debugging with lots of pasted code

---

## 6. About Stella: Stellar's AI Assistant

**Stella** is Stellar’s official AI assistant for developer questions.

Use Stella when your question is specifically about:
- Stellar
- Soroban
- accounts
- assets
- transactions
- SDKs
- network behavior
- ecosystem documentation

### Where to find Stella
- On the Stellar developer docs site: https://developers.stellar.org
- Look for the chat icon
- Also use the `#stella-help` channel in the Stellar developer Discord if available

### What Stella is good for
- Stellar-specific documentation questions
- Soroban contract questions
- SDK usage questions
- asset and transaction basics
- understanding network concepts

### Best practice
Use **Stella** for Stellar-specific questions.  
Use **Claude / Qwen / Llama / Cursor / Gemini** for broader programming, debugging, architecture, and coding tasks.

---

## 7. Quick Recommendations

| Situation | Recommended Tool |
|---|---|
| Best simple free setup | OpenRouter free models |
| Best Stellar-specific help | Stella |
| Best local coding setup | Qwen2.5-Coder 7B via Ollama |
| Best Claude Code compatibility | Llama 3.1 8B via Ollama |
| Low-end laptop | Phi-4 |
| Strong local / VPS coding quality | DeepSeek-Coder-V2-Lite |
| Fastest no-setup fallback | Cursor free tier or Google AI Studio |
| Bigger model without local hardware | RunPod or Vast.ai |

---

## Final Note

This guide exists to help StellarX Philippines builders move faster with less friction.

You do not need perfect hardware or paid subscriptions to build something strong. The best setup is the one that gets you from:
- idea
- to prototype
- to working demo

as fast as possible.

Use the cheapest setup that is good enough, and spend the rest of your energy shipping.
