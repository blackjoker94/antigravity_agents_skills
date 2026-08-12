# New Flutter Project Setup — Antigravity Agent Rules

## How the System Works

| What | Where | Scope | Commit to Git? |
|---|---|---|---|
| **Project Rules** | `<project-root>/GEMINI.md` | This project only, travels with git | ✅ Yes |
| **Claude Rules** | `<project-root>/CLAUDE.md` | Claude model only, travels with git | ✅ Yes |
| **Global Skills** | `~/.gemini/config/skills/` | Every workspace on this machine | ❌ No (already installed) |

> **Skills are machine-global** — you install them once and they work in every project automatically. You never need to commit them per project.

> **Rules (`GEMINI.md` + `CLAUDE.md`) are per-project** — commit them to every Flutter project repo so they travel with the code.

---

## Steps for Every New Flutter Project

### Step 1 — Copy rule files into the project root

From this repo (`antigravity_agents_skills`), copy these 2 files into the root of your new Flutter project:

```
GEMINI.md  →  <new-project-root>/GEMINI.md
CLAUDE.md  →  <new-project-root>/CLAUDE.md
```

Or via PowerShell (replace `<project-path>` with your project path):

```powershell
Copy-Item "d:\programming\antigravity_agents_skills\GEMINI.md" "<project-path>\GEMINI.md"
Copy-Item "d:\programming\antigravity_agents_skills\CLAUDE.md" "<project-path>\CLAUDE.md"
```

### Step 2 — Commit them

```bash
git add GEMINI.md CLAUDE.md
git commit -m "chore: add Antigravity agent rules"
```

### Step 3 — Open the project in Antigravity

That's it. Both models will now automatically pick up the rules:
- Gemini reads `GEMINI.md`
- Claude reads `CLAUDE.md`
- Both models see `flutter-code-review` and `flutter-cubit` skills globally

---

## On a New Machine

If you're on a new computer, skills are **not** committed — you need to reinstall them once:

```powershell
# Create skill directories
New-Item -ItemType Directory -Path "$env:USERPROFILE\.gemini\config\skills\flutter-code-review" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.gemini\config\skills\flutter-cubit" -Force

# Copy skill files from this repo
Copy-Item "d:\programming\antigravity_agents_skills\skills\flutter-code-review\SKILL.md" "$env:USERPROFILE\.gemini\config\skills\flutter-code-review\SKILL.md"
Copy-Item "d:\programming\antigravity_agents_skills\skills\flutter-cubit\SKILL.md" "$env:USERPROFILE\.gemini\config\skills\flutter-cubit\SKILL.md"
```

---

## Updating Rules

When you update `GEMINI.md`, always keep `CLAUDE.md` in sync (same content, different file). Both files live in this repo as the source of truth.

---

## Verify It's Working

After opening a project in Antigravity, ask the agent:

> "What skills do you have available?"

You should see `flutter-code-review` and `flutter-cubit` listed. If not, the skills aren't in the global directory — re-run the "On a New Machine" steps above.
