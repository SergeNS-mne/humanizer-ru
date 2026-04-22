# humanizer-ru

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)](CHANGELOG.md)
[![GitHub stars](https://img.shields.io/github/stars/SergeNS-mne/humanizer-ru?style=social)](https://github.com/SergeNS-mne/humanizer-ru/stargazers)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-5B3FCA)](https://claude.com/claude-code)

> 🇷🇺 [Читать на русском](README.md)

A Claude Code skill that removes signs of AI-generated writing from **Russian-language** text.

Russian adaptation of [blader/humanizer](https://github.com/blader/humanizer), redesigned for language-specific patterns that don't exist in English: nominalization (канцелярит), genitive-case chains, "является" as a parasite verb, calques from English, Russian typography, and formal "Вы" by default.

## Why this exists

Modern LLMs (Claude, GPT, Gemini) write Russian in recognizable patterns: long subordinate clauses, abstract nominalization, stock phrases like *"в современном мире, где..."* ("in today's rapidly changing world"), *"не просто X, это Y"* (calque of "it's not just X, it's Y"), and chains of three abstract genitive-case nouns. The text reads as AI even when the facts are correct.

`humanizer-ru` is a catalog of ~38 patterns and rewriting rules that remove these markers and produce more natural Russian prose.

Works in two modes:
- **Basic** – applies rules directly to text.
- **Voice calibration** – analyzes a 2-3 paragraph sample of your own writing and matches your rhythm, vocabulary, and typographic habits (ты vs Вы, dash style, guillemets vs straight quotes, use of ё), instead of producing a "sterile clean" output.

## Installation

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/SergeNS-mne/humanizer-ru.git ~/.claude/skills/humanizer-ru
```

### OpenCode

```bash
mkdir -p ~/.config/opencode/skills
git clone https://github.com/SergeNS-mne/humanizer-ru.git ~/.config/opencode/skills/humanizer-ru
```

> OpenCode also scans `~/.claude/skills/` – one clone works for both clients.

## Usage

### Basic
```
/humanizer-ru

[paste Russian text here]
```

### With voice calibration
```
/humanizer-ru

Sample of my writing:
[2-3 paragraphs you wrote yourself]

Now clean this text:
[AI-generated Russian text]
```

## Pattern categories (~38 total)

| Category | Examples |
|---|---|
| **Nominalization / канцелярит** | «осуществление проверки» → «проверка» |
| **Genitive-case chains** | «улучшение качества обслуживания клиентов компании» → «клиенты стали довольнее» |
| **"Является" as parasite verb** | «является эффективным» → «эффективен» |
| **Era stock phrases** | «в современном мире, где...» → remove |
| **English calques** | «в конце дня», «погрузимся», «меняет игру» (at the end of the day, let's dive in, game-changer) |
| **Rule of three** | «быстро, надёжно и удобно» → specific claim |
| **Negative parallelisms** | «не просто X, это Y» (calque of "it's not just X, it's Y") |
| **Inflated superlatives** | «революционный, уникальный, беспрецедентный» without evidence |
| **Russian typography** | em-dash / en-dash, guillemets, letter ё – calibrated to author style |
| **Chatbot artifacts** | «Надеюсь, это помогло!» |

Full catalog: [SKILL.md](./SKILL.md) (in Russian).

## Example

**Before (AI-sounding Russian):**
> В современном мире, где технологии не стоят на месте, AI-ассистенты являются неотъемлемой частью процесса разработки. Это не просто автокомплит – это раскрытие творческого потенциала в масштабе.

**After (humanized):**
> AI-ассистенты помогают в рутине: шаблонный код, конфиги, тесты-заготовки. Опасность в том, как уверенно выглядят подсказки – легко принять код, который компилируется, но мимо задачи.

## Roadmap

- [x] v0.1 – initial catalog of ~38 patterns
- [ ] v0.2 – real-world text testing, rule refinement
- [ ] v0.3 – channel-specific presets (blog, Telegram, LinkedIn, email, documentation)
- [ ] v0.4 – domain whitelists (IT, finance, medicine terminology)
- [ ] v0.5 – regression examples in `examples/`
- [ ] v1.0 – stable release, frozen API

## Credits

Inspired by [blader/humanizer](https://github.com/blader/humanizer) (MIT License) – the original English-language skill, based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).

## Contributing

PRs welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to propose new patterns and submit regression examples.

Found an AI pattern the skill doesn't catch? Open an [issue](https://github.com/SergeNS-mne/humanizer-ru/issues) with a before/after example.

## License

MIT. See [LICENSE](./LICENSE).
