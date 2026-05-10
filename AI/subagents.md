# Subagents in Claude Code — Course Notes

## 1. What Are Subagents?

Specialized helpers that handle focused tasks separately from your main session.

**Three benefits:**
- **Focused work** — each subagent handles one specific task
- **Clean main context** — intermediate work stays isolated
- **Concise summaries** — only the result comes back

> Less noise in main context = longer, more effective sessions.

---

## 2. Creating a Subagent

Use `/agents` → **Create new agent**.

**Scope:** Project-level (current project) or User-level (all projects).

**Creation method:** Manual, or let Claude generate it from your description (recommended).

**Tools to choose from:** Read-only, Edit, Execution, MCP, Other. Only enable what's needed (e.g., a code reviewer needs read + execution, not edit).

**Model options:**
- `haiku` — fast, lightweight
- `sonnet` — balanced
- `opus` — complex analysis
- `inherit` — matches main conversation

**Color** — UI marker to identify which subagent is active.

---

## 3. The Config File

Saved at `.claude/agents/<name>.md`.

```markdown
---
name: code-quality-reviewer
description: Use this agent when you need to review recently written or modified code for quality, security, and best practice compliance.
tools: Bash, Glob, Grep, Read, WebFetch, WebSearch
model: sonnet
color: purple
---

You are an expert code reviewer specializing in quality assurance...
```

**Frontmatter fields:**
- `name` — unique ID; reference with `@agent <name>`
- `description` — controls **when** Claude uses it (single line; use `\n` for breaks; can include example conversations)
- `tools` — comma-separated tool list
- `model` — `sonnet` / `opus` / `haiku` / `inherit`
- `color` — UI color

**Body** = the **system prompt** (instructions, focus, output format).

---

## 4. Triggering & Testing

- Add **"proactively"** in `description` → Claude auto-delegates without being asked.
- Include concrete example conversations for sharper triggering.
- If a subagent isn't being used when expected, fix the description with more specific examples.

---

## 5. Designing Effective Subagents — 4 Principles

1. **Specific descriptions** — steers both *when* it launches and *how* it behaves.
2. **Structured output** — defined format so it knows when it's done and returns usable info.
3. **Obstacle reporting** — dedicated section for quirks, workarounds, and problems so the main thread doesn't rediscover them.
4. **Limited tool access** — read-only for research, bash for reviewers, edit/write only for agents that should change code.

---

## 6. When to Use Subagents

**Decision rule:** *Does the intermediate work matter to the main thread?*
- **No** → delegate to a subagent.
- **Yes** → keep it in the main thread.

### ✅ Good Fits
| Use Case | Why |
|----------|-----|
| **Research** | Subagent reads many files; main thread gets a clean summary like *"JWT validation in `middleware/auth.js:42`"*. |
| **Code reviews** | Claude reviews better when code looks like someone else's work. Reviewer sees changes in fresh context (`git diff` + files) with consistent standards. |
| **Custom system prompts** | E.g., a **copywriter** with tone/style rules (default Claude Code prompt skews technical), or a **styling** agent pointed at design system files. |

### ❌ Anti-Patterns
1. **Expert claims** — "You are a Python expert" adds nothing; Claude already knows it.
2. **Sequential pipelines** — Reproduce → debug → fix fails when steps depend on each other; info is lost in handoffs.
3. **Test runners** — Hides full output you need for debugging. *Performed worst in testing.*

---

## 7. Sample Subagent

A research subagent that demonstrates all four design principles:

### `.claude/agents/codebase-researcher.md`

```markdown
---
name: codebase-researcher
description: Proactively use when the user asks how something works in the codebase, where a feature lives, or how data flows. Examples — "How does auth work?", "Where is the rate limiter?". Returns a focused summary, not a search log.
tools: Read, Glob, Grep, Bash
model: sonnet
color: blue
---

You are a codebase research specialist. Investigate how the code works and
return a focused summary — not a transcript of your exploration.

## Process
1. Use Glob/Grep to locate relevant files.
2. Read the most relevant ones; skim adjacent files.
3. Trace calls and imports to understand data flow.
4. Stop once you can answer confidently — do not over-explore.

## Required Output Format

### Summary
2–4 sentences answering the question in plain language.

### Key Locations
Bullets formatted as `path/to/file.ext:line — what happens here`.

### Data Flow (if applicable)
Short numbered list of how data/control moves through the system.

### Obstacles & Quirks
Anything surprising: inconsistent patterns, dead code, missing tests,
unexpected dependencies. Write "None observed." if there are none.

## Rules
- Read-only — never modify files.
- No step-by-step search log.
- Don't speculate; flag unclear areas under Obstacles.
- Keep response under ~400 words unless depth was requested.
```

**Why it works:**
- Specific trigger examples + "proactively" in description
- Fixed output sections so the main thread knows what it'll get
- Dedicated Obstacles section forces surfacing quirks
- Read-only tools — research should never modify code

---

## Cheat Sheet

- **Create:** `/agents` → Create new agent
- **Location:** `.claude/agents/<name>.md`
- **Auto-trigger:** put **"proactively"** in `description`
- **Manual call:** `@agent <name>`
- **Decision rule:** *Does intermediate work matter?* No → subagent. Yes → main thread.
- **Four design principles:** specific description, structured output, obstacle reporting, limited tool access.
