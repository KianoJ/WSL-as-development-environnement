# Install Node LTS

You need to use [NVM](https://github.com/nvm-sh/nvm) to be able to install Node and use it without `sudo`

```
# Install NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.36.0/install.sh | bash

# Load NVM without restart the terminal
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

# Install the latest Node LTS
nvm install --lts
```
