# Ubuntu 22.04 Guest Additions instructions

This is for Virtual Box
1. Once you have Ubuntu 22.04 installed run this in a terminal
    ```
    sudo apt update
    sudo apt install build-essential linux-headers-$(uname -r) -y
    ```
2. Insert Guest Additions disk by clicking on the Device menu of the VM and select Insert Guest Additions Disk
3. Open a Terminal in Guest Additions Disk and run the following
    ```
    sudo ./VBoxLinuxAdditions.run
    ```
4. Reboot if needed