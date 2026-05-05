# Claude Code Guide

A practical reference for using Claude Code effectively during **StellarX Philippines**: core workflows, plan mode, parallel agents, useful commands, Stellar-specific plugins, browser automation, and testing patterns that help teams ship faster.

---

## 1. Core Workflow Concepts

### Plan Mode

Activate plan mode with `/plan` or `Shift+Tab`.

In plan mode, Claude thinks through the problem before taking action. No code is written and no files are changed. Use it for anything bigger than a tiny one-line edit, especially:
- new features
- refactors
- multi-file changes
- architecture decisions
- integration planning

Claude will return a numbered plan that you can review and refine before execution. This is one of the best ways to avoid wasting time during StellarX, especially when you are building wallets, payment flows, remittance tools, or multi-step integrations on Stellar.

---

### Parallel Agents

Claude Code can spawn multiple subagents to work on independent tasks simultaneously.

A strong default build flow for StellarX is:

```text
[Plan mode] → [Scaffold agent] → [3 parallel agents] → [Integration agent] → [Browser smoke test]
```

Once your scaffold is ready, use parallel agents for clearly separable workstreams.

#### Recommended parallel prompt

```text
The scaffold is in place. Divide the remaining work into three independent tracks:

Track 1: Core logic and tests
- [list the pure logic modules]
- Write Vitest unit tests for each module as you go

Track 2: State management and routing
- [list the stores, state singletons, and routing logic]

Track 3: UI components
- [list the pages and components]
- Use the stores from Track 2; do not duplicate state

Spawn one agent per track and run them in parallel.
Once all three complete, spawn a fourth agent to wire everything together and run the full test suite.
```

#### Use parallel agents when
- tasks do not share files
- tasks do not have strict ordering dependencies
- you want research and implementation happening at the same time
- you want to compare multiple approaches quickly

#### Why plan mode matters first
The planning pass is what makes parallelization work. Without it, subagents often make conflicting assumptions about:
- state shape
- file structure
- naming conventions
- component boundaries

With a shared blueprint, each agent can move faster and the integration pass becomes much lighter.

---

### `CLAUDE.md`

`CLAUDE.md` is a project-level instruction file that Claude Code reads automatically at session startup. Put it at the root of your repo.

This file should contain the context you do not want to repeat every session.

#### What to include
- tech stack and versions
- project conventions
- naming and folder structure
- code style expectations
- network configuration
- project-specific gotchas
- asset assumptions
- testnet addresses
- API endpoint overrides
- product constraints Claude should always respect

For StellarX Philippines, this is especially useful when your project depends on:
- a specific wallet architecture
- a specific USDC or asset assumption
- a specific anchor or payment rail flow
- a specific Stellar protocol or Soroban integration path

Treat `CLAUDE.md` as a living document and keep updating it as the build evolves.

---

## 2. Full Command Reference

### Slash Commands

| Command | What it does |
|---|---|
| `/plan` | Enter plan mode so Claude reasons before acting |
| `/clear` | Clear conversation history and start fresh |
| `/compact` | Compress conversation to save context while keeping working memory |
| `/memory` | View and edit Claude's persistent memory |
| `/cost` | Show token usage and estimated cost |
| `/plugin` | List installed plugins |
| `/plugin marketplace add owner/repo` | Install a plugin from GitHub |
| `/plugin install path/to/plugin` | Install a plugin from a local path |
| `/model` | Switch the active model |
| `/help` | Show help |
| `/status` | Show current session status |
| `/vim` | Toggle vim keybindings |
| `/doctor` | Diagnose configuration issues |
| `/login` | Authenticate with Anthropic |
| `/logout` | Sign out |
| `/review` | Review code changes |
| `/pr` | Create a pull request |
| `/commit` | Create a git commit |
| `/test` | Run tests |
| `/bug` | Report a bug |
| `/explain` | Explain selected code |
| `/fix` | Fix a bug or error |
| `/todo` | Manage a task list |

---

### Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Shift+Tab` | Toggle plan mode |
| `Escape` | Interrupt current operation |
| `Ctrl+R` | Search command history |
| `Ctrl+C` | Cancel current operation |
| `Up / Down arrows` | Navigate command history |

---

### Useful CLI Flags

| Flag | What it does |
|---|---|
| `--print` | Non-interactive output mode |
| `--model` | Specify model at startup |
| `--max-tokens` | Set max output tokens |
| `--allowedTools` | Restrict which tools Claude can use |
| `--dangerouslySkipPermissions` | Skip confirmation prompts; use carefully |

---

### Pro Tips

- **`CLAUDE.md` is load-bearing.** The more stable project context you put there, the less time you waste re-explaining the codebase.
- Use **`/compact`** when you want to continue the same task but the conversation is getting too long.
- Use **`/clear`** when you are switching to a completely new task.
- End one task with a clear handoff like:  
  `"Now do X next using the same conventions."`  
  This helps Claude carry useful context forward.
- During StellarX, use Claude to get to a **demo-ready core flow** first. Do not try to build the full product at once.

---

## 3. Plugins and Skills

### What’s what

- **Plugin**: a package that bundles skills and optionally MCP servers
- **Skill**: a reusable prompt playbook for a specific type of work
- **MCP server**: gives Claude access to external tools and APIs such as documentation, contract generators, browsers, databases, and more

---

### Relevant Plugins for StellarX Builders

| Plugin / Skill | What it does | Install |
|---|---|---|
| `stellar-dev:stellar-dev` | Full Stellar development playbook covering Soroban contracts, RPC vs Horizon, frontend + wallet integration, classic assets, pitfalls, security, testing, and ecosystem mapping | Pre-installed in Claude Code; invoke by name |
| `openzeppelin-skills` | Skills for secure Stellar contract development and OpenZeppelin MCP support | `/plugin marketplace add OpenZeppelin/openzeppelin-skills` |

---

### How to Invoke a Skill

Type the skill name directly in chat or use the `skill-name:action` format.

Example:

```text
stellar-dev:stellar-dev
```

Then tell Claude what area you are working on so it loads the most relevant guidance.

---

### What’s in `stellar-dev`

The `stellar-dev` skill is useful for StellarX projects that need network-specific context. It contains multiple modules that can be used depending on what you are building.

| Module | Use when |
|---|---|
| `contracts-soroban` | Writing or debugging Soroban contracts in Rust |
| `api-rpc-horizon` | Working with RPC, Horizon, method references, or migration issues |
| `frontend-stellar-sdk` | Connecting wallets, building/signing/submitting transactions, passkeys, Wallets Kit |
| `stellar-assets` | Issuing assets, deriving SAC addresses, using assets in contracts, SEP patterns |
| `common-pitfalls` | Something works locally but fails on testnet, or you hit a confusing issue |
| `security` | Pre-deploy review for auth, reinitialization, overflow, TTL, storage issues |
| `testing` | Unit tests, local Quickstart, testnet setup, CI/CD |
| `ecosystem` | Discovering integration targets such as DeFi protocols, wallets, oracles, and tooling |

For StellarX Philippines, these modules are especially helpful if you are building:
- wallet-led products
- consumer payment flows
- remittance tools
- DeFi integrations
- Soroban-based smart contract apps

---

## 4. Browser Automation

There are two useful browser automation patterns depending on how you want to test.

---

### Claude in Chrome

Claude in Chrome gives Claude access to the active browser tab. Claude can:
- read page content
- click buttons
- fill forms
- inspect flows
- test your app end to end

This is useful for:
- local app testing
- live UI interaction
- smoke tests
- repetitive QA flows

Setup: install the Chrome extension and Claude will get `mcp__claude-in-chrome__*` tools automatically.

---

### Integration Testing with Claude in Chrome

This is one of the most useful but underused workflows in a builder program.

Claude can open your running app in a browser, click through user flows, and verify whether the expected product behavior actually works.

For StellarX projects, this is particularly useful for:
- onboarding flows
- wallet creation
- testnet funding
- trustline creation
- payment actions
- transaction result checks
- balance verification
- lock/unlock flows

#### Example smoke test prompt

```text
Open http://localhost:5173 in Chrome.

Run this smoke test sequence and report pass/fail for each step:

1. Create wallet
2. Fund the wallet on testnet
3. Perform the primary user flow
4. Lock and unlock the wallet if relevant
5. Verify balances and transaction results

For each step:
- describe what you saw
- describe what action you took
- say whether it passed or failed

If a step fails, include the exact error message or browser output.
```

You should adapt the steps to your own product.

For example:
- if you are building a payment app, test the payment flow
- if you are building a remittance app, test quote → send → receive states
- if you are building a wallet, test create → fund → asset/trustline → send flow

---

### Known input reactivity issue

Some frameworks rely on the `input` event for reactivity. Programmatic typing may not always trigger this correctly.

If needed, instruct Claude to dispatch a synthetic input event after filling an input:

```javascript
const input = document.querySelector('input[name="password"]');
input.value = 'your-value';
input.dispatchEvent(new Event('input', { bubbles: true }));
```

Useful instruction to Claude:

```text
After typing into any input field, dispatch a synthetic input event so framework reactivity updates correctly.
```

---

### `agent-browser` by Vercel Labs

`agent-browser` is a CLI-based headless browser built for AI agents.

Useful for:
- server-side automation
- CI-based testing
- headless scraping
- environments where you do not want a visible browser

It is a good option if you want more automated browser workflows.

- Repo: https://github.com/vercel-labs/agent-browser
- Install: `npm install -g @vercel/agent-browser`

---

## 5. Recommended Build Workflow for StellarX Philippines

If you are building during StellarX Philippines, this is a strong default pattern:

### Step 1: Scope correctly
Start in plan mode.
- define the product clearly
- identify the smallest demo-worthy version
- decide what is core vs optional

### Step 2: Scaffold the project
Ask Claude to set up:
- folder structure
- routes
- shared types
- stores
- UI shell
- test setup

### Step 3: Parallelize
Once structure is stable:
- one agent handles logic and tests
- one handles state and routing
- one handles UI

### Step 4: Integrate
Run an integration pass to:
- connect everything
- remove duplicated logic
- fix mismatched assumptions
- run tests

### Step 5: Browser smoke test
Use Claude in Chrome or another browser automation setup to verify the full product flow.

### Step 6: Tighten the demo
Have Claude help with:
- empty states
- error handling
- loading states
- user copy
- demo sequence
- pitch clarity

The goal is not to generate the most code.  
The goal is to ship the strongest working demo in the shortest time.

---

## 6. What Claude Code is Best At

Claude Code is strongest when you use it for:
- project scaffolding
- structured refactors
- test generation
- code explanation
- bug isolation
- build planning
- browser-assisted QA
- multi-step implementation with clear structure

It is much less effective when:
- the prompt is vague
- the product architecture is unclear
- you ask it to do everything at once without scoping

The more specific you are about:
- what you are building
- what the main user flow is
- what the constraints are
- what files should or should not change

the better the results will be.

---

## 7. Final Advice

Use Claude Code as a force multiplier, not as a replacement for judgment.

It works best when you:
- scope the product clearly
- define the right architecture
- use plan mode before large tasks
- keep `CLAUDE.md` updated
- parallelize only after the structure is stable
- test with real flows, not assumptions

For StellarX Philippines, always optimize for:
- a real problem
- a usable flow
- meaningful use of Stellar
- a clean demo

Shipping a smaller but working product is better than aiming too big and missing the demo.
