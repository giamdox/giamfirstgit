# CLAUDE.md

## Project Overview

This is a **GitHub Skills** educational template repository that teaches "Introduction to GitHub." It is not a software project — it contains no source code, no build system, and no runtime dependencies. The repository guides learners through fundamental GitHub workflows (branching, committing, pull requests, merging) using automated GitHub Actions that detect user actions and advance through tutorial steps.

## Repository Structure

```
.
├── .github/
│   ├── dependabot.yml              # Dependabot config (monthly GitHub Actions updates)
│   ├── steps/                      # Tutorial step content (Markdown)
│   │   ├── 0-welcome.md
│   │   ├── 1-create-a-branch.md
│   │   ├── 2-commit-a-file.md
│   │   ├── 3-open-a-pull-request.md
│   │   ├── 4-merge-your-pull-request.md
│   │   ├── X-finish.md
│   │   └── -step.txt              # Current step tracker (single digit: 0–4 or X)
│   └── workflows/                  # GitHub Actions workflow files
│       ├── 0-welcome.yml
│       ├── 1-create-a-branch.yml
│       ├── 2-commit-a-file.yml
│       ├── 3-open-a-pull-request.yml
│       └── 4-merge-your-pull-request.yml
├── images/                         # Tutorial screenshots (PNG)
├── .gitignore                      # Ignores compiled binaries, archives, logs, OS files
├── LICENSE                         # MIT License (GitHub, Inc.)
└── README.md                       # Main tutorial page (auto-updated by workflows)
```

## How the Tutorial Works

The repository implements a 5-step interactive tutorial driven entirely by GitHub Actions:

1. **Step 0 — Welcome**: Triggered on repo creation. Updates README to Step 1.
2. **Step 1 — Create a Branch**: User creates `my-first-branch`. Workflow detects `create` event.
3. **Step 2 — Commit a File**: User commits to `my-first-branch`. Workflow detects `push`.
4. **Step 3 — Open a Pull Request**: User opens a PR from `my-first-branch`. Workflow detects `pull_request`.
5. **Step 4 — Merge**: User merges the PR. Workflow detects `push` to `main`.

State is tracked in `.github/steps/-step.txt`. Each workflow checks the current step before executing and uses `skills/action-update-step@v2` to advance.

## Key Conventions

### File Naming
- Workflow files: `{step-number}-{action-name}.yml` (e.g., `1-create-a-branch.yml`)
- Step docs: `{step-number}-{action-name}.md` (e.g., `1-create-a-branch.md`)
- Completion marker: `X-finish.md`

### Markdown Style
- GitHub Flavored Markdown
- `##` headers for main sections
- `> [!NOTE]` callout syntax for tips
- Relative paths for image references (e.g., `images/filename.png`)

### Workflow Style
- Each workflow has a single job named `Autograding`
- All run on `ubuntu-latest`
- Use `actions/checkout@v4` and `skills/action-update-step@v2`
- Authenticate with `secrets.GITHUB_TOKEN`
- Guard execution with step-number checks to prevent out-of-order runs

## Development Notes

- **No build, test, or lint commands** — this is a documentation-only repository.
- **No runtime dependencies** — no `package.json`, `requirements.txt`, or similar.
- **External dependencies** are limited to GitHub Actions: `actions/checkout@v4` and `skills/action-update-step@v2`.
- **Dependabot** is configured to check for GitHub Actions version updates monthly.
- The `.gitignore` covers common compiled artifacts, archives, logs, databases, and OS-generated files.

## Editing Guidelines

- When modifying tutorial content, update the corresponding file in `.github/steps/` and ensure the README stays consistent.
- When modifying workflows, preserve the step-number guard logic and the `skills/action-update-step@v2` call pattern.
- Do not change `.github/steps/-step.txt` manually unless resetting the tutorial.
- Images in `images/` are referenced by the step Markdown files — keep filenames stable.
