# Setting Up Mailgun DNS Records with Amazon Route 53

In this section, we'll walk through the process of configuring DNS records in Amazon Route 53 to work with Mailgun. This setup is essential for sending emails through Mailgun using your own domain. Follow along carefully to ensure all records are correctly configured.

## Prerequisites

- A registered domain in Amazon Route 53 (in this example, we use `FishermanIsland.com`).
- A Mailgun account with access to the dashboard.

## Step-by-Step Guide

### 1. Access Mailgun and Add a New Domain

1. Log in to your Mailgun dashboard.
2. Navigate to **Sending** > **Domains**.
3. Click the **Add New Domain** button in the top right corner.
4. Enter your domain name (e.g., `FishermanIsland.com`).
5. Select the domain region (e.g., **US**). If your target audience is in the EU, you may choose the EU region instead.
6. Click **Add Domain**.

Mailgun will now display a list of DNS records that need to be added to your domain's DNS settings.

### 2. Add DNS Records in Amazon Route 53

You'll need to create several records in Route 53 based on the values provided by Mailgun. Below are the specific records to add.


<img width="1199" height="605" alt="image" src="https://github.com/user-attachments/assets/ee8fc561-c409-4fd8-be71-9f681f806057" />


#### **TXT Record (SPF)**
- **Record Type:** TXT
- **Host Name:** `FishermanIsland.com` (leave blank if the domain is automatically appended)
- **Value:** Copy the entire value from Mailgun (e.g., `v=spf1 include:mailgun.org ~all`)

#### **DKIM Record**
- **Record Type:** TXT (or DKIM if available)
- **Host Name:** `smtp._domainkey.FishermanIsland.com` (only enter `smtp._domainkey` if the domain is auto-appended)
- **Value:** Copy the DKIM value from Mailgun

#### **MX Records**
- **Record Type:** MX
- **Host Name:** `FishermanIsland.com` (leave blank if auto-appended)
- **Values:** 
  - `10 mxa.mailgun.org`
  - `10 mxb.mailgun.org`
- **Note:** Both MX records can be added in a single MX record entry by listing them with their priorities.

#### **CNAME Record**
- **Record Type:** CNAME
- **Host Name:** `email.FishermanIsland.com` (only enter `email` if the domain is auto-appended)
- **Value:** `mailgun.org`

### 3. Verify DNS Settings in Mailgun

After adding all records in Route 53, return to Mailgun and click the **Verify DNS Settings** button at the top of the domain page. It may take a few minutes for the DNS changes to propagate. Continue clicking the button until all records are verified and the domain status changes to **Active**.

### 4. Create SMTP Credentials

Once the domain is active, you'll need to create SMTP credentials to send emails.

<img width="1084" height="610" alt="image" src="https://github.com/user-attachments/assets/8b28c6bb-10d1-4255-b07d-78078f0288fb" />


1. In the Mailgun domain settings, go to **SMTP Credentials**.
2. Click **Add New SMTP User**.
3. Enter a username (e.g., `alerts`). This will create an email address like `alerts@FishermanIsland.com`.
4. Click **Create**.
5. **Important:** Save the generated password immediately in a secure location (e.g., a text file or password manager). You'll need it later to configure your phishing tool (e.g., GoPhish).

### 5. Confirm SMTP User Creation

If the new user does not appear immediately, refresh the page. You should see the new SMTP user listed. If you ever need to reset the password, you can use the **Reset Password** option.

## Next Steps

With your domain configured and SMTP credentials ready, you're all set to move on to configuring the sender settings in GoPhish using the email address and password you just created.

---

*Note: DNS propagation can take time. If verification fails initially, wait a few minutes and try again.*
