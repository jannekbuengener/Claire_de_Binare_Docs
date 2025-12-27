# .local/ - Machine-Local Workspace State

**⚠️ DO NOT COMMIT THIS DIRECTORY (except this README)**

## Purpose

This directory contains **machine-local state** that should **never** be committed to version control:

- Workspace-level tooling configurations
- IDE settings and caches
- Local environment variables
- Agent runtime state
- Temporary working files

## Structure

```
.local/
├── README.md              # This file (ONLY tracked file)
└── workspaces-root/       # Artifacts from Workspaces Root consolidation
    ├── agents/            # Former .cdb_local/agents/
    ├── .claude/           # Claude CLI configuration
    ├── .vscode/           # VSCode workspace settings
    └── legacy/            # Historical workspace-level files
```

## Rules

1. **Everything in `.local/` is untracked** (except this README)
2. **Never commit secrets, credentials, or API keys**
3. **Machine-specific paths belong here, not in tracked files**
4. **Tooling state goes here, documentation goes in tracked locations**

## Migration Note

This directory was created during the **Workspaces Root Consolidation** (Dec 2025) to centralize machine-local state that previously lived scattered across the Workspaces Root.

**Before:** `C:\Users\janne\Documents\GitHub\Workspaces\` contained mixed tracked/untracked artifacts
**After:** Clean Workspaces Root with only 2 repos; all local state lives here
