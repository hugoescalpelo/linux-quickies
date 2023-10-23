# Visual Studio Code Installation

> _Updated 2023 10 22_

This instructions are provided from [Microsoft Site](https://code.visualstudio.com/docs/setup/linux).

1. Download Visual Studio Code from [official site](https://code.visualstudio.com/Download).
2. Open a terminal where downloaded .deb file is.
3. Run the installation command.
```
sudo apt install ./<file>.deb
```

## Alternative Installation method

### Manual Instalation

```
sudo apt-get install wget gpg

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg

sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

rm -f packages.microsoft.gpg

sudo apt install apt-transport-https

sudo apt update

sudo apt install code # or code-insiders
```
### Snap Installation

```
sudo snap install --classic code # or code-insiders
```

Or install from Ubuntu Software App.