---
name: megalens-workflow
description: Spec-driven build workflow with MegaLens review gates. Use when starting a new app or feature, or when the user asks to build with the MegaLens workflow. Takes a project from plain-words idea to shipped code through spec, plan, tasks, implementation, and cross-company review gates.
---

# MegaLens Build Workflow

Follow these phases in order. Never skip a gate. The spec is the source of truth for the whole project.

## Phase 0, Abstract
The user describes what the app must do in plain words. Ask clarifying questions, at most 5 to 7, batched in one message. Do not write any code or plan yet.

## Phase 1, Spec
Write `spec.md` from the abstract:
- Functional requirements
- Acceptance criteria per feature
- Failure modes and how each must behave
- Security and permissions
- Out of scope list

Rule: if output is ever wrong later, start with the spec. If a requirement is missing or wrong, fix it in the spec and regenerate the affected work. If the requirement was right and the code missed it, fix the code. Never patch code and leave the spec behind.

## Phase 2, Plan
Write `plan.md` from `spec.md`: architecture, file structure, database tables, external services.

STOP here. Send the plan to MegaLens for review before any code is written. MegaLens has AI models from other companies review it, because the model that writes a plan should not be the one that approves it. Apply the findings you agree with. List the findings you reject and the reason, and show that list to the user. Wait for the user's go before Phase 3.

## Phase 3, Tasks
Break the plan into `tasks.md`: small tasks, each completable and testable on its own, grouped into milestones. No task bigger than one review sitting.

## Phase 4, Implement
One task at a time:
1. Write tests first, from the acceptance criteria in `spec.md`
2. Write code until tests pass
3. Run lint and type checks

Never weaken or delete a failing test to get to green. Fix the code, or flag the conflict with the spec to the user. Keep `tasks.md` status current.

## Phase 5, Review gate, per milestone
Send `spec.md` plus the diff to MegaLens for review. Never send the chat that produced the code. The spec goes along as context, so the reviewers, reading in fresh context, can see what the code was meant to do. Checking that the finished work meets the spec stays with you and the user; that is what the Phase 4 tests are for.

Treat review findings as a filter, not a verdict. Verify each finding against the actual code before applying it. Show the user the findings you rejected and why.

## Phase 6, Ship
Nothing deploys without the user's explicit go. Give the user a short deploy report first: what changed, test count, and any deviation from `spec.md` with the reason.

## Standing rules
- Secrets never in code or frontend
- Database never readable or writable without auth
- Ambiguous requirement mid-task: stop and ask the user, never guess and build
