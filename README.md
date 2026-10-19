# dna_install

English | [Deutsch](README.de.md)

Gives a repo the install guides that set up a development machine, and a skill
that reports what is missing.

## Motivation

A new development machine needs the same tools in the same order — editor,
package manager, Node with pnpm, Azure access, the GitHub CLI and Flutter.
This layer puts that order into every repo as one overview with one guide per
tool. Higher layers hook their own tools into the same overview instead of
keeping a second list: [dna_gg](https://github.com/ggsuite/dna_gg) adds the gg
install guides this way.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-install   # TypeScript projects
dart pub add dev:dna_install     # Dart projects
helix init
```

`helix init` places a test that instantiates and verifies the DNA on every
test run. It copies the guides to `doc/guides/` and the skill to
`.claude/skills/install/`.

Open `doc/guides/install-guide.md` and follow the guides in order, or type
`/install` in Claude Code. The skill runs the version command of every tool
the overview names, lists the missing ones with the guide that installs each,
and installs nothing before that report.

## Guides

- `dna/doc/guides/install-guide.md` — the ordered overview, start here
- `dna/doc/guides/install-guide/install-vscode-guide.md` — VS Code and the
  recommended workspace extensions
- `dna/doc/guides/install-guide/install-brew-on-mac-guide.md` — Homebrew,
  the package manager on Mac
- `dna/doc/guides/install-guide/install-node-mac-guide.md` — Node via nvm on
  Mac
- `dna/doc/guides/install-guide/install-node-win-guide.md` — removing an old
  Node and installing Node via nvm on Windows
- `dna/doc/guides/install-guide/install-corepack-guide.md` — corepack and
  pnpm
- `dna/doc/guides/install-guide/install-azure-cli-guide.md` — the Azure CLI,
  its DevOps extension and the login, for repos in Azure DevOps
- `dna/doc/guides/install-guide/install-azure-npm-feed-guide.md` — the
  personal access token for an Azure Artifacts npm feed in `~/.npmrc`
- `dna/doc/guides/install-guide/install-github-cli-guide.md` — the GitHub
  CLI the workflow scripts use
- `dna/doc/guides/install-guide/install-flutter-guide.md` — Flutter, which
  brings the Dart SDK

## Skills

- `/install` — runs the version command of every tool the overview names,
  reports what is missing or too old and which guides do not apply to this
  machine, then follows the guides for the missing tools one at a time; reads
  the install guide

## Scope

The layer only covers setting up the machine, not a single repo or workspace.
It carries no gg-specific guides: `install-guide/install-gg-guide.md`, which
the Flutter guide links, and the workspace setup come from dna_gg. Add that
layer too if you work with gg.

## Layers

The layer is orthogonal: `dna/_dna.json` lists no parent layers. It carries
only its own topic and is combined with other layers by the consuming repo.

The overview marks its tooling section with the tag `@tooling`
(`## @tooling Tooling`), so a higher layer can replace it with an
`install-guide.overrides.md` next to the guide. dna_gg does that: it keeps the
GitHub CLI and Flutter entries, adds `Install gg` and appends a `Workspace`
section.

## Variables

- `dnaCopyrightHolder` — the holder named in the copyright header of every
  placed file. `mustOverride` in `dna/_dna.json` forces every repo or layer
  that lists this layer to set it in its own `dna/_vars.json`; an umbrella
  such as dna_ggdna sets it once for its organization
- `dnaAzureDevOpsOrg`, `dnaAzureDevOpsProject` — the Azure DevOps
  organization and project every `az devops` command defaults to; the npm
  feed URL contains them too
- `dnaAzureNpmFeed` — the Azure Artifacts feed packages come from

The three Azure variables are not forced, but their defaults are
placeholders: a repo that uses the Azure guides sets them in its own
`dna/_vars.json`.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a file
the DNA would overwrite must not carry uncommitted work.

Edit the files below `dna/`, never their copies in `doc/` and `.claude/`: the
test overwrites them.

## License

MIT — see [LICENSE](LICENSE).
