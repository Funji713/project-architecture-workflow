# Project Architecture Workflow

Builds implementation-ready software architecture with minimal unnecessary complexity. It is intended for new projects, substantial features, module boundaries, directory layout, service or data interfaces, executable architecture plans, and visible implementation-progress conformance.

## Install

Run this in PowerShell to install directly into your local Codex skills directory:

```powershell
git clone https://github.com/Funji713/project-architecture-workflow.git "$env:USERPROFILE\.codex\skills\project-architecture-workflow"
```

To update an existing installation:

```powershell
git -C "$env:USERPROFILE\.codex\skills\project-architecture-workflow" pull --ff-only
```

Start a new Codex task after installation if the current task does not discover the skill.

## Use

```text
$project-architecture-workflow Design the architecture for a multi-branch inventory and POS system, including milestones and conformance tracking.
```

The skill separates architecture decisions from implementation, favors a small verifiable first vertical slice, and maintains evidence-based architecture and implementation status for multi-slice work.

See [SKILL.md](SKILL.md) for the full workflow.
