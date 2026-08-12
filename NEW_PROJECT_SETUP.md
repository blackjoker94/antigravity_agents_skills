# New Flutter Project Setup — Antigravity Agent Rules

## How the System Works

| What | Where | Scope | Commit to Git? |
|---|---|---|---|
| **Global Rules** | `~/.gemini/GEMINI.md` | Every workspace on this machine | ❌ No (machine-local) |
| **Project Rules** | `<project-root>/GEMINI.md` | This project only, travels with git | ✅ Yes |
| **Claude Rules** | `<project-root>/CLAUDE.md` | Claude model only, travels with git | ✅ Yes |
| **Global Skills** | `~/.gemini/config/skills/` | Every workspace on this machine | ❌ No (already installed) |

> **Global Rules (`~/.gemini/GEMINI.md`) are already installed on this machine.**
> All your Flutter rules apply automatically to every workspace — no copying needed!

---

## Steps for Every New Flutter Project

### Step 1 — Copy rule files into the project root

Even though the global rules already cover you, commit `GEMINI.md` + `CLAUDE.md`
to every project so the rules **travel with the code** and work for any teammate
or on any machine that clones the repo.

```powershell
# Replace <project-path> with your project's path
Copy-Item "d:\programming\antigravity_agents_skills\GEMINI.md" "<project-path>\GEMINI.md"
Copy-Item "d:\programming\antigravity_agents_skills\CLAUDE.md" "<project-path>\CLAUDE.md"
```

### Step 2 — Commit them

```bash
git add GEMINI.md CLAUDE.md
git commit -m "chore: add Antigravity agent rules"
```

### Step 3 — Open the project in Antigravity

Done. Both models automatically pick up the rules:
- **Gemini** reads `~/.gemini/GEMINI.md` (global) + `GEMINI.md` (project)
- **Claude** reads `CLAUDE.md` (project)
- Both models see `flutter-code-review` and `flutter-cubit` skills globally

---

## On a New Machine

Run these commands once to install the global rules and skills:

```powershell
# 1. Install global rules (applies to ALL workspaces automatically)
Copy-Item "d:\programming\antigravity_agents_skills\GEMINI.md" "$env:USERPROFILE\.gemini\GEMINI.md"

# 2. Install global skills
New-Item -ItemType Directory -Path "$env:USERPROFILE\.gemini\config\skills\flutter-code-review" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.gemini\config\skills\flutter-cubit" -Force
Copy-Item "d:\programming\antigravity_agents_skills\skills\flutter-code-review\SKILL.md" "$env:USERPROFILE\.gemini\config\skills\flutter-code-review\SKILL.md"
Copy-Item "d:\programming\antigravity_agents_skills\skills\flutter-cubit\SKILL.md" "$env:USERPROFILE\.gemini\config\skills\flutter-cubit\SKILL.md"
```

---

## Updating Rules

When you update `GEMINI.md` in this repo:
1. Keep `CLAUDE.md` in sync (same content, different file for Claude models).
2. Re-copy `GEMINI.md` to `~/.gemini/GEMINI.md` to update the global rule on this machine.

```powershell
Copy-Item "d:\programming\antigravity_agents_skills\GEMINI.md" "$env:USERPROFILE\.gemini\GEMINI.md" -Force
```

---

## Verify It's Working

After opening any project in Antigravity, ask the agent:

> "What skills do you have available?"

You should see `flutter-code-review` and `flutter-cubit` listed.

> "What are my state management rules?"

The agent should say: use **Cubit/Bloc**, not Riverpod/Provider/GetX.
