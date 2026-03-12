# Code Model Prompting — Deep Dive

## Bolt (StackBlitz)

### Processing Logic
- Generates full project scaffolds from prompts
- Understands framework-specific patterns (React, Next.js, Vue, Svelte)
- Processes instructions as project specifications
- Iterates on existing code with follow-up prompts

### Optimal Prompt Structure
```
Build a [type of application] using [framework + version].

Tech stack:
- Frontend: [framework]
- Styling: [CSS solution]
- State management: [library]
- Backend: [if applicable]

Features:
1. [Feature with specific behavior]
2. [Feature with specific behavior]

Design:
- [Color scheme, layout preferences]
- [Responsive requirements]
- [UI component library if any]

Behavior:
- [User flow description]
- [Edge cases to handle]
```

### Best Practices
- Specify the complete tech stack upfront
- Describe features as user stories with acceptance criteria
- Include design preferences (colors, layout, responsive behavior)
- Reference specific UI patterns ("like Notion's sidebar", "like Stripe's pricing table")
- For iterations, reference specific files and line numbers
- Ask for one major feature per prompt for best results

---

## Cursor

### Processing Logic
- Context-aware — reads your open files and project structure
- Composer mode for multi-file changes
- Tab completion for inline suggestions
- Chat mode for explanations and complex refactors

### Optimal Prompt Structure (Chat/Composer)
```
[Context: what you're working on and why]

[Specific task with file references]

Constraints:
- [Coding patterns to follow]
- [Libraries to use or avoid]
- [Naming conventions]

Expected behavior:
- Input: [example input]
- Output: [example output]
```

### Best Practices
- Reference files with `@filename` for context
- Use `@codebase` for project-wide understanding
- Specify "edit" vs. "create" vs. "refactor" clearly
- Include type definitions and interfaces for typed languages
- Use Cursor Rules (`.cursorrules` file) for project-wide conventions
- Composer mode for changes spanning multiple files

---

## GitHub Copilot

### Processing Logic
- Inline completion based on surrounding code context
- Comment-driven generation — comments become code
- Understands file structure and imports
- Chat mode for explanations and refactoring

### Optimal Comment-to-Code Pattern
```
// Function: [name]
// Purpose: [what it does]
// Parameters: [param: type — description]
// Returns: [type — description]
// Edge cases: [what to handle]
// Example: [input] -> [output]
```

### Best Practices
- Write descriptive function signatures before implementation
- Use JSDoc/docstring comments as generation guides
- Keep files focused — Copilot uses the current file as primary context
- Open related files in adjacent tabs for cross-file context
- Accept suggestions incrementally, line by line for complex code
- Use chat for refactoring and explanations, inline for new code

---

## General Code Prompting Principles

### For All Code-Gen Tools
1. **Specify the language and version** — "Python 3.12", "TypeScript 5.x", "Rust 2024 edition"
2. **Provide type signatures/interfaces** — Define data shapes before asking for implementations
3. **Include test cases** — Show expected input/output pairs
4. **Reference patterns** — "Use the repository pattern", "Follow SOLID principles"
5. **Specify error handling** — "Throw typed errors", "Return Result types", "Use try-catch with specific exceptions"
6. **Define naming conventions** — camelCase, snake_case, naming prefixes
7. **State performance requirements** — "Must handle 10K items", "O(n log n) or better"
