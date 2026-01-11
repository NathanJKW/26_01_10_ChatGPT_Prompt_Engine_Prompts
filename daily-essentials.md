@pack daily-essentials
@name Daily Essentials

# A small example pack demonstrating all supported variable types.

@template rewrite
@name Rewrite
@description Rewrite text with a chosen tone.
@variables
> The tone to use for rewriting
Tone: select [friendly, professional, concise] required default=friendly
> The text you want rewritten
Text: textarea required
> Include emojis in the rewrite
UseEmojis: boolean default=false

Rewrite the following text in a {{Tone}} tone.

Text:
{{Text}}

Use emojis: {{UseEmojis}}

@template summarize
@name Summarize
@description Summarize content into bullet points.
@variables
> How many bullets to produce
Bullets: text required default=5
> The content to summarize
Content: textarea required

Summarize the following content into {{Bullets}} bullet points:

{{Content}}

@template brainstorm
@name Brainstorm
@description Generate ideas for a topic.
@variables
> The topic you want ideas for
Topic: text required
> Optional constraints (style, audience, format)
Constraints: textarea

Brainstorm ideas for:

Topic: {{Topic}}

Constraints:
{{Constraints}}
