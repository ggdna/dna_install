# Example

`dna_install` is a DNA layer: it ships the install overview, the install
guides and the `/install` skill, no library code. Declare it as a dev
dependency and instantiate it once:

```bash
dart pub add dev:dna_install    # Dart projects
pnpm add -D @ggdna/dna-install  # TypeScript projects
gg dna init
gg dna build
```

Then open `doc/en/guides/install-guide.md`, or type `/install` in Claude
Code to set up a machine step by step.
