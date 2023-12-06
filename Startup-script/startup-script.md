# Startup Script
A common task for Linux systems, for example, Raspberry Pi, is to run a program at startup. This guide explains a simple way to do that.

## Instructions
### Step 1: Create your Python script

First, create a script that you want to run at startup. Let's assume your script is named my_script.py and it's located in the `/home/pi/` directory.

### Step 2: Create a systemd service file

Next, you need to create a systemd service file that tells the Raspberry Pi to run your Python script at startup. Open a terminal and use the following command to create a new service file:

```
sudo nano /etc/systemd/system/my_script.service
````

Replace my_script with a suitable name for your service. In the text editor, add the following content:

```
[Unit]
Description=My Python Script

[Service]
ExecStart=/usr/bin/python3 /home/pi/my_script.py
WorkingDirectory=/home/pi
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

Make sure to replace /usr/bin/python3 with the correct path to your Python interpreter if it's different. For different programs, put the route to the executer. Also, ensure that the ExecStart path matches the location of your Python script.

### Step 3: Save and exit

Save the file by pressing `Ctrl + O`, then press Enter. Exit the text editor by pressing `Ctrl + X`.

### Step 4: Enable and start the service

Now, you need to enable the service and start it. Use the following commands:

```
sudo systemctl enable my_script.service
sudo systemctl start my_script.service
```

This will enable the service to start at boot and also start it immediately without having to reboot.

### Step 5: Check the status

You can check the status of your service to ensure it's running without errors using the following command:

```
sudo systemctl status my_script.service
```

If everything is set up correctly, you should see that the service is active and running.

Your Python script should now run automatically at startup on your Raspberry Pi. Make sure to replace my_script.py and other paths with the appropriate names and locations according to your setup.

## Service Example
If the locaation of your script is different than `home` folder, make routes match as shown.

```
[Unit]
Description=My Python Script

[Service]
ExecStart=/usr/bin/python3 /home/user/Documents/GitHub/repo-name/python/script-name.py
WorkingDirectory=/home/user/Documents/GitHub/repo-name/python/
Restart=always
User=user

[Install]
WantedBy=multi-user.target
```
Then run the following.
```
sudo systemctl enable my_script.service
sudo systemctl start my_script.service
```

## Troubleshooting

If you get the following error:

`The unit file, source configuration file or drop-ins of deseos.service changed on disk. Run 'systemctl daemon-reload' to reload units.`

Try this:

```
sudo systemctl daemon-reload
sudo systemctl start my_script.service
```