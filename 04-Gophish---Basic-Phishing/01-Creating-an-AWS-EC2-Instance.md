# Setting Up an Amazon EC2 Instance for Your Phishing Server

In this section, we'll walk through the process of creating an Amazon EC2 instance that will host your phishing server (GoPhish). This step-by-step guide covers instance creation, key pair setup, and initial SSH access.

## Step 1: Launch an EC2 Instance

1. Log in to your **Amazon AWS Console**.
2. Click on **Services** in the top navigation bar.
3. Find and select **EC2** (right-click to open in a new tab for easy reference).
4. Click the orange **Launch Instance** button.

<img width="1203" height="605" alt="image" src="https://github.com/user-attachments/assets/6be24028-c26f-4f96-9cf6-c11622caa181" />

<img width="1178" height="601" alt="image" src="https://github.com/user-attachments/assets/3b4c677a-cd7f-43a0-944e-eeb1f1d18287" />


### Instance Configuration

- **Name:** Enter a recognizable name, e.g., `Phishing Server 1`.
- **OS Image:** Select **Ubuntu** (the default version is fine).
- **Instance Type:** Choose **t2.micro** (this is sufficient for GoPhish and falls within the free tier).

### Key Pair Setup

1. Under **Key pair (login)**, click **Create new key pair**.
2. **Key pair name:** Enter `PhishingServer-PEM` (or any name you prefer).
3. Click **Create key pair**.
4. The `.pem` file will automatically download. **Save this file securely**—you'll need it to SSH into your server.

<img width="1200" height="606" alt="image" src="https://github.com/user-attachments/assets/a12f8913-3c48-4b83-83db-db3c06a1cf69" />

<img width="1270" height="318" alt="image" src="https://github.com/user-attachments/assets/71895954-c47d-4b10-9578-99de522a027f" />


### Network Settings

- For now, allow **SSH traffic from anywhere** to simplify setup. However, for production or real engagements, you should restrict this to your specific IP address.
  - To do this, select **My IP** from the dropdown instead of **Anywhere**.

### Launch Instance

- Review your settings and click **Launch Instance**.
- You'll see a success message confirming that your instance has been launched.

## Step 2: Connect to Your EC2 Instance via SSH

Once the instance is running, you'll need to connect to it using the `.pem` key pair you downloaded.

### Find Your Instance's Public IP Address

1. In the EC2 dashboard, click **Instances** in the left sidebar.
2. Locate your newly created instance and copy its **Public IPv4 address**.

### Open a Terminal (Command Prompt)

1. Open your terminal (Command Prompt, PowerShell, or any terminal emulator).
2. Navigate to the directory where your `.pem` file is saved. For example:
   ```bash
   cd ~/Downloads
   ```
3. Run the following SSH command to connect:
   ```bash
   ssh -i phishingserver.pem ubuntu@<your-instance-public-ip>
   ```
   Replace `<your-instance-public-ip>` with the actual IP address you copied.

### Accept the Connection

- The first time you connect, you'll see a prompt asking if you're sure you want to continue connecting. Type `yes` and press Enter.

### Verify the Connection

- Once logged in, you can verify your user by running:
  ```bash
  whoami
  ```
  The output should be `ubuntu`, confirming you're successfully connected to your EC2 instance.

<img width="736" height="385" alt="image" src="https://github.com/user-attachments/assets/a33be03d-0ec0-4423-9b53-fb13457fd2ec" />


## Next Steps

Now that your EC2 instance is set up and you have SSH access, the next series of videos will cover:

- Installing and configuring **GoPhish** on your Ubuntu instance.
- Additional security configurations within AWS to protect your phishing server.
