# Whitelisting Considerations for Phishing Campaigns

Before diving into the practical, hands-on portion of the course, it's crucial to address whitelisting. Proper whitelisting ensures your phishing infrastructure can deliver emails and function without being blocked by the client's security controls. This is especially important if you had less than 30 days to set up your domains and infrastructure, as older, more established domains often face fewer restrictions.

## Why Whitelisting Matters

Whitelisting is the process of explicitly allowing specific senders, domains, or IP addresses to bypass security filters. Without it, your phishing emails may be blocked by email gateways, spam filters, or firewalls, potentially derailing your engagement. Working closely with your client to whitelist your infrastructure is essential for a successful campaign.

## Key Areas to Whitelist

Based on common industry practices, here are the most important places to ensure whitelisting:

### 1. Email Gateway
The email gateway is the first line of defense for most organizations. To ensure your emails reach recipients, request whitelisting for:
- **Sender Email Address:** The specific email address used to send phishing emails.
- **Domain:** The domain from which the emails originate.
- **Public IP Address:** The IP address of your email server.

### 2. Spam Filter
Spam filters often use additional criteria to evaluate emails. To prevent your messages from being marked as spam, whitelist:
- **Sender Email Address:** Again, ensure the sender is explicitly allowed.
- **Subject Line:** Some filters may block emails based on specific keywords or patterns in the subject line.

### 3. Domain Whitelisting (Outbound Firewall)
Outbound firewalls may restrict access to certain domains or IP addresses. To ensure victims can reach your phishing site, whitelist:
- **Your Domain Name:** The domain hosting your phishing page.
- **Phishing Server IP Address:** The IP address of your server to prevent it from being blocked mid-engagement.

## Testing Your Whitelisting

Whitelisting is only effective if it works as intended. Before launching your campaign, thorough testing is essential to confirm that everything is functioning correctly.

### Steps for Testing:
1. **Send Test Emails:** Send the phishing email to your client point of contact multiple times to ensure consistent delivery.
2. **Verify Email Content:** Have the client review the email to confirm it looks as intended and isn't being altered by filters.
3. **Test the Link:** Ask the client to click the link in the email and verify it directs to the correct phishing page.
4. **Simulate Data Submission:** Have the client submit fake credentials (e.g., a test username and password) to confirm that your system captures the data correctly.
5. **End-to-End Validation:** Walk through the entire process with the client, from email receipt to data capture, to ensure no step fails.

By rigorously testing with the client, you can identify and resolve any issues before the campaign begins, ensuring a smooth and successful engagement.
