---
name: prompt-engineering
description: >
  This skill provides expert knowledge on prompt engineering best practices
  for different AI tools and models. Use when the user asks to "create a prompt",
  "write a prompt", "optimize a prompt", "improve a prompt", mentions
  "prompt engineering", or needs guidance on crafting effective prompts for
  specific AI platforms like Claude, ChatGPT, Midjourney, DALL-E, Stable Diffusion,
  Bolt, Cursor, or Gemini.
version: 0.1.0
---

# Prompt Engineering Knowledge Base

Expert reference for crafting optimized prompts across AI platforms. Each tool has unique processing characteristics that demand specific prompt architectures.

## General Principles (All Tools)

- Be specific and unambiguous — vague prompts yield vague results
- Provide context before instructions
- Use structured formatting when the tool supports it
- Include examples of desired output when possible (few-shot prompting)
- Specify constraints, tone, audience, and format explicitly
- Break complex tasks into sequential steps
- Define the role/persona the AI should adopt

## Tool-Specific Quick Reference

### Claude (Anthropic)
- Excels with XML tags for structure (`<context>`, `<instructions>`, `<examples>`, `<output_format>`)
- Supports system prompts for persistent behavior
- Responds well to chain-of-thought reasoning requests
- Use `<thinking>` tags to encourage step-by-step reasoning
- Prefill assistant responses to guide output format
- Long-context capable — provide full documents rather than summaries

### ChatGPT / GPT-4 (OpenAI)
- System / User / Assistant role separation is key
- Responds well to persona assignment in system prompt
- Use markdown formatting in prompts
- Custom Instructions for persistent context
- Benefits from explicit output format specification
- Chain-of-thought via "Let's think step by step"

### Midjourney
- Prompt = subject + style + parameters
- Key parameters: `--ar` (aspect ratio), `--v` (version), `--s` (stylize), `--c` (chaos), `--q` (quality)
- Front-load important descriptors
- Use style references: `--sref`, `--cref` for character consistency
- Negative prompting with `--no` parameter
- Short, descriptive phrases outperform long sentences

### DALL-E (OpenAI)
- Descriptive natural language works best
- Specify art style, medium, lighting, composition
- Camera angles and lens types for photorealistic results
- Avoid complex multi-subject scenes
- Be explicit about spatial relationships

### Stable Diffusion
- Positive and negative prompts are separate
- Keyword weighting with `(keyword:weight)` syntax
- Embedding and LoRA references for fine-tuned styles
- Sampler and step count affect output significantly
- Quality tags: "masterpiece, best quality, highly detailed"

### Bolt / Cursor / Code-Gen Tools
- Specify language, framework, and version explicitly
- Include file structure and naming conventions
- Provide interface/type definitions upfront
- Reference existing code patterns in the project
- Use variables and placeholder syntax native to the tool
- Describe expected behavior with input/output examples

### Gemini (Google)
- Supports multimodal input natively
- Grounding with Google Search for factual accuracy
- Structured output with JSON mode
- System instructions for persistent behavior
- Effective with step-by-step task decomposition

## Detailed References

For in-depth best practices per platform, consult:
- **`references/text-model-prompting.md`** — Deep-dive on Claude, GPT, Gemini prompting
- **`references/image-model-prompting.md`** — Deep-dive on Midjourney, DALL-E, Stable Diffusion
- **`references/code-model-prompting.md`** — Deep-dive on Bolt, Cursor, Copilot, code generation
