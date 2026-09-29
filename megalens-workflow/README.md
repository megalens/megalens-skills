# MegaLens Build Workflow Skill

Spec-driven build workflow for Claude Code with MegaLens review gates built in. Takes a project from plain-words idea to shipped code: spec, plan, tasks, implementation, and cross-company review at every gate.

## Install

```
npx skills add https://github.com/megalens/megalens-skills
```

Or copy the `megalens-workflow` folder into your Claude Code skills directory.

## Use

Start a new project and say:

```
Use the megalens-workflow skill. Here is my app idea: ...
```

The workflow needs the MegaLens MCP connected for the review gates: https://megalens.ai

## What it enforces

- Spec is the source of truth, wrong output means fix the spec, not patch the code
- The plan is reviewed by AI models from other companies before any code is written
- Tests are written first, from acceptance criteria, and never weakened to pass
- Every milestone diff is reviewed against the spec in fresh context
- Review findings are a filter, not a verdict, each one is verified before applying
- Nothing ships without your explicit go
