# dna_install

[English](README.md) | Deutsch

Gibt einem Repo die Installations-Guides, die einen Entwicklungsrechner
einrichten, und einen Skill, der meldet, was fehlt.

## Motivation

Ein neuer Entwicklungsrechner braucht dieselben Werkzeuge in derselben
Reihenfolge — Editor, Paketmanager, Node mit pnpm, Azure-Zugang, die GitHub
CLI und Flutter. Diese Schicht bringt diese Reihenfolge in jedes Repo, als eine
Übersicht mit einem Guide pro Werkzeug. Höhere Schichten hängen ihre eigenen
Werkzeuge in dieselbe Übersicht ein, statt eine zweite Liste zu führen:
[dna_gg](https://github.com/ggsuite/dna_gg) ergänzt so die
gg-Installations-Guides.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-install   # TypeScript projects
dart pub add dev:dna_install     # Dart projects
helix init
```

`helix init` legt einen Test ab, der die DNA bei jedem Testlauf instanziiert
und prüft. Er kopiert die Guides nach `doc/guides/` und den Skill nach
`.claude/skills/install/`.

Öffne `doc/guides/install-guide.md` und folge den Guides der Reihe nach, oder
tippe `/install` in Claude Code. Der Skill ruft den Versionsbefehl jedes
Werkzeugs der Übersicht auf, listet die fehlenden mit dem Guide, der sie
installiert, und installiert vor diesem Bericht nichts.

## Guides

- `dna/doc/guides/install-guide.md` — die geordnete Übersicht, hier anfangen
- `dna/doc/guides/install-guide/install-vscode-guide.md` — VS Code und die
  empfohlenen Workspace-Erweiterungen
- `dna/doc/guides/install-guide/install-brew-on-mac-guide.md` — Homebrew, der
  Paketmanager auf dem Mac
- `dna/doc/guides/install-guide/install-node-mac-guide.md` — Node über nvm auf
  dem Mac
- `dna/doc/guides/install-guide/install-node-win-guide.md` — ein altes Node
  entfernen und Node über nvm unter Windows installieren
- `dna/doc/guides/install-guide/install-corepack-guide.md` — corepack und pnpm
- `dna/doc/guides/install-guide/install-azure-cli-guide.md` — die Azure CLI,
  ihre DevOps-Erweiterung und die Anmeldung, für Repos in Azure DevOps
- `dna/doc/guides/install-guide/install-azure-npm-feed-guide.md` — das
  persönliche Zugriffstoken für einen npm-Feed in Azure Artifacts in
  `~/.npmrc`
- `dna/doc/guides/install-guide/install-github-cli-guide.md` — die GitHub CLI,
  die die Workflow-Skripte nutzen
- `dna/doc/guides/install-guide/install-flutter-guide.md` — Flutter, das das
  Dart-SDK mitbringt

## Skills

- `/install` — ruft den Versionsbefehl jedes Werkzeugs der Übersicht auf,
  meldet, was fehlt oder zu alt ist und welche Guides für diesen Rechner nicht
  gelten, und folgt dann den Guides für die fehlenden Werkzeuge, eins nach dem
  anderen; liest den Installations-Guide

## Umfang

Die Schicht deckt nur die Einrichtung des Rechners ab, nicht die eines
einzelnen Repos oder Workspaces. Sie enthält keine gg-spezifischen Guides:
`install-guide/install-gg-guide.md`, auf den der Flutter-Guide verlinkt, und
die Workspace-Einrichtung kommen aus dna_gg. Wer mit gg arbeitet, nimmt auch
diese Schicht dazu.

## Schichten

Die Schicht ist orthogonal: `dna/_dna.json` nennt keine Eltern-Schichten. Sie
trägt nur ihr eigenes Thema und wird vom nutzenden Repo mit anderen Schichten
kombiniert.

Die Übersicht markiert ihren Werkzeug-Abschnitt mit dem Tag `@tooling`
(`## @tooling Tooling`), sodass eine höhere Schicht ihn mit einer
`install-guide.overrides.md` neben dem Guide ersetzen kann. dna_gg tut das: Es
behält die Einträge für die GitHub CLI und Flutter, ergänzt `Install gg` und
hängt einen Abschnitt `Workspace` an.

## Variablen

- `dnaCopyrightHolder` — der Rechteinhaber im Copyright-Kopf jeder abgelegten
  Datei. `mustOverride` in `dna/_dna.json` zwingt jedes Repo und jede Schicht,
  die diese Schicht einbindet, ihn in der eigenen `dna/_vars.json` zu setzen;
  ein Umbrella wie dna_ggdna setzt ihn einmal für seine Organisation
- `dnaAzureDevOpsOrg`, `dnaAzureDevOpsProject` — die Azure-DevOps-Organisation
  und das Projekt, die jeder `az devops`-Befehl als Standard nimmt; auch die
  URL des npm-Feeds enthält sie
- `dnaAzureNpmFeed` — der Feed in Azure Artifacts, aus dem die Pakete kommen

Die drei Azure-Variablen sind nicht erzwungen, ihre Standardwerte sind aber
Platzhalter: Ein Repo, das die Azure-Guides nutzt, setzt sie in seiner eigenen
`dna/_vars.json`.

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das Repo
instanziiert seine eigene DNA — nach Änderungen `dart test` laufen lassen;
vorher committen, denn eine Datei, die die DNA überschreiben würde, darf keine
uncommittete Arbeit enthalten.

Bearbeite die Dateien unter `dna/`, nie ihre Kopien in `doc/` und `.claude/`:
Der Test überschreibt sie.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
