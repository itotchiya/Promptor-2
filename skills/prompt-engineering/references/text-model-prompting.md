# Text Model Prompting — Deep Dive

## Claude (Anthropic)

### Architecture & Processing
- Processes XML tags as semantic structure — use them to clearly delineate sections
- Long context window (200K tokens) — supply complete documents rather than extracts
- Strong instruction-following — be explicit about format, tone, and constraints

### Optimal Prompt Structure
```
<context>
Background information the model needs
</context>

<role>
Who the model should act as, with domain expertise specified
</role>

<instructions>
Step-by-step task description
</instructions>

<constraints>
What to avoid, length limits, format requirements
</constraints>

<examples>
<example>
Input: ...
Output: ...
</example>
</examples>

<output_format>
Exact structure of desired response
</output_format>
```

### Best Practices
- Use `<thinking>` blocks for complex reasoning tasks
- Prefill the assistant turn to steer output format
- Provide both positive and negative examples
- Place the most important instructions at the beginning and end of the prompt
- Use numbered steps for sequential tasks
- Specify "Do NOT..." for common failure modes

---

## ChatGPT / GPT-4 (OpenAI)

### Architecture & Processing
- Three-role structure: System, User, Assistant
- System prompt sets persistent behavior and constraints
- Temperature and top_p control creativity vs. determinism

### Optimal Prompt Structure
```
System: You are a [role] specializing in [domain]. You always [behavior].
You never [anti-behavior]. Output format: [format].

User: [Context paragraph]

[Specific task with numbered steps]

[Constraints and preferences]

[Example of desired output]
```

### Best Practices
- System prompt for role, tone, and persistent rules
- User prompt for specific task and context
- Use markdown formatting (headers, lists, code blocks)
- "Let's think step by step" for reasoning tasks
- Specify output length ("in 3 paragraphs", "in under 100 words")
- Custom GPTs for reusable prompt configurations

---

## Gemini (Google)

### Architecture & Processing
- Native multimodal — can process text, images, video, audio together
- Grounding feature connects to Google Search for real-time facts
- Structured output mode for JSON responses

### Optimal Prompt Structure
```
System instruction: [Persistent behavior and role definition]

[Context and background]

[Task description with clear steps]

[Output format specification — use JSON mode when structured data is needed]

[Grounding instruction if factual accuracy is critical]
```

### Best Practices
- Leverage multimodal inputs — upload images/docs directly
- Use grounding for factual queries to reduce hallucination
- Specify JSON schema for structured outputs
- Break complex tasks into numbered sub-tasks
- Provide examples with diverse edge cases
