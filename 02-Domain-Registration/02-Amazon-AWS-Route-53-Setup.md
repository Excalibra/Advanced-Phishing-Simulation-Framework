# Registering a Domain with Amazon Route 53

In this section, we'll walk through the process of registering a domain using **Amazon Route 53**. This domain will be used for your phishing campaigns, including sending emails via Mailgun and hosting your phishing pages on an EC2 instance.

---

## Accessing Route 53

1. Log in to your **Amazon AWS Console**.
2. In the services menu, find and click **Route 53** (you can also search for it).
3. You'll primarily be using two AWS services in this course:
   - **EC2** – For hosting your phishing server.
   - **Route 53** – For domain registration and DNS management.

---

## Step 1: Start Domain Registration

1. In the Route 53 dashboard, click **Get Started** under **Domain Registration**.
2. Click **Register a Domain**.

---

## Step 2: Check Domain Availability

1. Enter your desired domain name in the search box (e.g., `FishermanIsland.com`).
2. Click **Check** to see if the domain is available.
3. If available, the price will be displayed (e.g., `$13.00` for `.com`).
4. Click **Select** next to your chosen domain.

---

## Step 3: Configure Domain Settings

1. You'll be taken to the checkout page.
2. **Auto-renew:** For client engagements where the domain is only needed short-term, it's recommended to **turn off auto-renew** to avoid unexpected charges. If you plan to keep the domain long-term, you can leave it on or purchase multiple years upfront for a discount.
3. **Registration Period:** Choose the number of years you want to register the domain (1–10 years). The price will update accordingly.
4. Click **Next** to proceed.

---

## Step 4: Enter Contact Information

1. Fill in your contact details (name, address, email, phone number, etc.).
2. **Privacy Protection:** **Always enable privacy protection** for all contacts. This prevents anyone from looking up your WHOIS records and seeing who registered the domain. It's a critical step to avoid exposing your identity to defenders.
   - Check the box for **Privacy Protection** (it may be labeled as "Hide whois information" or similar).
3. After filling out the form, click **Next**.

---

## Step 5: Review and Submit

1. Review all the details you've entered to ensure accuracy.
2. If everything looks correct, click **Review and Submit** to complete the purchase.
3. You'll need to confirm the order and authorize payment via the credit card linked to your AWS account.

---

## Step 6: Domain Registration in Progress

- After submitting, you'll see a message indicating that domain registration is **in progress**. This can take a few minutes to several hours, depending on the TLD and registry processing times.
- You can monitor the status in the Route 53 dashboard under **Domains > Pending Requests**.

---

## Step 7: Access Your Hosted Zone

Once the domain registration is complete, it will appear in your **Hosted Zones** list. This is where you'll manage DNS records for your domain.

1. In the Route 53 dashboard, click **Hosted Zones** in the left sidebar.
2. You'll see your newly registered domain listed. Click on the domain name to open its configuration page.
3. This is where you'll:
   - Add DNS records (A, CNAME, MX, TXT, etc.) for email setup and traffic routing.
   - Point your domain to your EC2 instance's public IP address.
   - Configure Mailgun-related records (SPF, DKIM, MX).

---

## Key Takeaways

- **Privacy Protection:** Always enable it to hide your identity from WHOIS lookups.
- **Auto-Renew:** Disable it for short-term engagements to avoid unnecessary charges.
- **Hosted Zones:** This is the central location for managing all DNS records for your domain.

---

## Next Steps

With your domain registered, the next step is to configure it for email delivery using **Mailgun**. In the upcoming documents, we'll:

- Set up a Mailgun account.
- Add the necessary DNS records in Route 53.
- Verify domain ownership and configure SMTP credentials.
