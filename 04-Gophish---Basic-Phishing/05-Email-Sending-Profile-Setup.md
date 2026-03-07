# Setting Up Your First Sending Profile in GoPhish

Now that your GoPhish server is secured with a TLS certificate, it's time to configure a **sending profile**. This profile connects GoPhish to your Mailgun account, allowing you to send phishing emails through your domain.

## Accessing the GoPhish Admin Dashboard

You can access the admin dashboard using either:
- Your EC2 instance's public IP address: `https://<your-ip>:3333`
- Your domain name (if you set up the A record): `https://fishermanisland.com:3333`

*Note: You may see a TLS certificate warning when accessing the admin panel. This is because GoPhish uses its default self-signed certificate for the admin interface. You can ignore this warning or replace the certificate in `config.json` (though it's not necessary for functionality).*

---

## Step 1: Create a New Sending Profile

1. In the GoPhish admin panel, navigate to **Sending Profiles** in the left sidebar.
2. Click the **New Profile** button.

### Profile Configuration

Fill in the following fields:

- **Name:** A descriptive name for the profile (e.g., `Alerts Fish Island`).
- **From Email:** The email address you created in Mailgun (e.g., `alerts@fishermanisland.com`).
- **SMTP Host:** `smtp.mailgun.org`
- **SMTP Port:** `587` (GoPhish may not work with port 25, so 587 is recommended).
- **Username:** Your full Mailgun email address (e.g., `alerts@fishermanisland.com`).
- **Password:** The password you saved when creating the SMTP user in Mailgun. If you lost it, you can reset it in the Mailgun dashboard under **Domains > SMTP Credentials**.

---

## Step 2: Test the Sending Profile

Before saving, it's wise to test the configuration to ensure everything works.

1. Click the **Send Test Email** button.
2. Enter a recipient email address. You can use a temporary email service like [10 Minute Mail](https://10minutemail.com) for testing.
3. Click **Send**.

If successful, you'll see a confirmation message: **Email Sent**.

### Verify Delivery

- **Check the recipient inbox:** The test email should arrive shortly. If it doesn't appear, check the spam folder.
- **Check Mailgun Logs:** In your Mailgun dashboard, go to **Sending > Domains**, select your domain, and click **Logs**. You should see an entry for the test email, confirming it was accepted for delivery.

*In my test, the email was received successfully after a short delay.*

---

## Step 3: Save the Profile

Once the test is successful, click **Save Profile**. Your sending profile will now appear in the list and is ready for use in campaigns.

---

## What's Next?

In future videos, we'll harden this sending profile by adding custom email headers to improve deliverability and avoid spam filters. For now, you have a functional setup that can send emails through your domain.

### Recap

- **Sending Profile Name:** Alerts Fish Island
- **From Address:** alerts@fishermanisland.com
- **SMTP Host:** smtp.mailgun.org:587
- **Credentials:** Your Mailgun SMTP username and password

With this profile saved, you're ready to move on to creating email templates and launching your first phishing campaign.
