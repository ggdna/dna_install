# dna_install

The DNA layer that carries the install guides for a new development
machine.

## Guides

- `dna/doc/guides/install-guide.md` — the ordered overview, start here
- `dna/doc/guides/install-guide/install-vscode-guide.md` — the editor
- `dna/doc/guides/install-guide/install-brew-on-mac-guide.md` — the
  package manager on Mac
- `dna/doc/guides/install-guide/install-node-mac-guide.md`,
  `install-node-win-guide.md` — Node per operating system
- `dna/doc/guides/install-guide/install-corepack-guide.md` — corepack and
  pnpm
- `dna/doc/guides/install-guide/install-azure-cli-guide.md` — the Azure
  CLI, its DevOps extension and the login
- `dna/doc/guides/install-guide/install-azure-npm-feed-guide.md` — the
  personal access token for an Azure Artifacts npm feed
- `dna/doc/guides/install-guide/install-github-cli-guide.md` — the GitHub
  CLI
- `dna/doc/guides/install-guide/install-flutter-guide.md` — Flutter

## Skills

- `/install` — runs the version command of every tool the overview names
  and reports what is missing before installing anything

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo.

The overview marks its tooling section with the tag `@tooling`, so a
higher layer can extend it. [dna_gg](https://github.com/ggdna/dna_gg)
does that to add the gg install guides.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file
- `dnaAzureDevOpsOrg`, `dnaAzureDevOpsProject` — the Azure DevOps
  organization and project the login defaults to
- `dnaAzureNpmFeed` — the Azure Artifacts feed packages come from

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-install   # TypeScript projects
dart pub add dev:dna_install         # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
