# humanizer-ru

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.2.0-blue.svg)](CHANGELOG.md)
[![GitHub stars](https://img.shields.io/github/stars/SergeNS-mne/humanizer-ru?style=social)](https://github.com/SergeNS-mne/humanizer-ru/stargazers)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-5B3FCA)](https://claude.com/claude-code)

> 🇷🇺 [Читать на русском](README.md)

An editorial skill for cleaning up Russian-language LLM output.

The goal is to **bring back the author's voice**, not to "fool the classifier". Editorial approach in the tradition of [Nora Gal](https://en.wikipedia.org/wiki/Nora_Gal) and infostyle. Built on classic Russian editing tradition, not on the arms race against AI detectors.

## What makes it different

Most humanizers operate at the phrase level only — they catch nominalization, stock phrases, calques. Useful but not enough. `humanizer-ru` has three layers:

1. **Phrase layer** — a catalog of 38+ rules against AI markers.
2. **Document layer** — structural diagnostics (listicle signature, dash density, AI-quote ratio, sentence/paragraph length variance).
3. **Voice passport** — a persistent artifact `.humanizer/voice.json` with author preferences that **evolves between sessions**. The skill gets more accurate the more you use it.

Plus **genre presets** (Habr / Telegram / email / vc.ru / LinkedIn / docs) — each describes channel expectations: dash type, formality, listicle allowed, micro-imperfections needed.

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

> OpenCode also scans `~/.claude/skills/` — one clone works for both clients.

## Commands

```
/humanizer-ru                          basic run with last passport or defaults
/humanizer-ru --sample                 calibrate from author's writing sample
/humanizer-ru --interview              calibrate via short interview (no sample)
/humanizer-ru --preset=<name>          use a genre preset (habr/telegram/email/vc/linkedin/docs)
/humanizer-ru --audit                  diagnostics only, no rewriting
/humanizer-ru --rough                  opt-in: allow micro-imperfections (for social media)
/humanizer-ru --reflect <final>        update passport from your final published version
/humanizer-ru --add-sample             append another sample to existing passport
```

## What the skill does NOT do

To be honest: **the skill does not guarantee passing statistical detectors** (GPTZero, Originality.ai, Habr's "НЛО" classifier, RuBERT-based detectors).

The skill works at phrase and document-structure levels and reports problems. The final structural rewriting (breaking listicle, varying paragraph rhythm, replacing AI-quote blocks with inline) requires **the author's editorial decision** — it can't be automated without losing meaning.

Reasoning: classifiers look at the document as a whole (perplexity, burstiness, morphological uniformity). Local phrase-level edits have weak influence on this. The skill provides diagnostics and a checklist; the author handles the rest.

## Pattern categories (38+ total)

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
| **Russian typography** | em-dash / en-dash, guillemets, letter ё — calibrated to author style |
| **Chatbot artifacts** | «Надеюсь, это помогло!» |
| **Structural diagnostics** | listicle signature, dash density, AI-quote ratio, burstiness |

Full catalog and architecture: [SKILL.md](./SKILL.md) (in Russian).

## Example

**Before (AI-sounding Russian):**
> В современном мире, где технологии не стоят на месте, AI-ассистенты являются неотъемлемой частью процесса разработки. Это не просто автокомплит – это раскрытие творческого потенциала в масштабе.

**After (preset `habr`, "ты" address):**
> AI-ассистенты помогают в рутине: шаблонный код, конфиги, тесты-заготовки. Опасность в том, как уверенно выглядят подсказки – легко принять код, который компилируется, но мимо задачи.

## Roadmap

- [x] **v0.1** — initial catalog of 38 patterns
- [x] **v0.2** — three-layer architecture, voice passport, audit mode, genre presets, auto-evolve
- [ ] **v0.3** — extended idiomatic catalog (30+ calques typed), domain whitelists (IT/finance/medicine)
- [ ] **v0.4** — regression examples in `examples/`, CLI utility for passport migration/validation
- [ ] **v0.5** — voice consistency as a metric, diff visualization
- [ ] **v1.0** — stable release, frozen `voice.json` schema

## Credits

Inspired by [blader/humanizer](https://github.com/blader/humanizer) (MIT License) — the original English-language skill, based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).

## Contributing

PRs welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to propose new patterns and submit regression examples.

Found an AI pattern the skill doesn't catch? Open an [issue](https://github.com/SergeNS-mne/humanizer-ru/issues) with a before/after example.

## License

MIT. See [LICENSE](./LICENSE).
