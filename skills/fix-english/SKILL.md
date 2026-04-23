---
name: fix-english
description: Rewrite a sentence into correct, natural English and offer a few tone variations. Use when the user asks to fix grammar, correct a sentence, or invokes /fix-english.
user_invocable: true
---

# Fix English

Rewrite the user's sentence into clear, grammatically correct English and offer a small set of alternatives so they can pick the tone that fits.

## Process

1. Read the sentence the user provided.
2. If NO sentence was provided (empty argument), offer two options:

   > Which sentence should I fix?
   > 1. Paste the sentence you want me to fix.
   > 2. Fix the previous prompt: "{preview of the user's most recent prior message}"

   For the preview, if the prior message is longer than ~60 characters, show the first ~20 chars + `...` + the last ~20 chars (e.g. `"i see Server Requi... heading for it"`). Otherwise show it in full.

   If there is no prior user message in the conversation, only show option 1. Then stop and wait for the user's reply. Do NOT invent an example sentence or guess.
3. If the intent is ambiguous, ASK one short clarifying question before rewriting. Otherwise skip straight to the output.
4. Produce one primary correction plus 2–3 short alternatives covering different tones (neutral, concise, formal/casual).
5. Do NOT explain every grammar rule. Only call out a fix if it changes the meaning or the user seems to be learning.

## Output Format

```
**Corrected:** {primary rewrite}

**Alternatives:**
- {alt 1 — different phrasing or tone}
- {alt 2 — shorter or more formal}
- {alt 3 — optional}
```

## Rules

- Preserve the user's original meaning — do not add new information.
- Keep rewrites roughly the same length unless the user asks for shorter/longer.
- Use natural, native-sounding English, not overly formal textbook phrasing.
- If the input is already correct, say so and offer 1–2 stylistic alternatives.
- Never lecture on grammar unless the user asks why.
