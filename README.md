# Solution Onboarding Bootstrap

A reusable skill and agent template for bootstrapping AI-assisted onboarding and troubleshooting guidance in software solution repositories.

## What This Is

This initiative moves developer setup and troubleshooting guidance into the solution repository itself, making AI the primary interface for helping developers get up and running. Instead of hunting through Confluence or asking a colleague, a developer opens the onboarding agent and gets walked through setup step by step.

## How It Works

1. A solutions architect runs the bootstrap skill against a target solution repository.
2. The skill inspects the repo for existing guidance, drafts standardized setup and troubleshooting docs, and interviews the architect to fill in gaps.
3. The skill creates or reconciles a standard set of markdown files and generates an in-repo onboarding agent.
4. Developers then use the onboarding agent directly inside the repo for setup help, troubleshooting, and doc update drafting.

## Repo Contents

| File | Purpose |
|------|---------|
| `SKILL.md` | The bootstrap skill — run this against a target solution repo to set up its onboarding system |
| `project_context.md` | AI continuity doc — design decisions, change log, and working principles for this initiative |
| `AI_Solution_Onboarding.pptx` | Presentation deck explaining the model and how to get started |

## Standard Output

When the bootstrap skill runs against a target repo, it creates or reconciles:

```
.github/
├─ copilot-instructions.md
├─ agents/
│  └─ onboarding.agent.md
└─ copilot/
   └─ solution-onboarding/
      ├─ setup.md
      ├─ troubleshooting.md
      ├─ environment-matrix.md
      └─ change-log-for-ai.md
```

## Who This Is For

- **Solutions architects** running the bootstrap skill on a project repo
- **Developers** using the generated onboarding agent to get set up on a solution
- **Contributors** maintaining or extending this initiative
