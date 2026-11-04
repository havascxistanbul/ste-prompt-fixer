# ste-prompt-fixer

An agent skill that fixes sloppy prompts. It rewrites them in controlled-English style (ASD-STE100, ~80% strict) and picks the right output format: plain text, diagram, or single-file HTML.

Inspired by Andrej Karpathy's X post (Oct 2, 2026) on understanding LLM outputs.

## What It Does

You paste a messy, vague, or bloated prompt. This tool rewrites it into one clear prompt, then asks for your approval before you send anything to an LLM.

It does **not** answer the task inside the prompt — it only improves the prompt itself.

## Style Profiles

| Profile | When to use | Key rules |
|---|---|---|
| **ste80** (default) | General-purpose English prompts | Max 15 words/sentence, active voice, no filler |
| **plain** | Public audiences, non-expert readers | Everyday words over jargon, contractions OK |
| **globish** | Multilingual teams, global docs | 1500-word ceiling, no idioms |
| **turkish** (auto for Turkish input) | Turkish docs and customer prompts | Active verbs, kills passive abuse (-dır), keeps tech terms in English |
| **cte** | Procedures, runbooks, migrations | Purpose → prerequisites → steps → verification → rollback |

Turkish-language input automatically selects the `turkish` profile.

## Format Ladder

| Format | When to use |
|---|---|
| **Plain text** (default) | Facts, comparisons, explanations |
| **Mermaid diagram / SVG** | Relations, flows, architectures, dependencies |
| **Single-file HTML** | Dense, explorable content — specs, style guides |

## Structure

```
SKILL.md core flow: intent -> rewrite -> format
profiles/ style packs, one standard per file
ste80.md ASD-STE100, 80% strict (default)
plain-english.md public plain-language style
globish.md 1500-word ceiling, non-native readers
cte-style.md procedure-first service manual style
turkish.md Turkish humanizer + STE hybrid
conventions/ context packs
agents-md.md align prompts with repo AGENTS.md rules
llms-txt.md suggest /llms.txt for site-targeted prompts
lint/ ste-lint.md linter-style rules + regex checks for LLM output
tests/ fixtures.md bad prompt -> fixed prompt seed set (goal: 50)
examples/ before-after.md one fixed prompt per profile
```

The model reads a profile file only when that profile is selected. Keeps context small.

## Examples

### Input (sloppy English)
> "You are a senior dev please explain microservices vs monolith thanks urgent"

### Output (ste80)
```text
Task: Compare microservices vs monolith architectures.

Audience: a team choosing a stack for a new project.

Requirements:
- Provide one table, max 6 rows: latency, deploy speed, debugging, scaling, team size, cost.
- End with a 3-sentence verdict: when to choose each.

Constraints:
- Max 300 words.
- Active voice throughout.
- One sentence, one idea.

Format: plain text
```

### Input (Turkish)
> "Bana REST API nedir anlat çok detaylı olsun lütfen"

### Output (turkish)
```text
Görev: REST API kavramını Türkçe açıkla.

Kitle: yazılımcı adayları ve junior geliştiriciler.

Gereksinimler:
- HTTP metodlarını (GET, POST, PUT, DELETE) madde madde açıkla.
- Her metot için bir örnek URL ver.
- Stateless kavramını 2 cümleyle tanımla.

Kısıtlamalar:
- 400 kelimeyi geçme.
- Teknik terimleri Türkçe çevirme: endpoint, payload, header, status code.
- Her cümle bir fikir olsun.

Format: plain text
```

## Install

Claude Code: copy `SKILL.md` to `~/.claude/skills/prompt-fixer/SKILL.md`.
Cursor: paste the body into `.cursor/rules/prompt-fixer.mdc`.
Any agent following the agentskills.io format: place the folder in its skills path.

## Linting

`lint/ste-lint.md` contains linter-style rules for checking any output against AI-slop, sentence length, passive voice, and more.

## Author

**Mehmet Turac**
- Email: mehmetturac@gmail.com
- GitHub: [mturac](https://github.com/mturac)
- Organization: [havascxistanbul](https://github.com/havascxistanbul)

Built with Cursor Agent (Oct 2026), inspired by Karpathy's post on understanding LLM outputs.

## License

MIT © 2026 Mehmet Turac
