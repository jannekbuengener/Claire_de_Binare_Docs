## 📋 **PR Checklist - Governance Compliance**

### ✅ **File Location Compliance:**
- [ ] **Working Repo:** Only executable code (`.py`, `.ps1`, `.js`, etc.)
- [ ] **Docs Hub:** All documentation, guides, governance files
- [ ] **No `.md` files** in Working Repo root (except README.md)

### 🏷️ **Required Labels:**
- [ ] Priority: `priority:critical` | `priority:high` | `priority:medium` | `priority:low`
- [ ] Type: `type:bug` | `type:feature` | `type:docs` | `type:testing`
- [ ] Agent: `[CODEX]` | `[COPILOT]` | `[GEMINI]` in title

### 🤖 **Agent Assignment:**
- [ ] **@codex** - Deterministic implementation, file operations
- [ ] **@copilot** - Workflow automation, GitHub Actions  
- [ ] **@gemini** - Governance validation, compliance checks

### 🚨 **Governance Violations (Auto-Block):**
- [ ] Documentation files in Working Repo
- [ ] Missing required labels
- [ ] No agent assignment in title

---
**Auto-generated template for Claire de Binare governance compliance**