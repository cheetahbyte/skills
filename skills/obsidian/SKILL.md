---
name: obsidian
description: Read, write, and file notes in the Obsidian vault at ~/Documents/brain using its house conventions and Obsidian-flavoured Markdown. Use when the user wants to save, note, log, look up, correct, or reorganise something in the vault, mentions Obsidian, a vault note, or the brain vault, or when creating or editing note content with wikilinks, embeds, callouts, properties, tags, or other Obsidian syntax.
---

# Obsidian

The vault is `~/Documents/brain`. It is a git repository, so edits are recoverable, but search before you write and update the canonical note rather than adding a second one on the same subject.

## Find the target first

1. Search the vault for the subject, its aliases, and distinctive phrases before creating anything.
2. Read the candidate note and its folder before editing.
3. Same question as an existing note: edit that note. Different question: create a focused note and link it from the related one.

Match the vault's existing title language and casing. Do not rename a note unless the user asks or the name breaks the naming rule.

## Where notes go

| Folder | Holds |
|---|---|
| `Inbox/`, `Quicknotes/` | Capture zone for anything not yet classifiable. Not a permanent home. |
| `Knowledge/` | Evergreen notes written from scratch. |
| `Sources/` | Notes about external material: a book, article, talk, video. |
| `People/` | One note per person. |
| `Personal/` | Life admin, subfoldered by domain. |
| `Projects/<Project>/` | Active work: a parent note plus sub-notes. |

## Naming

- Top-level and parent notes: readable phrase, spaces, sentence case. `Kepler.md`, `Developer resource bookmarks.md`.
- Project sub-notes: lowercase hyphenated, no project prefix, because the folder supplies it. `Projects/Kepler/plugin-api.md`.
- Give every project sub-note a vault-unique alias, and link to it from outside its folder by that alias or by full path, never by bare basename. Bare basenames are ambiguous vault-wide.

## Note shape

```markdown
---
aliases:
  - Kepler plugin API
tags:
  - kepler
  - plugins
created: 2026-09-16
updated: 2026-09-16
sources:
  - /Users/leonhardbreuer/Developer/project-hail-kepler/kepler/KeplerPluginHost/JSPluginRunner.swift
---
One sentence saying what this note covers, above the H1.

# Kepler plugin API

## Section

Link to [[Kepler]] inline. Link out with [Obsidian docs](https://help.obsidian.md/).
```

The summary sentence goes between the frontmatter and the H1. Bump `updated` on every substantive edit; never touch `created`. Put the paths or URLs a note was derived from in `sources` so it can be re-verified later.

## Obsidian syntax essentials

- **Wikilinks for vault content**, `[[Note]]` or `[[Note|display text]]`, because Obsidian tracks renames and resolves aliases. Markdown links only for external URLs.
- **Properties only in top-of-file frontmatter**; Obsidian indexes no other block.
- **Embeds use wikilink syntax**, `![[Note]]` or `![[image.png|300]]`. Standard image syntax does not resolve vault targets.
- **Tags are metadata**: prefer the `tags:` list; use inline `#tag` only when it reads naturally in the sentence.
- **Syntax must earn its place.** A link, tag, callout, or embed that does not improve navigation or rendering is noise.

```markdown
> [!info] Title
> Callout content.

> [!warning]- Collapsed by default
> Hidden until expanded.

A ==highlight==, a %%hidden comment%%, and a task:
- [ ] Incomplete
- [x] Done
```

Installed plugins worth using when they fit: dataview, tasks, templater, excalidraw.

## References

- **Conventions** (folders, naming, cross-folder linking, frontmatter fields, note shape): `references/conventions.md`
- **Links & Embeds** (wikilinks, headings, blocks, embeds, query blocks): `references/links-and-embeds.md`
- **Callouts** (types, aliases, collapsible and nested): `references/callouts.md`
- **Properties & Tags** (frontmatter types, YAML rules, tag rules): `references/properties-and-tags.md`
- **Additional Syntax** (highlights, comments, math, footnotes, diagrams, tasks): `references/additional-syntax.md`

## Success criteria

- Searched the vault before creating a note; no duplicate on the same subject.
- Note sits in the most specific folder that fits, and nothing is left in the capture zone whose subject is known.
- Filename follows the naming rule for its position in the vault.
- Frontmatter carries `aliases`, `tags`, `created`, `updated`, `sources`; `updated` reflects this edit.
- Summary sentence sits above the H1; sections are `##`.
- Internal links are wikilinks, external links are Markdown links, cross-folder links use an alias or full path.
