# Image Model Prompting — Deep Dive

## Midjourney

### Processing Logic
- Processes prompts as weighted keyword sequences, not natural language
- Earlier words carry more weight
- Parameters appended after `--` modify generation behavior
- Multi-prompt syntax with `::` for weighted blending

### Prompt Formula
```
[Subject] [Style/Medium] [Environment/Setting] [Lighting] [Composition] [Mood] --parameters
```

### Key Parameters
| Parameter | Function | Example |
|-----------|----------|---------|
| `--ar` | Aspect ratio | `--ar 16:9` |
| `--v` | Model version | `--v 6.1` |
| `--s` | Stylize (0-1000) | `--s 750` |
| `--c` | Chaos/variety (0-100) | `--c 25` |
| `--q` | Quality (0.25-2) | `--q 2` |
| `--no` | Negative prompt | `--no text, watermark` |
| `--sref` | Style reference | `--sref [URL]` |
| `--cref` | Character reference | `--cref [URL]` |
| `--tile` | Seamless pattern | `--tile` |

### Best Practices
- Front-load the subject and most important descriptors
- Use art movement names for style: "art nouveau", "brutalism", "impressionist"
- Specify medium: "oil painting", "watercolor", "3D render", "photograph"
- Add lighting: "golden hour", "studio lighting", "dramatic chiaroscuro"
- Use camera terms for realism: "85mm lens", "shallow depth of field", "wide angle"
- Multi-prompt weighting: `cat::2 dog::1` (cat emphasized 2x)

---

## DALL-E 3 (OpenAI)

### Processing Logic
- Interprets full natural language descriptions
- Internally rewrites prompts for clarity — keep original intent clear
- Handles complex compositions better than predecessors
- Text rendering support (specify text in quotes)

### Prompt Formula
```
[Detailed description of scene] in the style of [artistic style].
[Composition details]. [Lighting and mood]. [Technical specifications].
```

### Best Practices
- Write complete descriptive sentences, not keyword lists
- Be explicit about spatial relationships ("to the left of", "in the background")
- Specify art style and medium clearly
- Include emotional tone and atmosphere
- For text in images, put desired text in quotes
- Aspect ratio controlled via API parameter, not prompt

---

## Stable Diffusion

### Processing Logic
- Separate positive and negative prompt fields
- Token weighting with parentheses: `(keyword:1.5)` increases weight
- Processes tokens sequentially — order matters
- Model checkpoint, sampler, and steps affect output significantly

### Positive Prompt Formula
```
[Quality tags], [Subject], [Style], [Details], [Lighting], [Composition]
```

### Negative Prompt (Common)
```
(worst quality:1.4), (low quality:1.4), blurry, deformed, disfigured,
bad anatomy, extra limbs, watermark, text, signature
```

### Key Techniques
- Quality boosters: "masterpiece, best quality, highly detailed, sharp focus"
- Weighting: `(element:1.3)` for emphasis, `(element:0.7)` to reduce
- BREAK keyword to separate prompt sections across attention layers
- LoRA syntax: `<lora:model_name:weight>` for fine-tuned styles
- Controlnet for pose/composition control
- Embeddings for trained concepts: `embedding_name`

### Best Practices
- Start with quality tags
- Use specific artist names or art style names
- Negative prompt is essential — always include one
- Experiment with sampler choice (Euler a, DPM++ 2M Karras)
- CFG Scale 7-12 for most use cases
- Higher step count (30-50) for quality, lower (15-20) for speed
