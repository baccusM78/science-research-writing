# Science Research Writing

> A Claude / Codex **skill** that turns Hilary Glasman-Deal's *Science Research Writing* method into a repeatable workflow for drafting, revising, translating, and auditing STEMM research-paper text.
>
> 一个把《科技论文写作》方法论工程化的 Claude / Codex **技能包**：用「逆向工程目标范文 → 先功能后语言 → 主张-证据-边界审核」的流程，帮助（尤其是非英语母语的）研究者起草、修改、翻译、审校 STEMM 论文的各个部分。

---

## What it is / 这是什么

`science-research-writing` is a portable **agent skill**: a `SKILL.md` instruction file plus six reference playbooks that encode a disciplined research-writing process. It is **not** a sentence-polishing macro. It forces the agent to settle *section job, reader, genre, target articles, and claim–evidence–boundary logic* before it touches a single sentence.

它解决一个常见失败模式：把"润色英语"当成论文写作的全部。本 skill 要求 AI 在动笔前先想清楚——**这段文字要完成什么功能、读者是谁、目标体裁与目标期刊是什么、主张是否被证据支撑、边界在哪里**——然后才从功能映射到语言。

## Provenance / 背景与来源

This skill was generated with **OpenAI Codex** from two writing textbooks, using the books as the *method source* (not as copied text):

- **Hilary Glasman-Deal, _Science Research Writing: For Native and Non-Native Speakers of English_, 2nd ed., World Scientific, 2020** (ISBN 978-1-78634-783-1). The core engine — *reverse engineering target articles* and *writing from communicative function to language* — comes from this book.
- A Chinese-language scientific-writing textbook (《英语科技写作（第二版）》) used as a cross-reference for Chinese-author habits.

The skill captures **method, workflow, and checklists** — ideas and procedures — not the books' prose. Anyone using it should obtain the textbooks for the full treatment and worked examples.

> 本 skill 由 Codex 基于上述教材的**方法与流程**生成，不包含教材原文；建议使用者自行获取原书获取完整论述与范例。

## Core method / 核心方法

1. **Reverse-engineer real target articles.** For each section, label what every sentence/paragraph *does* (establishes importance, maps literature, identifies a gap, states method, reports a result, interprets, limits, claims value), then mine language *for those functions* — never collect decorative synonyms.
2. **Write from function to language**, not language to decoration:
   `function → evidence → reader need → sentence/paragraph → language check`.
3. **Treat grammar as meaning.** Tense, voice, article choice, subject choice, prepositions, modal verbs, and citation placement all change the claim.
4. **Audit by claim–evidence–boundary.** Every promised contribution in a title or abstract must be fulfilled by the paper's evidence and conclusion; certainty must match evidence.
5. **Never invent** data, mechanisms, references, novelty, sample sizes, statistics, limitations, or journal norms. If target articles are missing, it produces an explicitly *provisional* model and lists what is needed to localize it.

## What it does / 能力

- **Draft** any section: title, abstract, introduction, methods, results, discussion, conclusion, full outline.
- **Audit** an existing manuscript: risks ranked by reviewer impact, reverse-engineering diagnosis, line/paragraph edits, language-risk checks, next actions.
- **Chinese → English**: rebuild the research logic first, deliver polished English, then concise Chinese notes on structure changes, missing evidence, and high-risk language choices.
- **Title & abstract** specialist checks, including standalone-readability and overpromise detection.

## Repository layout / 目录结构

```
science-research-writing/
├── SKILL.md                                  # entry instructions + mandatory workflow + output formats
├── agents/
│   └── openai.yaml                           # OpenAI/Codex interface metadata
└── references/
    ├── reverse-engineering-workflow.md       # the controlling method (intake → 4-step → audit order)
    ├── section-models.md                     # generic IMRaD models + real writing order
    ├── title-abstract-checks.md              # title 7-checks, abstract model, highlights/graphical abstract
    ├── language-risk-checklist.md            # sentence flow, density, grammar-as-meaning, vocabulary
    ├── chinese-author-workflow.md            # logic-first rebuild for Chinese/translated sources
    └── target-article-analysis-template.md   # how to model a target journal from example papers
```

The agent only opens a reference when the task needs it (mapping table in `SKILL.md`), keeping the working context small.

## Install / 安装

**Claude Code**
```bash
# place the skill directory under your skills folder
cp -r science-research-writing ~/.claude/skills/
```
Then invoke it in a session — e.g. `/science-research-writing` — or just describe a paper-writing task and let the model route to it.

**OpenAI / Codex**
Use `agents/openai.yaml`; the default prompt is
`Use $science-research-writing to reverse-engineer target articles and draft a research-paper section.`

## Usage / 用法

Give the agent: the **genre**, the **target section**, your **evidence** (figures/tables/results), and ideally **3–4 recent target articles** from the journal you want. Without target articles it still works, but marks the model as provisional.

**Default output — drafting:** `Model used` · `Draft` · `Function map` · `Claim-evidence-boundary map` · `Target-article gaps`.

**Default output — auditing:** `Major risks` · `Reverse-engineering diagnosis` · `Line/paragraph edits` · `Language-risk checks` · `Next actions`.

For Chinese input: polished English first, then concise Chinese notes.

## Using it with the `nature-*` skills / 与 nature 技能协同

This skill owns **structure and argument**; the `nature-*` family owns the surrounding pipeline. A natural division of labour:

| Stage | Use |
|---|---|
| Read & model target papers | `nature-reader` → **science-research-writing** (reverse-engineer) |
| Draft / restructure a section | **science-research-writing** |
| Nature-house-style polish, EN↔CN refinement | `nature-polishing`, `nature-writing` |
| Figures, citations | `nature-figure`, `nature-citation` |
| Reviewer response | `nature-response` |

Rule of thumb: **science-research-writing decides what each sentence must do and whether the claim is earned; the `nature-*` skills make it look and read like the target journal.** Run this skill's claim–evidence–boundary audit *last*, after polishing, to catch claims that polishing accidentally strengthened.

## Principles & guardrails / 设计原则与边界

- Function before phrasing; known-information before new.
- Repeat stable technical terms — no thesaurus-hopping.
- Risk-reducing language only when interpretation outruns evidence (never to weaken a well-supported result).
- No fabricated data, references, or journal conventions.
- Target articles are modelled for *function and convention*, never copied as prose.

## Attribution & license / 出处与版权

Method and examples derive from Hilary Glasman-Deal's *Science Research Writing* (2nd ed., World Scientific, 2020) and a Chinese scientific-writing textbook. This repository contains an **independent re-expression of method and workflow**, not the textbooks' text. Please cite and obtain the original books for full study.

Skill files: released for personal and educational use. Add an explicit license (e.g. MIT for the instruction files) if you intend others to reuse them.
