# Repository Guidelines

## Project Structure & Module Organization

This repository powers the `sbusso` GitHub profile rather than a deployable application.

- `README.md` is the published profile content.
- `templates/README.md.tpl` contains the readme-scribe template for dynamic contribution and repository lists.
- `github-metrics.svg` is generated profile-metrics output.
- `.github/workflows/readme.yml` regenerates the README; `.github/workflows/metrics.yml` refreshes the metrics image.

Keep new profile content close to the existing section it extends. Treat generated output and its source template as separate concerns, and review workflow effects before changing either.

## Build, Test, and Development Commands

There is no package manifest, local build, or automated test suite. Use lightweight repository checks:

```bash
git diff --check
git diff -- README.md templates/README.md.tpl
git status --short
```

`git diff --check` catches whitespace errors. The scoped diff reviews profile and template changes together, while `git status --short` confirms that generated files were not changed accidentally. Maintainers can manually run `readme.yml` or `metrics.yml` from GitHub Actions to verify generation.

## Coding Style & Naming Conventions

Use concise GitHub-flavored Markdown, ATX headings (`## Heading`), fenced code blocks with language tags, and `-` for unordered lists. Match the existing two-space indentation for nested list items. Keep workflow YAML at two-space indentation and use lowercase `.yml` filenames. Preserve Go-template expressions in `templates/README.md.tpl`, such as `{{range ...}}` and `{{- end}}`.

## Testing Guidelines

Preview Markdown in GitHub or an equivalent renderer. Check that headings remain hierarchical, links resolve, badges and images display, and embedded HTML tables remain balanced. For template edits, verify both the template syntax and the resulting `README.md`; do not hand-edit generated dynamic lists as a substitute for updating their source.

## Commit & Pull Request Guidelines

History uses short, imperative subjects such as `Add stack`, `Revise introduction in README.md`, and `Update readme.yml`. Follow that style and keep each commit focused. Automated metrics commits use their workflow-defined message and should not be imitated manually.

Pull requests should explain the visible profile change, identify any workflow or secret dependency, and include a rendered screenshot when layout, badges, or images change. Confirm that no tokens or generated noise are included.

## Security & Configuration

Never commit values for `PERSONAL_GITHUB_TOKEN`, `GITHUB_TOKEN`, or `METRICS_TOKEN`. Configure them only as GitHub Actions secrets and keep workflow permissions minimal.
