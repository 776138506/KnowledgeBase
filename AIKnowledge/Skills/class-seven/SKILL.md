---
name: "class-seven"
description: "Provides Class Seven multi-agent development team functionality. Invoke when user needs complex development tasks requiring multiple perspectives/roles, PM planning, architecture, implementation, and testing."
---

# Class Seven

Class Seven (七班) is a structured multi-agent workflow that treats sub-agents as specialized development team members.

## When to Use

Use this skill when:

- Complex development tasks requiring multiple perspectives/roles
- Tasks needing PM planning + architecture + implementation + testing
- Debugging scenarios requiring systematic investigation
- Code review and quality assurance workflows
- Projects requiring end-to-end delivery (plan → build → test → deploy)

## Team Structure

```
Main Session (Manager)
├── PM Agent (产品经理)
├── Architect Agent (架构师)
├── Developer Agent (开发工程师)
├── Tester Agent (测试工程师)
└── Debugger Agent (调试专家)
```

## Workflow Phases

### Phase 1: Task Analysis & Planning
- Manager (Main Session) analyzes task complexity
- Spawn PM Agent for requirement clarification
- PM returns: requirements doc, scope, acceptance criteria

### Phase 2: Architecture & Design
- Spawn Architect Agent with PM output
- Architect returns: tech stack, module design, interfaces

### Phase 3: Implementation
- Spawn Developer Agent with architecture specs
- Developer returns: implemented code

### Phase 4: Quality Assurance
- Spawn Tester Agent with code + requirements
- Tester returns: test plan, test cases, bugs found

### Phase 5: Debugging (if needed)
- Spawn Debugger Agent with bug reports
- Debugger returns: root cause analysis, fixes

### Phase 6: Integration & Delivery
- Manager reviews all outputs
- Integrates final deliverable
- Validates against acceptance criteria

## Agent Personas

### PM Agent
- **Role**: 产品经理
- **Expertise**: Requirements analysis, user stories, acceptance criteria
- **Output**: PRD, user stories, scope definition
- **Tools**: Kimi (for Chinese context), Claude Code (for complex products)

### Architect Agent
- **Role**: 架构师
- **Expertise**: System design, tech stack selection, API design
- **Output**: Architecture doc, module diagrams, interface specs
- **Tools**: Claude Code (preferred for architecture), Kimi (for validation)

### Developer Agent
- **Role**: 开发工程师
- **Expertise**: Code implementation, refactoring, optimization
- **Output**: Production-ready code
- **Tools**: Claude Code (complex logic), Kimi (quick implementation), Native (boilerplate)

### Tester Agent
- **Role**: 测试工程师
- **Expertise**: Test design, edge case identification, quality assurance
- **Output**: Test cases, test scripts, bug reports
- **Tools**: Native (execution), Kimi (test design), Claude Code (complex scenarios)

### Debugger Agent
- **Role**: 调试专家
- **Expertise**: Root cause analysis, performance profiling, bug fixing
- **Output**: RCA report, patches, prevention recommendations
- **Tools**: Claude Code (deep analysis), Kimi (pattern matching)

## Execution Modes

- **Mode A: Full Team (Full Orchestration)**: All 5 phases executed sequentially. Use for complex projects.
- **Mode B: Sprint Team (Dev + Test)**: Skip PM/Architect phases. Use when requirements are clear.
- **Mode C: Firefighter (Debug Only)**: Debugger agent only. Use for urgent bug fixes.
- **Mode D: Review Board (PM + Tester)**: Code review workflow. Use for quality gates.

## Quick Commands

```bash
# Full team deployment
class_seven deploy --mode=full --task="<description>"

# Sprint mode
class_seven deploy --mode=sprint --specs="<requirements>"

# Debug mode
class_seven deploy --mode=debug --bug="<bug description>"
```

## Best Practices

- Always start with task analysis - Determine mode and required agents
- Pass context explicitly - Each agent receives relevant previous outputs
- Set clear boundaries - Define what each agent should/shouldn't do
- Use appropriate timeout - Complex tasks need longer timeouts
- Review before integration - Manager validates all outputs

## Error Handling

If an agent fails or produces insufficient output:

- Analyze failure reason
- Respawn with clearer instructions or different tool
- Consider breaking task into smaller sub-tasks
- Escalate to human if stuck after 2 retries

## References

- Detailed workflow patterns: See references/workflows.md
- Tool integration guide: See references/tools-guide.md
- Example projects: See references/examples.md