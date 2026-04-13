---
name: copilot-unlimit-workflow
description: >-
  Interactive workflow skill for AI agents. Enforces a structured design-review-execute loop:
  the agent must analyze the user's request, produce a detailed plan with a todo list,
  then open an interactive confirmation window before execution. After execution, the agent
  must again confirm results with the user. The agent MUST NOT end the conversation without
  explicit user consent. Use for any multi-step code analysis, design, or modification task
  that benefits from iterative user feedback.
license: Apache-2.0
compatibility: Designed for VS Code Copilot, Claude Code, and compatible Agent Skills clients.
metadata:
  author: $workspace
  version: "1.0.0"
---

# Interactive Workflow Skill

## Overview

This skill enforces a structured, interactive workflow for AI agents handling complex tasks.
It prevents the agent from silently completing work without user review, ensuring every
significant output goes through an explicit confirmation loop.

## Core Principles (MUST obey)

1. **Interactive confirmation is mandatory**: After completing any phase output (analysis, design plan, code execution result), the agent MUST open an interactive user inquiry window to ask for confirmation. In VS Code, use the `vscode_askQuestions` tool. In other environments, use the equivalent interactive prompt mechanism.
2. **Never end the conversation unilaterally**: The agent MUST NOT terminate the session unless the user explicitly signals completion (e.g., "done", "finish", "no more changes").
3. **Every reply's final step must be an interactive prompt**: Not a plain text ending, but a structured inquiry with selectable options.

## Workflow Stages

### Stage 1: Receive Request → Analyze & Research

- Deeply analyze the user's question or task description
- Search relevant code, documentation, and context in the workspace
- Identify key modules, conventions, and dependencies
- Avoid blind modifications — understand before acting

### Stage 2: Design Plan → Output in Chat

- Summarize analysis into a detailed design plan
- Build a todo list where each sub-task includes:
  - **Goal**: What problem does this sub-task solve?
  - **Input**: What information or preconditions are needed?
  - **Expected result**: What state should be achieved after completion?
  - **Dependencies**: Does it depend on other sub-tasks?
- Output the complete plan in the chat window

### Stage 3: User Inquiry Window (MUST execute)

- MUST open an interactive confirmation prompt asking:
  - Is the plan reasonable?
  - Are there modifications, additions, or reordering needed?
  - Should execution begin?
- Provide clear selectable options (e.g., "Confirm & Execute", "Needs Modification", "Add Requirements", "End Conversation")
- Incorporate user feedback, update the plan, and repeat Stage 2 → 3 until confirmed

### Stage 4: Execute Tasks

- Execute tasks in the confirmed todo list order
- Track progress with a task management tool
- After each sub-task, briefly describe what was done and the current status
- If the plan changes during execution due to discovered issues, MUST rebuild the todo list and return to Stage 3 for re-confirmation

### Stage 5: Completion → User Inquiry Window Again (MUST execute)

- Summarize what was executed and the results achieved
- MUST open an interactive confirmation prompt asking:
  - Are the results as expected?
  - Are there further improvements needed?
  - Should we end this task?
- Only terminate the session when the user explicitly chooses "End Conversation"

## Todo List Design Requirements

1. Each task must have a clear description with its design logic explained in chat
2. Break plans into actionable sub-tasks with: goal, input, expected result, dependencies
3. After each task execution, briefly summarize its design content and progress
4. If the plan changes, MUST rebuild and update the todo list

## User Inquiry Window Specification

- **Tool**: Use `vscode_askQuestions` in VS Code, or equivalent interactive prompt in other environments
- **When to invoke**:
  - After design plan completion (Stage 3)
  - After task execution completion (Stage 5)
  - When a critical issue is discovered during execution that requires user decision
- **Content requirements**:
  - Include plan confirmation, request for modifications, execution authorization
  - Provide clear selectable options
  - Allow freeform text input for additional context

## Conversation Termination Conditions

The agent may ONLY terminate the conversation when:
- The user explicitly selects an "End Conversation" option in the inquiry window
- The user explicitly uses termination phrases like "done", "finish", "complete", "no more"
- In ALL other cases, the agent MUST NOT terminate

## Prohibited Behaviors

- MUST NOT end the conversation after outputting analysis conclusions
- MUST NOT end the conversation after completing code modifications
- MUST NOT substitute plain text questions for the interactive inquiry tool
- MUST NOT skip any workflow stage
- MUST NOT begin code modifications before the user confirms the plan
