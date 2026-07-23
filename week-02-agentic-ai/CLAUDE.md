# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

This is **Week 2: Agentic AI** from the DevOps Micro Internship (DMI) Cohort 3. The project is a learning-focused assignment track covering Claude Code capabilities and agentic AI patterns. The learner is completing 8 sequential assignments to build practical knowledge of:

- The Agentic Loop (Gather → Act → Verify)
- CLAUDE.md file design
- Skills system for controlled automation
- Subagents for specialized AI delegation
- MCP servers for external system integration
- Hooks and permissions management
- Claude Code's memory system
- Reflection and knowledge synthesis

## Assignment Structure

All assignments follow a consistent format with:

- **Purpose**: The learning goal
- **Tasks**: Numbered subtasks with specific deliverables
- **Evidence**: Screenshots or completed code demonstrating task completion
- **Submission**: GitHub repository link for version control

### Directory Structure

```
.
├── assignment-01-setup-agentic-loop.md    # Installing Claude Code, basic setup
├── assignment-02-claude-md.md              # Creating/customizing CLAUDE.md
├── assignment-03-skills.md                 # Building .claude/skills/ system
├── assignment-04-subagents.md              # Building .claude/agents/ delegation
├── assignment-05-mcp.md                    # Configuring MCP servers
├── assignment-06-hooks-permissions.md      # Setting up automation & access control
├── assignment-07-memory.md                 # Using Claude's persistent memory
├── assignment-08-week-2-reflection.md      # Synthesis & public learning
├── assignment-briefs/                      # Original assignment specifications
├── assignment-solutions/                   # Reference solutions
└── [screenshots]                           # Evidence images for submission
```

## Key Concepts

### The Agentic Loop

Claude's core capability: **Gather** (read files, run commands) → **Act** (modify, create, delegate) → **Verify** (confirm success, check assumptions). All assignments demonstrate this pattern.

### Skills (`/.claude/skills/`)

Predefined command blocks with:
- Restricted tool access (Bash, Read, Grep but not Write)
- Specific model configurations
- Pre-written prompts for domain tasks (e.g., `/scaffold-terraform`, `/tf-plan`)
- Can disable model invocation for deterministic execution

### Subagents (`/.claude/agents/`)

Specialized AI delegates with their own:
- Model choice (Haiku for cost, Sonnet for complexity)
- Tool permissions (security-auditor has no Write)
- Reasoning patterns
- Launched via `Agent()` tool

### MCP Servers (`.mcp.json`)

External system integrations (GitHub, databases, APIs):
- Define available tools for Claude
- Authenticate via env vars in `.claude/settings.local.json`
- Verify with `/mcp` command
- Enable real-time data access

### Hooks (`.claude/settings.json`)

Automation rules that fire on events (on-success, on-error, before-submit, etc.). Can run arbitrary commands but do not have access to Claude's context.

### Memory System

Persistent recall across sessions:
- User memories (role, preferences, knowledge)
- Feedback memories (what to avoid/repeat)
- Project memories (current goals, deadlines)
- Reference memories (where to find things)

Stored in `~/.claude/projects/<project>/memory/` with MEMORY.md index.

## Common Working Patterns

### Submitting Assignments

1. **Complete the assignment** using Claude Code in VS Code or browser
2. **Commit and push** to GitHub fork (repo: `enejepromise/Ultimate-Agentic-DevOps-with-Claude-Code`)
3. **Add evidence** (screenshots showing tool calls, command output, file changes)
4. **Update assignment file** with completion status and submission link

### Testing Claude's Behavior

Assignment 2 establishes the verify pattern:
1. **Before state**: Observe Claude's generic response (baseline)
2. **Add CLAUDE.md**: Customize with project rules
3. **After state**: Verify Claude's response changes (shows context was loaded)
4. **Compare**: Demonstrate the instruction impact

### Skill Testing Pattern (Assignment 3)

1. Run `/scaffold-terraform` to generate infrastructure
2. Verify generated files exist in VS Code
3. Run `terraform init` (local setup)
4. Execute `/tf-plan` to verify skill execution
5. Check output analysis (Claude reads terraform plan output)

### Subagent Delegation (Assignment 4)

Create agent definitions in `.claude/agents/`:
- `security-auditor.md` — analyze infrastructure risks (no Write tools)
- `cost-optimizer.md` — suggest cost reductions (Haiku model)
- `tf-writer.md` — generate Terraform code (inherit model)

Trigger with `Agent()` tool, agent returns structured findings.

### MCP Integration (Assignment 5)

1. Create GitHub Personal Access Token
2. Define `.mcp.json` with GitHub server config
3. Store token in `.claude/settings.local.json`
4. Verify with `/mcp` command
5. Test with real GitHub queries (fetch README, list issues, etc.)

## File Conventions

- **Assignment files**: `assignment-NN-name.md` (working versions)
- **Brief files**: `assignment-briefs/assignment-NN-name.md` (original spec)
- **Solution files**: `assignment-solutions/assignment-NN-name.md` (reference)
- **Screenshots**: Named by task (`Task1 screenshot 1.png`, etc.)
- **Terraform artifacts**: Generated to `./terraform/` by skill
- **.claude/** hidden directory: Project configuration (not committed to main repo)

## Learning Progression

Each assignment builds on prior knowledge:

| Assignment | Focus | Prerequisite |
|:---|:---|:---|
| 1 | CLI Setup & Agentic Loop | None |
| 2 | Project Documentation | Assignment 1 |
| 3 | Skill Building & Tool Restriction | Assignment 2 |
| 4 | Subagent Specialization | Assignment 3 |
| 5 | External System Integration | Assignment 4 |
| 6 | Automation & Access Control | Assignment 5 |
| 7 | Persistent Context & Recall | Assignment 6 |
| 8 | Synthesis & Public Learning | All prior |

## Testing Assignments

When helping with any assignment:

1. **Read the assignment file** to understand the specific goal
2. **Check the evidence requirements** (screenshots, code output, answers)
3. **Follow the Agentic Loop**: gather (read files/run commands) → act (complete task) → verify (check results)
4. **Capture evidence** as you work (screenshot tool calls, file changes, command output)
5. **Update assignment file** with completed sections

For assignments with BEFORE/AFTER testing (like Assignment 2), explicitly show:
- Claude's response WITHOUT context loaded
- Claude's response WITH context loaded
- The behavioral difference

## Important Notes

- **GitHub fork**: This is a personal learning fork of the Ultimate-Agentic-DevOps-with-Claude-Code repository
- **.claude/ directory**: Project settings are not committed to git (per Assignment 6)
- **Credentials**: Store in `.claude/settings.local.json`, never in main code
- **Assignment brevity**: Assignments are intentionally short to encourage exploration—the learning happens in the experimentation
- **Reflection focus**: Assignment 8 emphasizes transferring knowledge to public learning (blog, LinkedIn)

## References

- **DMI Program**: DevOps Micro Internship by Pravin Mishra (The CloudAdvisory)
- **Claude Code Documentation**: https://claude.ai/code
- **Anthropic API**: https://api.anthropic.com
- **GitHub MCP Server**: https://github.com/modelcontextprotocol/servers
