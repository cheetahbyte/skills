# Vault Conventions

> The house style for `~/Documents/brain`: where notes live, what they are called, and how they are shaped.

## Folder taxonomy

| Folder | Holds |
|---|---|
| `Inbox/`, `Quicknotes/` | One capture zone. Anything whose subject is not yet clear. Never a permanent home. |
| `Knowledge/` | Evergreen notes written from scratch: how something works, what was decided, reusable reference. |
| `Sources/` | Notes *about* external material: a book, article, talk, video. One note per source. |
| `People/` | One note per person. |
| `Personal/` | Life admin. Subfolders by domain, such as `Home/`. |
| `Projects/<Project>/` | Active work. One folder per project, containing a parent note plus sub-notes. |

File into the most specific folder that fits. Create a `Projects/` subfolder only when a project needs more than one note; a single-note project can live as one note under `Projects/`.

Capture into the capture zone only when the subject is genuinely unknown. A note that clearly belongs in `Knowledge/` goes straight there.

## Filenames

**Top-level and parent notes** use a readable phrase with spaces, sentence case:

```
Knowledge/Developer resource bookmarks.md
Projects/Kepler/Kepler.md
Personal/Home/Stromverbrauch.md
```

**Project sub-notes** use lowercase hyphenated names with no project prefix, because the folder already supplies it:

```
Projects/Kepler/plugin-api.md
Projects/Kepler/plugin-system.md
Projects/Kepler/release-procedure.md
```

The parent note keeps the project name so it is findable on its own: `Projects/Kepler/Kepler.md`.

## Linking across folders

The vault uses Obsidian's default shortest-path link format, so `[[plugin-api]]` is a bare basename and resolves to the copy in the linking note's own folder. That is correct inside `Projects/Kepler/` and unreliable everywhere else, because a second project can add its own `plugin-api.md`.

- **Inside the project folder:** link by bare name, `[[plugin-api]]`.
- **From anywhere else:** link by alias, `[[Kepler plugin API]]`, or by full path, `[[Projects/Kepler/plugin-api]]`. Never by bare basename.

Every project sub-note therefore carries an alias that is unique vault-wide and reads as a human phrase. That alias is the cross-folder link target.

## Frontmatter

Every note except pure data tables carries:

```yaml
---
aliases:
  - Kepler plugin API
  - Writing a Kepler plugin
tags:
  - kepler
  - plugins
created: 2026-09-16
updated: 2026-09-16
sources:
  - /Users/leonhardbreuer/Developer/project-hail-kepler/kepler/KeplerPluginHost/JSPluginRunner.swift
---
```

| Field | Rule |
|---|---|
| `aliases` | Other names the note should answer to. For a project sub-note, include the vault-unique human phrase used for cross-folder links. Empty list when there are none. |
| `tags` | Lowercase, kebab case. A project tag (`kepler`) plus a topic tag (`plugins`). See `properties-and-tags.md`. |
| `created` | `YYYY-MM-DD`, set once, never edited. |
| `updated` | `YYYY-MM-DD`, bumped on every substantive edit. |
| `sources` | Absolute paths or URLs the note was derived from, so the note can be re-verified against them later. Empty list when the note is original. |
| `cssclasses` | Optional, only when the note needs specific rendering. |

## Note shape

```markdown
---
(frontmatter)
---
One sentence saying what this note covers, above the H1.

# Human readable title

## Section

Prose and lists.

## Section
```

- The summary sentence sits **between the frontmatter and the H1**. It is one sentence, it names the subject, and it is what a reader sees first in a preview.
- The `# H1` is the note's human title, matching the first alias for a hyphenated sub-note.
- Sections are `##`. Use `###` only inside a section that genuinely nests.
- Link related notes inline in prose wherever the link belongs to a sentence.
- A note with siblings may close with a `## Related` section: a list of wikilinks, each followed by a colon and one line saying what that note covers and why you would go there.

```markdown
## Related

- [[plugin-package-format]]: what an npm package and a `.keplugin` bundle must contain.
- [[plugin-api]]: what a plugin author writes in `index.js`.
```

## Writing rules

- Internal references are wikilinks; external references are Markdown links. Never a relative `.md` path.
- Code, paths, and commands go in backticks.
- Prefer a table when the content is a set of parallel facts; prefer prose when it is an explanation.
- Keep a note answering one question. When a section outgrows its note, split it into a sibling and replace it with a link.
