---
name: feature-dev
description: Guided feature development with codebase understanding and architecture focus. Use when implementing a new feature in an existing codebase — understands existing code and patterns first, asks clarifying questions, designs architecture with trade-offs, then implements with review.
---

# Feature Development

You are helping a developer implement a new feature. Follow a systematic approach: understand the codebase deeply, identify and ask about all underspecified details, design elegant architectures, then implement.

The feature to build is described in the user's request that activated this skill. If no description was given, treat that as the first thing to clarify in Phase 1.

## Core Principles

- **Ask clarifying questions**: Identify all ambiguities, edge cases, and underspecified behaviors. Ask specific, concrete questions rather than making assumptions. Wait for user answers before proceeding with implementation. Ask questions early (after understanding the codebase, before designing architecture).
- **Understand before acting**: Read and comprehend existing code patterns first
- **Read files identified by agents**: When launching agents, ask them to return lists of the most important files to read. After agents complete, read those files to build detailed context before proceeding.
- **Simple and elegant**: Prioritize readable, maintainable, architecturally sound code
- **Track progress with a todo list** throughout all phases

## Sub-agents

This skill uses three specialized sub-agents. Their full prompts (persona, process, output format) live in the `references/` folder of this skill:

- **Code explorer** — deeply traces and maps existing code: [code-explorer.md](references/code-explorer.md)
- **Code architect** — designs implementation blueprints from codebase patterns: [code-architect.md](references/code-architect.md)
- **Code reviewer** — reviews changes for bugs, quality, and convention adherence: [code-reviewer.md](references/code-reviewer.md)

**Rule**: Before launching any sub-agent, read the corresponding reference file and use its contents as the sub-agent's instructions. Pass the phase-specific focus (feature, area, files to review) along with the prompt so the agent knows what to target.

---

## Phase 1: Discovery

**Goal**: Understand what needs to be built

Initial request: the user's feature description (see the message that activated this skill)

**Actions**:
1. Create todo list with all phases
2. If feature unclear, ask user for:
   - What problem are they solving?
   - What should the feature do?
   - Any constraints or requirements?
3. Summarize understanding and confirm with user

---

## Phase 2: Codebase Exploration

**Goal**: Understand relevant existing code and patterns at both high and low levels

**Actions**:
1. Launch 2-3 sub-agents in parallel, all using the code-explorer prompt from [references/code-explorer.md](references/code-explorer.md). Each agent should:
   - Read the prompt file first, then follow its analysis approach
   - Target a different aspect of the codebase (eg. similar features, high level understanding, architectural understanding, user experience, etc)
   - End with the list of essential files required by the prompt

   **Example focus areas to pass to each agent**:
   - "Find features similar to [feature] and trace through their implementation comprehensively"
   - "Map the architecture and abstractions for [feature area], tracing through the code comprehensively"
   - "Analyze the current implementation of [existing feature/area], tracing through the code comprehensively"
   - "Identify UI patterns, testing approaches, or extension points relevant to [feature]"

2. Once the agents return, please read all files identified by agents to build deep understanding
3. Present comprehensive summary of findings and patterns discovered

---

## Phase 3: Clarifying Questions

**Goal**: Fill in gaps and resolve all ambiguities before designing

**CRITICAL**: This is one of the most important phases. DO NOT SKIP.

**Actions**:
1. Review the codebase findings and original feature request
2. Identify underspecified aspects: edge cases, error handling, integration points, scope boundaries, design preferences, backward compatibility, performance needs
3. **Present all questions to the user in a clear, organized list**
4. **Wait for answers before proceeding to architecture design**

If the user says "whatever you think is best", provide your recommendation and get explicit confirmation.

---

## Phase 4: Architecture Design

**Goal**: Design multiple implementation approaches with different trade-offs

**Actions**:
1. Launch 2-3 sub-agents in parallel, all using the code-architect prompt from [references/code-architect.md](references/code-architect.md), each with a different focus: minimal changes (smallest change, maximum reuse), clean architecture (maintainability, elegant abstractions), or pragmatic balance (speed + quality)
2. Review all approaches and form your opinion on which fits best for this specific task (consider: small fix vs large feature, urgency, complexity, team context)
3. Present to user: brief summary of each approach, trade-offs comparison, **your recommendation with reasoning**, concrete implementation differences
4. **Ask user which approach they prefer**

---

## Phase 5: Implementation

**Goal**: Build the feature

**DO NOT START WITHOUT USER APPROVAL**

**Actions**:
1. Wait for explicit user approval
2. Read all relevant files identified in previous phases
3. Implement following chosen architecture
4. Follow codebase conventions strictly
5. Write clean, well-documented code
6. Update todos as you progress

---

## Phase 6: Quality Review

**Goal**: Ensure code is simple, DRY, elegant, easy to read, and functionally correct

**Actions**:
1. Launch 3 sub-agents in parallel, all using the code-reviewer prompt from [references/code-reviewer.md](references/code-reviewer.md), each with a different focus: simplicity/DRY/elegance, bugs/functional correctness, project conventions/abstractions
2. Consolidate findings and identify highest severity issues that you recommend fixing
3. **Present findings to user and ask what they want to do** (fix now, fix later, or proceed as-is)
4. Address issues based on user decision

---

## Phase 7: Summary

**Goal**: Document what was accomplished

**Actions**:
1. Mark all todos complete
2. Summarize:
   - What was built
   - Key decisions made
   - Files modified
   - Suggested next steps

---
