## Starting a project
Source: https://docs.google.com/document/d/121dFvASh8Xd8rR_YKXWJ2arWKqMQvo2AOR9lKFxRMIg/edit?tab=t.0

```
// High level app requirements as dot points

Ask me questions to clarify product requirements, technical requirements, engineering principles and constraints
```
- Shift + Tab to plan mode
- Press enter
- Answer questions
- Critically review the plan
	- You will likely need to correct some details of the implementation plan
- Run the app yourself and manually test
	- Likely their are some bugs
- Commit early and often before fixing bugs

## Prompt to create CLAUDE.md - Existing project
Source: https://docs.google.com/document/d/121dFvASh8Xd8rR_YKXWJ2arWKqMQvo2AOR9lKFxRMIg/edit?tab=t.0

- Use `CLAUDE.md` what, how and why?

```
Analyze this codebase and create a CLAUDE.md file following these principles:

1. Keep it under 150 lines total - focus only on universally applicable information
2. Cover the essentials: WHAT (tech stack, project structure), WHY (purpose), and HOW (build/test commands)
3. Use Progressive Disclosure: instead of including all instructions, create a brief index pointing to other markdown files in .claude/docs/ for specialized topics
4. Include file:line references instead of code snippets
5. Assume I'll use linters for code style - don't include formatting guidelines

Structure it as: project overview, tech stack, key directories/their purposes, essential build/test commands, and a list of additional documentation files Claude should check when relevant.

Additionally, extract patterns you observe into separate files:

- .claude/docs/architectural_patterns.md - document the architectural patterns, design decisions, and conventions used (e.g., dependency injection, state management, API design patterns). Make sure these are patterns that appear in multiple files.

Reference these files in the CLAUDE.md's "Additional Documentation" section.
```

 