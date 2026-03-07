# Reducing Indicators of Compromise (IOCs) in GoPhish

To make your phishing campaigns harder to detect, it's essential to reduce **indicators of compromise (IOCs)** that defenders might recognize. GoPhish has default signatures that can be easily identified by security tools and analysts. In this section, we'll harden your GoPhish server by:

- Removing default binary names and strings.
- Changing HTTP response headers.
- Modifying tracking URL parameters.

---

## Step 1: SSH into Your Phishing Server

Log in to your EC2 instance via SSH:

```bash
ssh -i phishingserver.pem ubuntu@<your-instance-public-ip>
```

---

## Step 2: Navigate to the GoPhish Directory

```bash
cd /home/ubuntu/gophish
```

---

## Step 3: Remove GoPhish Binary Signatures

GoPhish binaries contain identifiable strings like `gophish` that can be detected by defenders. We'll replace these with generic terms.

### Replace `gophish` with Custom Names

Run the following commands to replace occurrences of `gophish` in the binary:

```bash
find . -type f -exec sed -i 's/gophish/customname/g' {} +
find . -type f -exec sed -i 's/GoPhish/CustomName/g' {} +
```

<img width="958" height="241" alt="image" src="https://github.com/user-attachments/assets/dac0c8ab-60af-4f8c-b052-5ed8644193c4" />


*Note: You may see "permission denied" errors for certificate files—this is normal and safe to ignore.*


<img width="957" height="335" alt="image" src="https://github.com/user-attachments/assets/68dd4a18-879f-4326-9cb9-5c892f16537e" />

---

## Step 4: Change the Server Header

By default, GoPhish responds with a `Server: gophish` header in HTTP responses. This is a clear IOC. We'll change it to something generic like `Apache` or `nginx`.

1. Navigate to the `config` directory:
   ```bash
   cd /home/ubuntu/gophish/config
   ```

2. Open `config.go` in a text editor:
   ```bash
   nano config.go
   ```

3. Scroll down until you find the line:
   ```go
   ServerName = "gophish"
   ```

   <img width="959" height="511" alt="image" src="https://github.com/user-attachments/assets/a36d95ad-b0bb-42e1-a482-45c551acf592" />


5. Change it to something generic, e.g.:
   ```go
   ServerName = "Apache"
   ```

6. Save the file (`Ctrl+O`, `Enter`, `Ctrl+X`).

---

## Step 5: Change the Tracking URL Parameter

GoPhish uses a default parameter `rid` in tracking URLs (e.g., `?rid=12345`). This is another well-known IOC. You can change it to anything you like.

<img width="1918" height="574" alt="image" src="https://github.com/user-attachments/assets/b96d8a17-70a0-40a0-9b40-d31cafd0fe45" />


1. Return to the main GoPhish directory:
   ```bash
   cd /home/ubuntu/gophish
   ```

2. Run the following command to replace all instances of `rid` with a custom parameter (e.g., `identifier`):
   ```bash
   sed -i 's/const RecipientParameter = "rid"/const RecipientPrameter = "identifier"/g' models/campaign.go
   ```

   You can replace `identifier` with any word you choose (e.g., `token`, `id`, `user`, `auth`).

---

## Step 6: Restart the GoPhish Service

1. Stop the service:
   ```bash
   sudo systemctl stop gophish.service
   ```

2. Start the service:
   ```bash
   sudo systemctl start gophish.service
   ```

3. Check the status to ensure it's running:
   ```bash
   sudo systemctl status gophish.service
   ```

---

## Step 7: Rebuild the GoPhish Binary

After making these changes, you need to rebuild the GoPhish binary for them to take effect.

```bash
go build
```

This will create a new `gophish` executable with all your customizations.

---

## Step 8: Verify the Changes

### Test the Server Header

Use `curl` to check the HTTP response headers:

```bash
curl -I https://fishermanisland.com
```

Look for the `Server:` header. It should now show your custom value (e.g., `Apache`).

### Test the Tracking Parameter

1. Send yourself a test email using GoPhish (as shown in previous lessons).
2. In the received email, click the link and observe the URL parameter. It should now use your custom name (e.g., `?identifier=12345`) instead of `rid`.

---

## Example: Customizing the Parameter Further

If you want to change the parameter again in the future, simply rerun the `sed` command with a new value:

```bash
find . -type f -exec sed -i 's/identifier/newparam/g' {} +
```

Then rebuild and restart the service.

---

## Troubleshooting

If you encounter errors after modifying the binary (e.g., `libc` errors), try rebuilding GoPhish:

```bash
cd /home/ubuntu/gophish
go build
sudo systemctl restart gophish.service
```

This often resolves issues caused by incomplete binary patching.

---

## Why These Changes Matter

- **Binary Signatures:** Defenders often scan for known GoPhish strings in binaries and memory.
- **Server Headers:** HTTP response headers are easily inspected; changing them blends your server in with legitimate web servers.
- **URL Parameters:** Security tools may flag URLs containing `rid` as malicious. Customizing this parameter helps evade detection.

By implementing these changes, you significantly reduce the likelihood of your phishing infrastructure being identified by automated scanners and manual analysis.

---

## Next Steps

With your server hardened, you're ready to create more sophisticated campaigns. In the next documents, we'll explore:

- Creating realistic email templates.
- Cloning legitimate login pages.
- Advanced targeting and scheduling.
