# DevSecOps AI Agents

Reusable AI agent profiles for software development, with clear responsibilities, explicit boundaries, and project-specific memory.

The collection currently includes three specialists: **Beck** for back-end development, **Faye** for front-end development, and **Uma** for UX/UI design. Together, they support the design and development portions of a broader DevSecOps workflow.

## Meet the Agents

| Agent | Role | Focus |
| --- | --- | --- |
| **Beck** | Back-end Developer | APIs, business logic, database schemas and migrations, service integrations, server-side authorization, and developer tests |
| **Faye** | Front-end Developer | User interfaces, responsive layouts, accessibility implementation, client-side state, API integration, and developer tests |
| **Uma** | UX/UI Agent | User journeys, information architecture, wireframes, prototypes, interface copy, design-system guidance, and usability reviews |

Each agent follows the project’s existing conventions, asks when a consequential decision is unresolved, and hands off work outside its responsibilities.

## Getting Started

1. Select the agent whose responsibilities match your task.
2. Load its Markdown profile into your AI environment using the environment’s supported agent configuration or instruction-loading mechanism.
3. Provide project context, relevant files, requirements, and acceptance criteria.
4. Configure the tools and permissions needed for the assignment.
5. Review the deliverables, verification evidence, and unresolved dependencies before integrating the work.

The profiles contain YAML frontmatter specifying their names, descriptions, intended handoff partners, model preferences, memory scope, and version metadata. All three currently declare `model: sonnet` and `memory: project`.

Support for configuration fields varies by environment. Verify how your runner handles the frontmatter, particularly `allowed_handoffs`. Automatic delegation requires support from the environment running the agents.

## Example Assignments

### Beck — Back-end Development

> Implement the agreed project-members API using the existing service and database patterns. Enforce server-side authorization, test relevant success and failure cases, and document the contract for Faye.

### Faye — Front-end Development

> Implement the project-members screen from Uma’s approved design using the documented API. Include loading, empty, error, and success states, verify keyboard behavior, and report the checks performed.

### Uma — UX/UI Design

> Design the project-members management flow using our existing design system. Define relevant interaction states, identify unresolved product decisions, and provide an implementation handoff for Faye and Beck.

## Working Together

For a feature involving all three roles:

1. **Uma** defines the experience and communicates the intended behavior.
2. **Beck and Faye** agree on the API contract and implementation dependencies.
3. **Beck** implements the supporting services and data behavior.
4. **Faye** implements the interface and integrates it with those services.
5. **Uma** reviews the implemented experience, while Beck and Faye verify their changes and address findings within their scope.

Work can proceed in parallel when ownership and shared contracts are clear. Each profile identifies the other two agents as intended handoff partners. If delegation is unavailable, the agent asks the user or coordinator how to proceed.

A useful handoff includes:

- The action or decision needed.
- The reason it is needed.
- Relevant requirements, evidence, and constraints.
- Unresolved questions and dependencies.
- What has already been completed or verified.

## Profile Structure

Each profile follows a shared structure:

| Section | Purpose |
| --- | --- |
| Frontmatter | Agent identity, description, and configuration metadata |
| Who Are You | The role’s purpose |
| What You Do | Responsibilities the agent owns |
| Rules | Scope boundaries and actions to avoid |
| What Good Output Looks Like | Expectations for deliverables and verification |
| Memory | Instructions for preserving project knowledge |

## Project Memory

Each agent maintains its own memory file within the project:

| Agent | Memory file |
| --- | --- |
| Beck | `.claude/agent-memory/Beck/MEMORY.md` |
| Faye | `.claude/agent-memory/Faye/MEMORY.md` |
| Uma | `.claude/agent-memory/Uma/MEMORY.md` |

Agents read their own memory at the start of each session and update it at the end. They do not create a root-level `MEMORY.md` or read or edit another role’s memory.

`CLAUDE.md` is authoritative project guidance. Memory notes that conflict with it or the current code must be verified and corrected.

Entries should remain concise and specific to the project. Agents distinguish confirmed decisions from assumptions, revise outdated information, and exclude secrets or sensitive user data.

## Scope and Quality

The current collection covers design and development. Dedicated QA, security-review, operations, and release-management profiles are not yet included.

Each agent is expected to:

- Stay within its assigned responsibilities.
- Preserve existing project conventions and other agents’ work.
- Identify mocks, unresolved dependencies, and verification limitations.
- Report checks as passed only when they were actually run and passed.
- Provide evidence and context for the next person or agent.

Developer tests and design reviews support—but do not replace—independent QA, security review, or release approval.

Role instructions guide behavior. Access permissions, repository protections, and deployment controls must be configured separately in the execution environment.

## Contributing

Contributions should preserve the shared profile structure and keep responsibilities clear.

- Define explicit ownership and practical handoff boundaries.
- Describe observable expectations for quality.
- Avoid unnecessary overlap between roles.
- Keep general instructions independent of specific application frameworks.
- Distinguish runtime-supported settings from descriptive metadata.
- Maintain separate project memory for each agent.
- Base new rules on demonstrated needs and practical experience.
