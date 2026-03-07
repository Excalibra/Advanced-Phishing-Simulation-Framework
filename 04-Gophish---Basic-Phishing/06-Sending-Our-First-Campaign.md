# Launching Your First Phishing Campaign in GoPhish

Congratulations on setting up your GoPhish infrastructure! Now it's time to launch your very first phishing campaign. In this section, we'll walk through creating an email template, setting up a landing page, defining a target group, and launching the campaign. We'll also monitor the results in real-time.

---

## Step 1: Create an Email Template

1. In the GoPhish admin panel, go to **Email Templates** and click **New Template**.
2. **Name:** Enter `Test` (or any descriptive name).
3. Switch to the **HTML** editor for more control.
4. Click the **Source** button to access the HTML editor toolbar.
5. Add some simple text, e.g., `Hello, please click me`.
6. Highlight the text `click me` and click the **Hyperlink** icon.


   <img width="1282" height="659" alt="image" src="https://github.com/user-attachments/assets/be6fa065-87e5-442b-8826-4252b7beff27" />


7. In the dialog box, set the URL to:

   
   ```
   {{.URL}}
   ```

   <img width="1282" height="658" alt="image" src="https://github.com/user-attachments/assets/27398838-ef04-4016-bc87-b13f667ab61c" />


   - This is GoPhish syntax that will automatically generate a unique tracking URL for each recipient.
9. Click **OK** and then **Save Template**.

---

## Step 2: Create a Landing Page

The landing page is where victims will be directed after clicking the link. We'll start with a generic login form.

1. Go to **Landing Pages** and click **New Page**.
2. **Name:** Enter `Test`.
3. In the HTML editor, paste the following basic form code:

   [genericPhishLanding.html](https://github.com/Excalibra/Advanced-Phishing-Simulation-Framework/blob/main/04-Gophish---Basic-Phishing/genericPhishLanding.html)

   ```html
   <html><head></head><body><form class="form-signin" action="" method="POST">
    <br/>
    <div style="text-align: left; font-family: Arial, Helvetica, sans-serif; font-weight: bold;">Username</div>
    <input type="text" name="username" class="form-control top-input" required="" autofocus="" style="text-align: left; width: 420px; height:30px; border-radius: 10px; border-width: 1px; border-color: lightgrey;"/>
    <br/>
    <br/>
    <div style="text-align: left; font-family: Arial, Helvetica, sans-serif; font-weight: bold;">Password</div>
    <input type="password" name="password" class="form-control bottom-input" autocomplete="off" required="" style="text-align: left; width:420px; height:30px; border-radius: 10px; border-width: 1px; border-color: lightgrey;"/>
    <br/>
    <br/>
    <button type="submit" style="border-radius: 10px; width: 80px; background-color: #cfd7f8; height:40px; font-style: bold;">Login</button>
   </form></body></html>
   ```


   <img width="957" height="491" alt="image" src="https://github.com/user-attachments/assets/a96f761f-12cd-4981-9d9b-c7c4ab98eb15" />

   <img width="1284" height="660" alt="image" src="https://github.com/user-attachments/assets/de5132eb-b63a-474c-b397-4419f9b91453" />


3. Click **Preview** to see how the form will look. It will be very basic—this is fine for testing.
4. Check the boxes:
   - **Capture Submitted Data**
   - **Capture Passwords**
5. Set **Redirect to** to `https://google.com` (or any URL where users should go after submitting credentials).
6. Click **Save Page**.

---

## Step 3: Create a User and Group

Before launching a campaign, you need at least one target.

1. Go to **Users & Groups** and click **New Group**.
2. **Name:** Enter `Test Group`.
3. Click **Add** and fill in:
   - **First Name:** `Test`
   - **Last Name:** `User`
   - **Email:** Use a disposable email address (e.g., from [10 Minute Mail](https://10minutemail.com))
   - **Position:** `Security Engineer` (optional)
4. Click **Save Changes**.

<img width="1278" height="656" alt="image" src="https://github.com/user-attachments/assets/6dcf2078-91ff-4dc4-bb5b-89d17d060c3a" />


---

## Step 4: Launch the Campaign

1. Navigate to **Campaigns** and click **New Campaign**.
2. **Name:** Enter `Test Campaign`.
3. **Email Template:** Select `Test`.
4. **Landing Page:** Select `Test`.
5. **URL:** Enter your phishing server's domain (e.g., `https://fishermanisland.com`). This is where the `{{.URL}}` placeholder will point.
6. **Groups:** Select `Test Group`.
7. Leave other settings as default (you can explore scheduling options later).
8. Click **Launch Campaign** and confirm.

---

## Step 5: Monitor Campaign Results

Once the campaign is launched, GoPhish will begin sending emails immediately. You can monitor progress in real-time.

### Check the Target's Inbox

- Open your disposable email inbox. You should see an email from `alerts@fishermanisland.com` with the subject `Test`.
- Open the email and click the **click me** link.

### Observe Events in GoPhish

Back in the GoPhish dashboard, you'll see events populate under the campaign:

- **Email Sent** – The initial event.
- **Email Opened** – When the recipient opens the email (if tracking images are enabled).
- **Clicked Link** – When the recipient clicks the phishing link.
- **Submitted Data** – When credentials are entered on the landing page.

Click the dropdown arrow next to the campaign to expand details. You'll see timestamps for each event.

<img width="1285" height="663" alt="image" src="https://github.com/user-attachments/assets/0bafec79-7157-4320-b6e8-cdb8a669cf81" />


### View Captured Credentials

After the victim submits the form, you can view the captured data:

- In the campaign details, scroll down to the **Submitted Data** section.
- You'll see the username and password entered by the victim.
- Optionally, you can use the **Replay Credentials** feature to automatically submit the captured credentials to a legitimate login page (e.g., if you know the actual login URL).

<img width="1280" height="625" alt="image" src="https://github.com/user-attachments/assets/363245c3-a18e-4e0d-80ef-d906e1061a35" />

<img width="1277" height="629" alt="image" src="https://github.com/user-attachments/assets/34c1271f-e188-42a6-86da-0f6c39909684" />


---

## Example Timeline

1. **Email Sent:** 12:00:00
2. **Email Opened:** 12:01:15
3. **Clicked Link:** 12:01:40
4. **Submitted Data:** 12:02:05

---

## What's Next?

You've successfully launched your first phishing campaign! In the next documents we'll:

- Harden your GoPhish setup to avoid detection.
- Improve email templates and landing pages for realism.
- Add custom email headers to bypass spam filters.
- Explore advanced scheduling and targeting options.

---

## Troubleshooting Tips

- **Email not received?** Check your Mailgun logs to confirm delivery. It may have gone to spam.
- **Link not working?** Verify that your domain resolves correctly and port 443 is open in your security group.
- **Data not captured?** Ensure **Capture Submitted Data** is enabled on the landing page.

Congratulations again—you're now ready to conduct realistic phishing simulations!
