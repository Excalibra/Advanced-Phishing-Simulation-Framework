# Configuring a TLS Certificate for Your GoPhish Server

In this section, we'll secure your GoPhish server with a valid TLS certificate using Let's Encrypt and Certbot. This ensures that your phishing pages are served over HTTPS, displaying the "secure" lock icon in browsers and reducing victim suspicion.

## Why TLS Matters

- By default, GoPhish listens on port **80 (HTTP)**, which browsers mark as "Not Secure."
- A valid TLS certificate (HTTPS) builds trust with victims and avoids security warnings.
- We'll configure GoPhish to listen on port **443 (HTTPS)** and obtain a free certificate from Let's Encrypt.

## Prerequisites

- A domain name pointed to your EC2 instance's public IP address (via an **A record** in Route 53).
- GoPhish installed and running as a system service.
- Port **80** temporarily open in your security group (for initial setup).

---

## Step 1: Verify Domain Resolution

Before obtaining a certificate, ensure your domain resolves to your EC2 instance.

1. In **AWS Route 53**, create an **A record** for your domain (e.g., `fishermanisland.com`) pointing to your EC2 instance's public IP.
2. Wait a few minutes for DNS propagation.
3. Test by visiting `http://fishermanisland.com` — you should see the GoPhish 404 page.

---

## Step 2: Install Certbot

Certbot is the tool we'll use to request a TLS certificate from Let's Encrypt.

```bash
sudo apt update
sudo apt install certbot -y
```

---

## Step 3: Request a Certificate via DNS Challenge

We'll use the **DNS-01 challenge** method, which requires adding a TXT record to your domain's DNS settings.

Run the following command (replace `fishermanisland.com` with your actual domain):

```bash
sudo certbot certonly --manual --preferred-challenges dns -d fishermanisland.com
```

You'll be prompted to:
- Enter an email address for renewal notices.
- Agree to the terms of service.
- Decide whether to share your email with EFF (optional).

Certbot will then display a message like:

```
Please deploy a DNS TXT record under the name:
_acme-challenge.fishermanisland.com
with the following value:
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

**Do not press Enter yet.**

---

## Step 4: Add the TXT Record in Route 53

1. Go to **Route 53** > **Hosted zones** and select your domain.
2. Click **Create record**.
3. **Record name:** Enter `_acme-challenge` (the domain will auto-append).
4. **Record type:** Select **TXT**.
5. **Value:** Paste the long string provided by Certbot.
6. Click **Create records**.

Wait a few minutes for the DNS change to propagate. You can check propagation using tools like [whatsmydns.net](https://whatsmydns.net).

---

## Step 5: Complete the Certificate Request

Once the TXT record is visible globally, return to your terminal and press **Enter**.

Certbot will verify the record and generate your certificate. Upon success, you'll see output similar to:

```
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/fishermanisland.com/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/fishermanisland.com/privkey.pem
```

---

## Step 6: Copy Certificates to the GoPhish Directory

To keep things organized, copy the certificate files into your GoPhish directory.

```bash
cd /home/ubuntu/gophish
sudo cp /etc/letsencrypt/live/fishermanisland.com/fullchain.pem ./mycert_fullchain.pem
sudo cp /etc/letsencrypt/live/fishermanisland.com/privkey.pem ./mycert_privkey.pem
```

Verify the files are present:

```bash
ls -la mycert_*
```

---

## Step 7: Update GoPhish Configuration

Edit the `config.json` file to use the new certificates and enable HTTPS.

```bash
nano config.json
```

Make the following changes:

- **`listen_url`:** Change from `"0.0.0.0:80"` to `"0.0.0.0:443"`.
- **`use_tls`:** Set to `true`.
- **`cert_path`:** Set to `"mycert_fullchain.pem"`.
- **`key_path`:** Set to `"mycert_privkey.pem"`.

Example snippet:

```json
{
  "admin_server": {
    "listen_url": "0.0.0.0:3333",
    "use_tls": true,
    "cert_path": "mycert_fullchain.pem",
    "key_path": "mycert_privkey.pem"
  },
  "phish_server": {
    "listen_url": "0.0.0.0:443",
    "use_tls": true,
    "cert_path": "mycert_fullchain.pem",
    "key_path": "mycert_privkey.pem"
  }
}
```

Save and exit (`Ctrl+O`, `Ctrl+X`).

<img width="1264" height="640" alt="image" src="https://github.com/user-attachments/assets/972b84b7-0c85-432a-ba47-b6c0afb3404d" />


---

## Step 8: Restart GoPhish Service

Restart the service to apply the changes:

```bash
sudo systemctl stop gophish
sudo systemctl start gophish
sudo systemctl status gophish
```

Ensure the status shows **active (running)**.

---

## Step 9: Update AWS Security Group

Now that GoPhish listens on port 443, update your security group rules:

1. Go to **EC2** > **Instances** > select your instance.
2. Click the **Security** tab and open the linked security group.
3. Click **Edit inbound rules**.
4. Replace the temporary port **80** rule with:
   - **Type:** HTTPS
   - **Protocol:** TCP
   - **Port range:** 443
   - **Source:** Your IP (or `0.0.0.0/0` for broader access, but restrict if possible).
5. Click **Save rules**.


<img width="1275" height="533" alt="image" src="https://github.com/user-attachments/assets/226ea88f-169d-48b5-a714-45fd51595a21" />


---

## Step 10: Test HTTPS Access

Open a browser and navigate to:

```
https://fishermanisland.com
```

You should see:
- A **secure lock icon** in the address bar.
- The GoPhish 404 page (or your phishing page if one is active).
- A valid TLS certificate when you click the lock icon.

<img width="1287" height="650" alt="image" src="https://github.com/user-attachments/assets/1a7f3859-b244-4ac7-9a31-f0cdf09e07a6" />


---

## Conclusion

Your GoPhish server is now fully secured with a trusted TLS certificate. Victims visiting your phishing pages will see the green padlock, increasing the perceived legitimacy of your campaign. In the next section, we'll explore how to create convincing email templates and landing pages.

---

*Note: Certificates from Let's Encrypt expire every 90 days. Set up automatic renewal if you plan to run long-term campaigns.*
