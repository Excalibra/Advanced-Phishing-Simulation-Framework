# Configuring GoPhish as a System Service and Accessing the Admin Panel

In this section, we'll walk through the final steps to set up GoPhish as a persistent system service, configure it to listen on all network interfaces, open the necessary firewall ports in AWS, and access the GoPhish admin panel for the first time.

## Step 1: Edit the GoPhish Configuration File

The default GoPhish configuration only allows access from localhost (`127.0.0.1`). To access the admin panel from your local machine, you need to modify the `config.json` file.

1. Navigate to the GoPhish directory:
   ```bash
   cd /home/ubuntu/gophish
   ```

2. Open the configuration file with `nano`:
   ```bash
   nano config.json
   ```

3. Locate the `"listen_url"` field. By default, it is set to `"127.0.0.1:3333"`. Change this to `"0.0.0.0:3333"` to listen on all network interfaces.
   ```json
   "listen_url": "0.0.0.0:3333"
   ```

   <img width="1256" height="549" alt="image" src="https://github.com/user-attachments/assets/4cc626b3-3ce8-46b6-a66d-2b0be54b4c38" />



4. Save the file (`Ctrl+O`, then `Enter`) and exit (`Ctrl+X`).

## Step 2: Create a Systemd Service for GoPhish

To ensure GoPhish starts automatically on system boot, create a systemd service file.

1. Create a new service file:
   ```bash
   sudo nano /etc/systemd/system/gophish.service
   ```

2. Add the following content (you can copy this from the course notes):
   ```ini
   [Unit]
   Description=GoPhish Phishing Server
   After=network.target

   [Service]
   Type=simple
   User=ubuntu
   WorkingDirectory=/home/ubuntu/gophish
   ExecStart=/home/ubuntu/gophish/gophish
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

3. Save and exit the file (`Ctrl+O`, `Ctrl+X`).

## Step 3: Enable and Start the Service

1. Reload systemd to recognize the new service:
   ```bash
   sudo systemctl daemon-reload
   ```

2. Enable the service to start on boot:
   ```bash
   sudo systemctl enable gophish
   ```

3. Start the service:
   ```bash
   sudo systemctl start gophish
   ```

4. Check the status to ensure it's running correctly:
   ```bash
   sudo systemctl status gophish
   ```
   You should see output indicating the service is **active (running)**.

### Retrieve the Auto-Generated Admin Password

The first time GoPhish runs, it generates a random admin password. You can find it in the service logs:

```bash
sudo journalctl -u gophish -n 50
```

Look for a line similar to:
```
Please login with the username admin and the password xxxxxxxx
```

Alternatively, you can temporarily stop the service and run GoPhish manually to generate a new password:
```bash
sudo systemctl stop gophish
sudo ./gophish
```
This will display the admin password in the terminal. After noting it, restart the service with `sudo systemctl start gophish`.

## Step 4: Open Firewall Ports in AWS

To access the GoPhish admin panel from your browser, you need to open port `3333` in the EC2 security group.

1. Go to the **AWS EC2 Console** and select your instance.
2. Click on the **Security** tab.
3. Under **Security groups**, click the security group link (e.g., `launch-wizard-1`).
4. Click **Edit inbound rules**.
5. Add the following rules:
   - **SSH:** Port `22`, Source: `Your IP` (or `0.0.0.0/0` for testing, but restrict it for security).
   - **Custom TCP:** Port `3333`, Source: `Your IP` (or `0.0.0.0/0` if you need access from anywhere).
6. Click **Save rules**.

<img width="1280" height="503" alt="image" src="https://github.com/user-attachments/assets/f846c2c2-a3fa-4d91-9792-82f7d4621b3b" />


## Step 5: Access the GoPhish Admin Panel

1. In your browser, navigate to:
   ```
   http://<your-instance-public-ip>:3333
   ```
   Replace `<your-instance-public-ip>` with the actual public IP address of your EC2 instance.

2. You'll see the GoPhish login page. Use the following credentials:
   - **Username:** `admin`
   - **Password:** The auto-generated password you retrieved earlier.

3. After logging in, you'll be prompted to change the password. Set a new password and save it.

## Step 6: Verify Successful Login

Once logged in, you'll see the GoPhish admin dashboard. From here, you can start creating campaigns, sending emails, and managing your phishing infrastructure.

<img width="1281" height="628" alt="image" src="https://github.com/user-attachments/assets/35eaa7f7-de9d-41af-b278-7d77a9e5b0d3" />


## Next Steps

Now that GoPhish is fully configured and accessible, the next files will cover:

- Setting up domain names and TLS certificates for secure campaigns.
- Creating email templates and landing pages.
- Launching your first phishing campaign.

Stay tuned for the next steps in your phishing engagement journey!
