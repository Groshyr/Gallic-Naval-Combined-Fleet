# Commit Conventions

A minimal commit message convention for the **Gallic Naval Combined Fleet** roleplay materials repository. Inspired by [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).

## Format

```text
<type>(<scope>): <description>
```

Both `type` and `scope` are required.

## Types

| Type | Usage |
| --- | --- |
| `add` | Introduce new files or materials. |
| `change` | Edit, replace, rename, or reorganize active files or materials. |
| `archive` | Move outdated or superseded materials into `archive/` rather than deleting them. |

## Scopes

| Scope | Usage |
| --- | --- |
| `lore` | Worldbuilding, history, and roleplay documentation. |
| `media` | Raw and edited images, PSD sources, and other visual assets. |
| `misc` | Other resources and repository-level files or settings. |

The scope identifies the **kind of material**, including when it is being archived. `archive` is a commit type and a directory, not a scope.

## Repository Structure

```text
Gallic-Naval-Combined-Fleet/
├── archive/
├── lore/
├── media/
│   ├── characters/
│   ├── misc/
│   └── psd/
├── misc/
└── COMMIT_CONVENTIONS.md
```

All retired materials go **directly into `archive/`**, regardless of their original category. Do not create category-specific archive subdirectories. Use descriptive, unique filenames to avoid collisions. Git does not track empty folders.

## Rules

1. Write commit messages in English.
2. Use lowercase types and scopes exactly as listed above.
3. Describe the specific material affected; do not repeat the action already expressed by the type.
4. Do not end the subject with a period. Aim for no more than 72 characters.
5. Group related files into one commit; keep unrelated changes separate.
6. For a commit affecting multiple scopes, use the main scope or split the commit if the changes are independent.
7. Move outdated materials directly into `archive/`, without category subdirectories. Keep filenames recognizable and unique.
8. Avoid moving or renaming files whose URLs have been published externally. Archiving such files changes their URLs and may break embedded images. If unavoidable, explain the change in the optional commit body.

A commit body is optional. No semantic versioning, changelog, CI, or automated validation is required.

## AI-Assisted Change Summaries (Optional)

AI assistants may use [OmniDiff](https://github.com/ivankovic/omnidiff) to inspect file changes and draft factual commit summaries.

1. Identify added, modified, and moved files using Git (for example, `git diff --name-status`).
2. For supported files with both old and new versions available, inspect their differences with OmniDiff:

   ```sh
   omnidiff --headless --color never BEFORE AFTER
   # Or use structured output:
   omnidiff --mode json BEFORE AFTER
   ```

3. Summarize only verified changes, then format the commit message according to the types and scopes above. Keep descriptions concise and avoid guessing from filenames alone.
4. For new files, **PSD/PSB projects**, Git LFS pointers, or other unsupported binary formats, use available file details or user-provided notes. Do not claim to have inspected changes that OmniDiff could not analyze.
5. Moving retired materials to `archive/` uses `archive(<scope>)`; OmniDiff is not required to recognize a file move.

OmniDiff provides diffs, **not AI-generated summaries**. AI assistance is optional; no automated commits, CI, or GitHub Actions are required.

## Examples

```text
add(lore): history of gallia
add(media): combined fleet uniform
add(misc): font files

change(lore): fleet command structure
change(media): uniform insignia colors
change(misc): repository description

archive(lore): superseded fleet history
archive(media): obsolete recruitment banner
archive(misc): unused font files
```

Avoid vague messages such as `change(media): files` or `add(misc): stuff`.

**Note:** Archiving does not make materials private. Do not use `archive/` to handle sensitive or unauthorized content; removing such material may require additional steps to address Git history.
