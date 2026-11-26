<!--
@license
Copyright (c) dnaCopyrightHolder

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Am Azure-npm-Feed anmelden

Führe diese Schritte vor dem ersten `pnpm install` aus und erneut, sobald
das Token abläuft.

## @personal Persönliches Zugriffstoken erstellen <a id="create-a-personal-access-token"></a>

<https://dev.azure.com/dnaAzureDevOpsOrg/_usersSettings/tokens> öffnen

Auf `New Token` klicken

Einen Namen eingeben, der den Rechner erkennbar macht, z. B. `Dell XPS`

Die benötigten Scopes anhaken:

- `Work Items`: `Read`
- `Code`: `Read, write`
- `Build`: `Read`
- `Release`: `Read`
- `Test Management`: `Read`
- `Packaging`: `Read, write`

Auf `Create` klicken

Das Token kopieren. Es wird nur einmal angezeigt.

## @encode Token kodieren <a id="encode-the-token"></a>

Ausführen:

```bash
node -e "require('readline').createInterface({input:process.stdin,output:process.stdout,historySize:0}).question('PAT> ',p => { b64=Buffer.from(p.trim()).toString('base64');console.log(b64);process.exit(); })"
```

Das Token einfügen und `Enter` drücken

Das kodierte Token kopieren. Weil das Token über eine Eingabeaufforderung
gelesen wird, landet es nicht in der Shell-History.

## @token Token in die .npmrc schreiben <a id="write-the-token-into-your-npmrc"></a>

Die Datei öffnen:

```bash
code ~/.npmrc
```

Einen vorhandenen Block für denselben Feed durch den folgenden ersetzen und
das kodierte Token über `[BASE64_ENCODED_PERSONAL_ACCESS_TOKEN]` einfügen:

```npmrc
; begin auth token
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/registry/:username=dnaAzureDevOpsOrg
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/registry/:_password=[BASE64_ENCODED_PERSONAL_ACCESS_TOKEN]
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/registry/:email=npm requires email to be set but doesn't use the value
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/:username=dnaAzureDevOpsOrg
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/:_password=[BASE64_ENCODED_PERSONAL_ACCESS_TOKEN]
//pkgs.dev.azure.com/dnaAzureDevOpsOrg/dnaAzureDevOpsProject/_packaging/dnaAzureNpmFeed/npm/:email=npm requires email to be set but doesn't use the value
; end auth token
```

Die Datei speichern.

Das Token nur in `~/.npmrc` aufbewahren. Niemals in ein Repository
committen.
