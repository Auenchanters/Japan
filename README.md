# Japan
Two separate questions — here are the direct answers:

***

## 1. Slash Commands — How They Work in Claude Code

Slash commands like `/grill-with-docs`, `/tdd`, `/diagnose` are **not typed manually** like Discord commands. They work one of two ways:

**Via the `/` menu in Claude Code's input bar:**
Type `/` and a popup appears listing every installed skill command. Click or arrow-key to the one you want — Claude executes it automatically on the current file/context.

**Via natural language (preferred for your setup):**
You do not need to type `/` at all. Because Karpathy + Pocock rules are baked into `CLAUDE.md`, Claude reads those rules on every session start and applies the correct workflow automatically when you describe what you're doing:

```
# These trigger the same behaviour as the slash command:

"I want to add a new endpoint to routes/"
→ Claude automatically runs /grill-with-docs then /tdd internally

"There's a bug in the auth middleware"
→ Claude automatically runs /diagnose workflow

"Code is getting messy"
→ Claude automatically runs /improve-codebase-architecture
```

The slash commands are just **shortcuts that invoke the same rule**. With your `CLAUDE.md` in place, the rule fires regardless of how you phrase it.

***

## 2. What to Install Manually BEFORE Running the Setup Prompt

The setup prompt installs most things itself, but these **must exist on your machine first** or the prompt will fail immediately:

### Required — Install These First

```bash
# 1. Node.js + npm (v18+)
node --version   # if missing: https://nodejs.org

# 2. Homebrew (macOS — needed for RTK and Sentrux)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 3. Git (already on most machines — verify)
git --version

# 4. curl (already on macOS/Linux — verify)
curl --version
```

### Strongly Recommended — Install Before Running

```bash
# 5. Rust toolchain (Fallow and RTK are Rust binaries)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env

# 6. Claude Code CLI itself (must already be running)
# Install from: https://claude.ai/code
# Verify:
claude --version
```

### The Setup Prompt Handles the Rest Automatically

| Tool | Installed by |
|---|---|
| context-mode | `npm install -g` in Step 2A |
| Fallow | `npx skills@latest` in Step 2B |
| RTK | `brew install` in Step 2C |
| claude-mem | `npx claude-mem@latest init` in Step 3A |
| Hermes | `curl install.sh` in Step 4A |
| Sentrux | `brew install` in Step 4B |

### Order to Run

```
1. Install Node, Homebrew, Git, Rust, curl  ← manual
2. Open your project in Claude Code          ← manual
3. Paste the full setup prompt               ← automated from here
```

That's it. If all 5 prerequisites are present, the entire setup prompt runs without interruption.
