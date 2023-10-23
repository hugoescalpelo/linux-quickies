# NodeJS Installation.

> _Updated 2023 10 22_

## Package Installation
A .tar.xz file is provided in [oficial site](https://nodejs.org/en).

## Manual Instalation

This method is cited from [oficial repository](https://github.com/nodesource/distributions).

> _If you have root access, you can omit the 'sudo' command as you already have full administrative privileges._

1. Download and import the Nodesource GPG key

```sh
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
```

2. Create deb repository

```sh
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
```

> ***Optional***: ``NODE_MAJOR`` can be changed depending on the version you need.
>
> ```sh
> NODE_MAJOR=16
> NODE_MAJOR=18
> NODE_MAJOR=20
> NODE_MAJOR=21
> ```

3. Run Update and Install

```sh
sudo apt-get update
sudo apt-get install nodejs -y
```