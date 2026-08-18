# dna_install

The DNA layer that carries the install guides for a new development
machine.

## Content

- `dna/doc/guides/install-guide.md` — the ordered overview, start here
- `dna/doc/guides/install-guide/install-vscode-guide.md` — the editor
- `dna/doc/guides/install-guide/install-brew-on-mac-guide.md` — the
  package manager on Mac
- `dna/doc/guides/install-guide/install-node-mac-guide.md`,
  `dna/doc/guides/install-guide/install-node-win-guide.md` — Node per
  operating system
- `dna/doc/guides/install-guide/install-corepack-guide.md` — corepack and
  pnpm
- `dna/doc/guides/install-guide/install-azure-cli-guide.md` — the Azure
  CLI, its DevOps extension and the login
- `dna/doc/guides/install-guide/install-azure-npm-feed-guide.md` — the
  personal access token for an Azure Artifacts npm feed
- `dna/doc/guides/install-guide/install-github-cli-guide.md` — the GitHub
  CLI
- `dna/doc/guides/install-guide/install-flutter-guide.md` — Flutter

## Extension point

The overview carries one tagged section: `## [@tooling] Tooling`. A higher
layer replaces it through an `install-guide.overrides.md` sidecar next to
the same path and thereby appends its own entries — and, because the
replacement block runs until the next block, whole sections after it.

[dna_gg](https://github.com/ggdna/dna_gg) does exactly that: it repeats the
two base entries (GitHub CLI, Flutter), adds `Install gg` and appends a
`Workspace` section. Add that layer too if you work with gg.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-install   # TypeScript projects
dart pub add dev:dna_install     # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run. This
layer is orthogonal: it carries only its own topic and is combined with
`dna_base` and other layers by the consuming repo.

## Development

This repo has `role: "dna"` in `dna/_dna.json`: the `dna/` folder is
authored by hand, never generated. The repo instantiates its own DNA — run
`dart test` after changes; commit first (a file the DNA would overwrite
must not carry uncommitted work).
