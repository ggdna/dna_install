<!--
@license
Copyright (c) dnaCopyrightHolder

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Install Node on Mac

Make sure [brew is installed](./install-brew-on-mac-guide.md)

## @nvm Install nvm with Homebrew

```bash
brew install nvm
```

## @nvm-directory Create nvm directory (if not created automatically)

```bash
mkdir ~/.nvm
```

## @nvm-shell Add nvm to your shell configuration

Add the following lines to your `~/.zshrc`:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion"
```

## @changes Apply changes

```bash
source ~/.zshrc
```

## @installation Verify installation

```bash
command -v nvm
```

## @node Install node

```bash
nvm install lts
nvm use lts
```
