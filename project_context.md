# Project Context
AI Project Onboarding Initiative

Version: 1.4
Last Updated: 2026-03-25
Owner: Daniel DeLay / Velir

## Purpose
This file is the AI onboarding and continuity document for the AI Project Onboarding initiative. It is intended to give an AI enough context to understand the purpose of the work, the deliverables created so far, the design decisions that have been made, and the standards to follow when updating this solution.

Use this file when making updates to:
- the solution-onboarding bootstrap skill
- onboarding and troubleshooting guidance patterns
- the project PowerPoint deck
- related markdown templates, references, and rollout materials

## Initiative Summary
The initiative is designed to improve developer onboarding and troubleshooting for project solutions by moving guidance closer to the codebase and making AI the primary interface for setup assistance.

The current model is:

1. A bootstrap skill performs the initial setup of the repo guidance system.
2. The skill analyzes the solution and existing documentation.
3. The skill drafts standardized onboarding and troubleshooting markdown files.
4. The skill interviews the solutions architect to close knowledge gaps.
5. The skill creates or reconciles a custom Copilot agent for in-repo daily use.
6. Ongoing updates are handled through normal repo workflows, not by the bootstrap skill itself.

## Scope Boundaries
### What the skill is responsible for
- Initial bootstrap of onboarding guidance
- Scaffolding or reconciling the standard markdown file set
- Inspecting existing `copilot-instructions.md`
- Inspecting linked markdown files and using them as source material
- Drafting initial setup, troubleshooting, environment matrix, and change-log files
- Running the solutions architect interview
- Creating the onboarding agent
- Operating in either draft mode or overwrite mode

### What the skill is not responsible for
- Ongoing autonomous maintenance after bootstrap
- Silent background changes over time
- Replacing human review and approval
- Long-term continuous documentation governance

## Standard File Set
The standard file set for a target solution is:

- `.github/copilot-instructions.md`
- `.github/agents/onboarding.agent.md`
- `.github/copilot/solution-onboarding/setup.md`
- `.github/copilot/solution-onboarding/troubleshooting.md`
- `.github/copilot/solution-onboarding/environment-matrix.md`
- `.github/copilot/solution-onboarding/change-log-for-ai.md`

If shared reference markdown is created for a target repo's onboarding system, place it under `.github/copilot/solution-onboarding/references/`.

## Directory Structure Convention
```text
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

## Key Design Decisions
### 1. Repo-native guidance
Setup and troubleshooting guidance should live in the solution repository, close to the code, rather than primarily in Confluence.

### 2. AI-assisted onboarding
AI should be the primary interface for helping developers get set up and troubleshoot environment issues, using repo-local markdown as its source of truth.

### 3. Bootstrap-only skill
The skill is for initial setup only. It is not the mechanism for ongoing autonomous maintenance.

### 4. Existing `copilot-instructions.md`
If a solution already has `.github/copilot-instructions.md`, the skill should preserve and augment it rather than blindly replacing it.

### 5. Existing linked markdown files
If `copilot-instructions.md` links to existing markdown files, the skill should inspect them and use them as source material for the initial setup documentation.

### 6. Legacy markdown handling
When older setup or troubleshooting markdown files are found, the skill should ask the solutions architect whether each should be:
- preserved
- retired
- absorbed into the new standard docs

### 7. Access and secrets
Access and secrets remain inside `setup.md`. They are not split into a separate file.

### 8. Environment matrix
`environment-matrix.md` is part of the default standard file set because the expected audience includes:
- FE developers
- BE developers
- Mac users
- Windows users

### 9. Change log
`change-log-for-ai.md` is part of the default standard file set and is considered important. It should track setup-impacting changes over time.

### 10. Agent scope
There is one agent for v1. It handles:
- onboarding
- troubleshooting
- doc update drafting

### 11. Agent and commit review
The agent may review commits for likely setup-impacting changes, such as:
- environment/config file changes
- runtime version changes
- package manager changes
- Docker/devcontainer changes
- startup script changes
- service dependency changes
- new required environment variables

This should happen as part of explicit update workflows, not as background autonomous maintenance.

### 12. Templates enforced
The solution guidance files should follow enforced section templates for consistency.

### 13. Mode of operation
The skill supports:
- draft mode: propose files/changes for review
- overwrite mode: directly write/update the standard files

### 14. Standard naming
Use consistent paths and filenames across project types. Content may vary by stack, but the core structure remains the same.

### 15. Proactive information gathering
Both the bootstrap skill and the onboarding agent should read files, inspect the repo, and run commands themselves rather than asking the solutions architect or developer to do it.

## Solutions Architect Interview
The bootstrap skill runs a core 12-question interview with the solutions architect after the initial repo draft. Questions are asked one at a time, waiting for a response before proceeding. See `SKILL.md` (Step 4) for the authoritative question set and interview behavior rules.

## Expected Behavior of the Onboarding Agent
The onboarding agent should:
- on startup, automatically run validation prechecks: required tools and runtimes, required environment variables, and any scripts needing elevated permissions — report results before proceeding
- read `.github/copilot-instructions.md` first
- follow linked onboarding docs before inventing guidance
- use the environment matrix for FE/BE and Mac/Windows differences
- walk developers through setup step by step using checkpoint-style questions
- surface missing environment variables immediately, especially those needed by Docker containers or services at startup
- flag any scripts or commands that require elevated permissions at the relevant step
- use troubleshooting docs before proposing speculative fixes
- draft documentation updates when a developer identifies needed changes
- inspect relevant files and recent commits when asked to update setup docs
- update `change-log-for-ai.md` when setup-impacting changes are identified in an explicit update workflow
- never flag newer versions of prerequisites as problems unless an exact version is required
- see the Onboarding Agent Template section of `SKILL.md` for the full authoritative agent definition

## Deliverables Created So Far
- Initial skill package for solution onboarding bootstrap
- PowerPoint deck explaining the process to developers
- Project bundle containing the skill and deck
- Standardized file structure and path conventions
- Core solutions architect interview set
- Initial onboarding agent concept and template references

## Recommended Future Assets
This initiative may later include:
- `project-context-template.md` in the reusable skill library
- sample repo outputs for one or more project archetypes
- rollout guidance for project teams
- example prompts for developers and solutions architects
- example PR/update workflow for maintaining onboarding docs after bootstrap

## Working Principles for Future AI Updates
When updating this initiative:
- keep `project_context.md` up to date whenever changes are made to the skill, templates, or design decisions
- preserve previously agreed design decisions unless explicitly changed
- prefer consistency of file paths and conventions
- do not move access/secrets into a separate file unless a new decision overrides that
- treat the bootstrap skill and ongoing agent as separate concerns
- preserve and augment existing repo instruction files where possible
- ask before removing or deprecating legacy content
- keep this file updated when major decisions change

## Open Questions
- Whether the initiative should also include a reusable `project-context-template.md` inside the skill package
- Whether rollout materials should include example repo outputs for multiple CMS/framework stacks
- Whether a dedicated follow-on workflow should exist for post-bootstrap doc governance

## Change Log
### 2026-03-25
- Inlined `section-templates.md` and `onboarding-agent-template.md` directly into `SKILL.md` so the skill is fully self-contained
- Published skill to `Velir/AIResources` at `Skills/skills/solution-onboarding-bootstrap/SKILL.md`
- Removed `agents/` folder and `solution-onboarding/references/` folder from the skill repo
- Moved `project_context.md` to the repo root
- Fixed all `.github/copilot/references/` path references to `.github/copilot/solution-onboarding/references/`
- Updated directory structure convention to reflect current standard output (references/ is no longer a standard output folder)
- Updated README to reflect current repo contents

### 2026-03-19
- Updated SKILL.md description to improve trigger accuracy: clarified SA-driven bootstrap context, added explicit trigger and do-not-trigger guidance, replaced implementation details with intent-focused language

### 2026-03-19
- Changed SA interview behavior: questions are now asked one at a time, waiting for the architect's response before proceeding to the next
- Follow-up questions are now inserted inline immediately after the question that prompted them, not batched at the end
- Replaced ambiguous "setup path/paths" with "setup approach/approaches" throughout the skill
- Added working principle: keep `references/project_context.md` up to date whenever changes are made to the skill, templates, or design decisions
- Removed duplicate interview question list from this file; `SKILL.md` Step 4 is now the single authoritative source
- Added question 12 to the SA interview: identify external sources of setup documentation (e.g., Confluence, Jira)
- Added interview behavior rules: ask all 12 questions in order, track completion, do not skip any question
- Added design decision 15: both the skill and agent should proactively gather information rather than asking the user to run commands
- Added agent rule: do not flag newer versions of prerequisites as problems; newer versions are acceptable unless an exact version is required
- Strengthened env variable discovery: both the skill and agent must actively look for required env variables in Docker/devcontainer config, compose files, .env templates, and scripts, and surface missing ones immediately
- Added rule: explicitly flag scripts or commands that require elevated permissions or admin mode (e.g., PowerShell as Administrator, sudo) at the relevant setup step
- Added agent startup behavior: automatically run validation prechecks (tools, env variables, elevated permission requirements) as the first step without waiting to be asked
- Removed model: gpt-5 from agent template; model selection is left to the environment
- Renamed agents/openai.yaml to agents/copilot.yaml for LLM-agnostic naming
- Updated section-templates.md: "Recommended Setup Paths" → "Recommended Setup Approach"
- Updated SKILL.md Step 7 to reference the agent template directly instead of maintaining a parallel list
- Updated project_context.md Expected Behavior section to reflect all current agent behaviors

### 2026-03-16
- Defined the overall model: bootstrap skill for initial setup, in-repo agent for ongoing use
- Chose preserve-and-augment behavior for existing `.github/copilot-instructions.md`
- Chose to inspect linked markdown files as source material
- Chose one agent for v1 with onboarding + troubleshooting + doc update drafting
- Chose to keep access/secrets inside `setup.md`
- Chose to include `environment-matrix.md` by default
- Chose to include `change-log-for-ai.md` by default
- Chose enforced section templates
- Chose draft mode and overwrite mode
- Chose to ask the solutions architect how older markdown files should be handled
- Changed the solution file layout from `docs/ai/` to `.github/copilot/solution-onboarding/`
- Changed shared initiative references to `.github/copilot/references/`
- Decided to create `project_context.md` as an AI onboarding file for this initiative

## Maintenance Notes
When this file is updated:
- increment the version if the changes are material
- update the last updated date
- add an entry to the change log
- keep the content focused on durable context and key decisions
