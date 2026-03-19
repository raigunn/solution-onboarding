---
name: solution-onboarding-bootstrap
description: bootstrap repo-native onboarding and troubleshooting guidance for a software solution. use when creating the initial ai-assisted setup system for an existing or new repository. the skill inspects the repo for existing .github/copilot-instructions.md, linked markdown guidance, and informal setup docs — updating them if present, creating them if not — and reconciles everything into a standard structure. this skill creates or reconciles standard setup files, interviews the solutions architect with a focused core question set, and generates an onboarding copilot agent.
---

# Solution Onboarding Bootstrap

Create the initial, standardized onboarding guidance system for a repository. Treat this as a one-time bootstrap workflow, not an ongoing maintenance workflow.

## Workflow overview

Complete the work in this order:

1. Discover existing repo guidance and setup signals.
2. Reconcile the standard file set.
3. Draft the initial docs from the repository.
4. Run the core solutions architect interview to close gaps.
5. Decide how to handle older markdown files.
6. Finalize the standard docs in draft or overwrite mode.
7. Generate the onboarding copilot agent.

## Operating rules

- Be proactive in gathering information. Read files, inspect the repo, and run commands directly rather than asking the solutions architect to do it.
- Default to preserving useful existing guidance.
- Never blindly overwrite an existing `.github/copilot-instructions.md`.
- If `.github/copilot-instructions.md` exists, preserve and augment it.
- If it links to other markdown files, inspect those files and use them as source material.
- Normalize useful content into the standard structure.
- Ask the solutions architect whether older markdown files should be preserved, retired, or absorbed.
- Keep access and secrets guidance inside `.github/copilot/solution-onboarding/setup.md`.
- Always include `.github/copilot/solution-onboarding/environment-matrix.md` and `.github/copilot/solution-onboarding/change-log-for-ai.md`.
- Use one onboarding agent that covers onboarding, troubleshooting, and doc update drafting.
- Enforce the section templates from `references/section-templates.md`.
- Support two execution modes:
  - **draft mode**: propose file contents or diffs for review.
  - **overwrite mode**: write or rewrite the standard files directly.
- Treat the change log as a required artifact.
- The onboarding agent may review recent commits for setup-impacting changes when explicitly asked to update docs, but this skill itself is for initial bootstrap only.

## Standard file set

Always create or reconcile these files:

- `.github/copilot-instructions.md`
- `.github/agents/onboarding.agent.md`
- `.github/copilot/solution-onboarding/setup.md`
- `.github/copilot/solution-onboarding/troubleshooting.md`
- `.github/copilot/solution-onboarding/environment-matrix.md`
- `.github/copilot/solution-onboarding/change-log-for-ai.md`

Use these exact paths unless the user explicitly requests a different convention. If shared reference markdown is created or reconciled for this onboarding system, place it under `.github/copilot/references/`.

## Step 1: discover existing guidance and repo signals

Inspect the repository before asking the solutions architect to write anything from scratch.

Look for:

- existing `.github/copilot-instructions.md`
- markdown files linked from it
- setup or troubleshooting content in `README.md`, `docs/`, `.github/`, `CONTRIBUTING.md`, scripts, devcontainer files, docker files, compose files, lockfiles, runtime version files, CI files, and local env templates
- environment variable files and templates (`.env`, `.env.example`, `.env.local`, `docker-compose.yml`, devcontainer `remoteEnv`, CI env blocks, and any scripts that reference `$ENV_VAR` or `process.env`)
- required environment variables, especially those needed by containers or services at startup (e.g., volume mounts, license paths, service URLs, feature flags)
- FE vs BE setup differences
- Mac vs Windows differences
- runtime, package manager, and service dependencies
- validation or smoke-test clues
- scripts or commands that require elevated permissions or admin mode (e.g., PowerShell scripts that must be run as Administrator, commands requiring sudo, or installers that require elevated privileges)
- likely setup blockers and stale guidance

When you find existing markdown guidance, classify it as:

- useful and current
- useful but informal
- stale or conflicting
- unknown and needs architect review

## Step 2: reconcile the standard file set

Create the standard file set if it does not exist.

If files already exist:

- preserve useful repo-specific content
- rewrite into the standard template only where helpful
- avoid duplication across files
- keep one clear source of truth per topic
- place solution-onboarding markdown under `.github/copilot/solution-onboarding/`
- place shared reference markdown under `.github/copilot/references/`

### Existing `copilot-instructions.md`

If `.github/copilot-instructions.md` already exists:

- preserve and augment it
- keep useful repo-specific instructions
- add or update links to the standard docs
- remove duplication only when the replacement location is clear
- do not fully rewrite unless the user explicitly asks

## Step 3: draft from the repository

Draft the first pass from the codebase and existing markdown before asking interview questions.

Infer and draft, where possible:

- recommended setup approaches already implied by the repo
- FE vs BE differences
- Mac vs Windows differences
- prerequisites and runtime versions
- required environment variables, including those used by Docker containers, devcontainers, or services at startup — inspect `.env` files, compose files, devcontainer config, and scripts for any variable that must be set before the solution will run
- local service dependencies
- setup steps and validation checks
- scripts or commands that require elevated permissions or admin mode — note these explicitly in setup docs
- common setup failure points suggested by config or scripts
- environment matrix rows
- seed entries for the change log if recent setup-impacting changes are already obvious

Do not invent:

- secret values
- credential locations that are not known
- internal access procedures that are not grounded
- unsupported setup approaches

Flag uncertain sections clearly for architect confirmation.

## Step 4: run the core solutions architect interview

Use the core interview after the first draft exists. Ask only follow-ups when needed.

### Core 12 questions

1. What is the recommended setup approach for this solution? (e.g., Docker, devcontainer, native local services, a setup script, etc.)
2. Does that differ for FE vs BE developers?
3. Does that differ for Mac vs Windows?
4. What access and secrets are required, and how should developers get them?
5. Which setup approaches or instructions in the repo are legacy and should not be recommended?
6. What confirms setup is working correctly?
7. What are the top 3 setup problems developers hit, and the best first fix for each?
8. When should a developer escalate instead of continuing to troubleshoot?
9. For the older markdown files I found, should each be preserved, retired, or absorbed?
10. What kinds of changes should always be logged in `.github/copilot/solution-onboarding/change-log-for-ai.md`?
11. Is there anything important about onboarding, setup, troubleshooting, or environment expectations that we have not covered yet?
12. Can you identify any additional places outside of this repo where setup information is documented? (e.g., Confluence, Jira, internal wikis)

### Interview behavior

- Ask one question at a time. Wait for the solutions architect's response before asking the next question.
- Ask all 12 questions in order. Do not skip any question, even if a previous answer seems to partially cover it.
- Track which questions have been asked and confirm all 12 are completed before ending the interview.
- Ask the first draft-informed version of the questions, not generic questions.
- Reference specific files or setup approaches you found when asking for confirmation.
- Keep the interview tight.
- Ask follow-ups only where the repo and current answers are ambiguous. Insert them immediately after the question that prompted them, before continuing to the next core question.
- Use the answers to resolve uncertain sections and legacy-doc handling.

## Step 5: handle older markdown files explicitly

When older markdown files already exist, present a concise recommendation for each file and ask the architect to confirm whether it should be:

- preserved
- retired
- absorbed into the standard files

If a file is absorbed, name the target standard file.
If a file is retired, recommend deprecation wording instead of silent deletion.

## Step 6: finalize the docs

Use `references/section-templates.md` for the required structure.

### Required output behavior

- Keep setup and access/secrets in `.github/copilot/solution-onboarding/setup.md`.
- Keep troubleshooting in `.github/copilot/solution-onboarding/troubleshooting.md`.
- Keep FE/BE and Mac/Windows guidance reflected in both `setup.md` and `environment-matrix.md`.
- Keep `change-log-for-ai.md` reverse chronological.
- Add clear notes where human confirmation is still needed.
- In draft mode, show proposed file contents or diffs.
- In overwrite mode, write the files directly.

## Step 7: generate the onboarding copilot agent

Create `.github/agents/onboarding.agent.md` using `references/onboarding-agent-template.md`.

Follow the template exactly. Do not add a `model:` field — leave model selection to the environment.

## Deliverable checklist

Before finishing, confirm that the repository has:

- reconciled `.github/copilot-instructions.md`
- created `.github/agents/onboarding.agent.md`
- created `.github/copilot/solution-onboarding/setup.md`
- created `.github/copilot/solution-onboarding/troubleshooting.md`
- created `.github/copilot/solution-onboarding/environment-matrix.md`
- created `.github/copilot/solution-onboarding/change-log-for-ai.md`
- recorded unresolved questions or confirmation gaps
- identified the disposition of older markdown files

## Output format

When reporting back, provide:

1. the execution mode used
2. the files created or updated
3. older markdown files found and the recommended disposition for each
4. key architect confirmations still needed, if any
5. any sections that remain intentionally marked for human confirmation
