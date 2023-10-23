# MySQL Server Installation

> _Updated 2023 10 22_

This instructions are cited from [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04).

## Package installation

On Ubuntu 22.04, you can install MySQL using the APT package repository. At the time of this writing, the version of MySQL available in the default Ubuntu repository is version 8.0.28.

To install it, update the package index on your server if you’ve not done so recently:

```
sudo apt update
```

Then install the mysql-server package:

```
sudo apt install mysql-server
```

Ensure that the server is running using the systemctl start command:

```
sudo systemctl start mysql.service
```

These commands will install and start MySQL, but will not prompt you to set a password or make any other configuration changes. Because this leaves your installation of MySQL insecure, we will address this next.