# Section Templates

Use these templates when drafting or rewriting the standard files.

## .github/copilot/solution-onboarding/setup.md

Use this exact section order unless the user explicitly requests a change.

# Setup

## Purpose
Briefly describe what the solution is and who this guide is for.

## Audience Notes
Summarize FE vs BE differences and any high-level Mac vs Windows notes.

## Prerequisites
List required runtimes, tools, accounts, VPN, and machine assumptions.

## Access and Secrets
Describe required access, secrets, and how developers obtain them. Never include secret values.

## Recommended Setup Approach
Describe the preferred setup approach. Split FE vs BE and Mac vs Windows only where needed.

## Step-by-Step Setup
Give a practical sequence.

## Validation Checklist
State the minimum checks that confirm setup is working.

## Common Setup Blockers
List the most likely blockers during first-time setup.

## Escalation Path
State when to stop troubleshooting and who or what to escalate to.

## Human Confirmation Notes
Capture any remaining assumptions or unverified details.

## .github/copilot/solution-onboarding/troubleshooting.md

# Troubleshooting

## How to Use This Guide
Explain how a developer should work through the guide.

## Common Symptoms
List symptoms developers are likely to see.

## Likely Causes
Map symptoms to common causes.

## Resolution Steps
Provide the best first fix, then deeper checks.

## Logs and Evidence to Gather
List the commands, screenshots, logs, or config details to collect before escalating.

## Escalation Criteria
State when local troubleshooting should stop.

## Human Confirmation Notes
Capture any remaining assumptions or unverified details.

## .github/copilot/solution-onboarding/environment-matrix.md

# Environment Matrix

## How to Read This Matrix
Explain that it captures supported onboarding variations.

## Matrix
Use a table with these columns when possible:
- role
- operating system
- runtimes / versions
- required tools
- local services
- supported setup path
- notable caveats

## Notes
Capture exceptions, unsupported combinations, or pending clarifications.

## .github/copilot/solution-onboarding/change-log-for-ai.md

# Change Log for AI

## Purpose
Explain that this file records setup-impacting changes that help future AI guidance stay current.

## What Belongs Here
Record changes such as runtime version changes, package manager changes, environment configuration changes, startup script changes, devcontainer or docker changes, service dependency changes, and new required setup steps.

## Entries
Keep entries reverse chronological. Each entry should include:
- date
- change summary
- setup impact
- docs updated
- human confirmation status

Example entry:

### 2026-03-15
- **Change summary:** Switched local startup from npm to pnpm.
- **Setup impact:** Developers must install pnpm and use `pnpm install` and `pnpm dev`.
- **Docs updated:** `.github/copilot/solution-onboarding/setup.md`, `.github/copilot/solution-onboarding/environment-matrix.md`
- **Human confirmation status:** Confirmed by solutions architect.
