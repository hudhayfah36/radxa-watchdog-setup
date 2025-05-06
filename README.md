## Step 1: Enable the Watchdog Kernel Module

1. Open the system configuration tool:
    
    ```bash
    rsetup
    ```
    
2. Navigate to **Modify** > **Overlays**.
    
3. Enable the **watchdog** overlay.
    
4. Save changes and exit.
    
5. Reboot the system to apply the changes:
    
    ```bash
    sudo reboot
    ```
    

## Step 2: Install the Watchdog Package

1. Open a terminal.
    
2. Install the Watchdog package:
    
    ```bash
    sudo apt update
    sudo apt install watchdog
    ```
    

## Step 3: Verify the Watchdog Service

1. Check the status of the Watchdog service:
    
    ```bash
    sudo systemctl status watchdog
    ```
    
2. If the service is not running, start it:
    
    ```bash
    sudo systemctl start watchdog
    ```
    
3. To ensure the service starts automatically on boot:
    
    ```bash
    sudo systemctl enable watchdog
    ```
    

## Step 4: Configure the Watchdog Service

1. Open the Watchdog configuration file in a text editor:
    
    ```bash
    sudo nano /etc/watchdog.conf
    ```
    
2. Locate and uncomment the following lines:
    
    ```conf
    watchdog-device = /dev/watchdog
    watchdog-timeout = 30
    interval = 10
    ```
    
3. Save the changes:
    
    - Press Ctrl + O, then Enter to write the file.
        
    - Press Ctrl + X to exit the editor.
        
4. Restart the Watchdog service to apply the configuration:
    
    ```bash
    sudo systemctl restart watchdog
    ```
    

## Step 5: Test the Watchdog Functionality

1. Reboot the system to ensure all changes are applied:
    
    ```bash
    sudo reboot
    ```
    
2. To verify that the Watchdog is functioning correctly, simulate a kernel panic:
    
    ```bash
    echo c | sudo tee /proc/sysrq-trigger
    ```
    
    **Note**: This command will crash the system intentionally, triggering the Watchdog to reboot the system.
    

## Troubleshooting

- If the Watchdog service fails to start, verify that the kernel module is loaded:
    
    ```bash
    lsmod | grep watchdog
    ```
    
- Ensure the Watchdog device (/dev/watchdog) exists and is accessible.
    
- Review the Watchdog service logs for errors:
    
    ```bash
    journalctl -u watchdog
    ```
