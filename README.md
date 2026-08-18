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
- `dna/doc/guides/install-guide/install-github-cli-guide.md` — the GitHub
  CLI
- `dna/doc/guides/install-guide/install-flutter-guide.md` — Flutter

The gg specific install guides live in
[dna_gg](https://github.com/ggdna/dna_gg). The overview links to them and
says so; add that layer too if you work with gg.

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
