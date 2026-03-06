# Modern Security Architecture: A Social Engineer's Perspective

## From External to Internal: The Inbound Journey

*Note: I apologize for the rapid color change in the diagram. We transitioned from a gray background to pure white, which I'm sure is searing your eyes. The only way I could effectively draw this architecture diagram was using a white background. Hope it doesn't hurt your eyes too much!*

In this section, we'll explore the modern security architecture that social engineers face when conducting phishing campaigns. Understanding this landscape is crucial for both attackers trying to bypass defenses and defenders trying to strengthen them.

### The Inbound Path: Getting to the User's Inbox


<img width="882" height="362" alt="Screenshot 2026-03-06 115113" src="https://github.com/user-attachments/assets/0945d2ca-27c4-444f-a4cb-060751792ee1" />


#### Layer 1: The Firewall
On the left side of our diagram, we have our phishing server—configured with a public IP address and associated domain name. Before any email reaches its target, it must first pass through the organization's firewall, which serves as the initial gatekeeper.

#### Layer 2: Email Gateway
Once through the firewall, email traffic hits the email gateway. This critical component inspects every message entering the organization. Modern email gateways employ multiple techniques:
- **Machine Learning algorithms** to detect anomalous patterns
- **Historical analysis** comparing incoming emails against previous phishing samples
- **Suspicious content detection** that triggers quarantine

If the email gateway deems a message suspicious, it's immediately quarantined—never reaching the user's inbox at all.

#### Layer 3: Spam Filter
The spam filter represents another hurdle. Organizations may use:
- **Custom spam filters** developed internally
- **Generic spam filters** provided by service providers (Microsoft, Google, etc.)

If our email lands here and gets marked as spam, it diverts to the user's spam folder. This significantly reduces the likelihood of the user seeing—and more importantly, clicking—our phishing email.

### The Goal: Landing in the Average Inbox

As social engineers, we must overcome each layer:
- ✅ Bypass the firewall
- ✅ Evade the email gateway
- ✅ Slip through the spam filter
- 🎯 Land in the user's standard inbox

## The Future: Trust Index Architecture

Looking ahead, inbound email inspection is evolving toward what I call a **Trust Index** model. This represents a paradigm shift in how organizations protect their users.

### Current vs. Future Architecture

**Traditional Model:**
```
Email → Gateway → Spam Filter → Inbox → STOP
```

**Future Model (Trust Index):**
```
Email → Gateway → Spam Filter → Inbox → Continuous Mailbox Inspection
                                                       ↓
                                              Trust Index Scoring
```

### How Trust Index Works

Even after an email lands in the mailbox, advanced inspection continues. These mailbox inspectors analyze every single message, asking questions like:

- **"Have I ever received an email from this address before?"**
- **"Have I seen these specific words in context previously?"**
- **"Have I encountered this embedded link before?"**
- **"Is this domain newly registered?"**

Based on these factors, the system builds a trust index score:

| Factor | Positive | Negative |
|--------|----------|----------|
| Known sender | ✓ | |
| Unknown sender | | ✓ |
| Established domain (>30 days) | ✓ | |
| New domain (<30 days) | | ✓ |
| Previously seen link patterns | ✓ | |
| Suspicious keywords | | ✓ |

If the cumulative score falls below a threshold, the email is immediately removed from the user's mailbox—even after delivery.

## The Outbound Journey: What Happens When Users Click

<img width="890" height="340" alt="image" src="https://github.com/user-attachments/assets/cae0a6a4-f1bb-48e2-a592-67e4b833d9d4" />


Now let's examine what happens when a victim clicks our link. They must navigate multiple security layers on the way out to reach our infrastructure.

### The Two Paths: Report vs. Click

#### Path 1: The Sad Face (User Reports the Phish)
```
User → Reports Phish → Security Analyst → Investigation
                                              ↓
                                      Infrastructure Compromised
```

If a user reports our phishing email, it triggers additional security protocols. A security analyst may:
1. Investigate the reported email
2. Examine the linked website
3. Analyze the email headers and content
4. **Compromise our entire operation**

At this point, we must consider our infrastructure burned.

#### Path 2: The Happy Path (User Clicks the Link)
```
User Clicks → Domain Filter Rules → Vendor Filter Rules → Our Website
```

### Outbound Security Layers

#### Layer 1: Domain Filter Rules
Many organizations now implement strict domain filtering. **I recommend defenders implement this immediately:**

- **Domain Age Restrictions**: Block access to domains less than 30 days old
- **Whitelisting**: Only allow traffic to known, trusted domains
- **Blacklisting**: Block known malicious or suspicious domains
- **Categorization Blocks**: Prevent access to domains in高风险 categories

If your phishing domain gets blacklisted or categorized negatively, outbound traffic will be blocked here.

#### Layer 2: Vendor Filter Rules
Major email providers have implemented link inspection:

**Office 365 Safe Links:**
- When users click links, they're redirected through Microsoft's safe links service (e.g., `nam.safeLinks`)
- Each clicked URL is compared against Microsoft's known malicious URL database

**Google Gmail Filter:**
- Similar link inspection before redirection
- Real-time checking against Google's threat intelligence

### Reaching Our Website

After successfully navigating through domain and vendor filters, the victim finally lands on our phishing website. Now they have the opportunity to:
- Enter their password
- Provide MFA codes
- Submit sensitive information

## Post-Click: Credential Harvesting and MFA Challenges

<img width="888" height="350" alt="image" src="https://github.com/user-attachments/assets/9249d414-e82e-4a9d-ab73-073cf27ad416" />

### The Basic Flow (No MFA)

```
Victim submits credentials → Attacker receives → Logs into service provider → Session ID → PROFIT
                      (username/password)          (Google, Office 365, etc.)
```

When victims provide their username and password, we as attackers can immediately:
1. Take those credentials
2. Log into the legitimate service provider
3. Obtain a session ID
4. Achieve our objective (data theft, lateral movement, etc.)

### The MFA Challenge

Multi-factor authentication introduces significant complications:

```
Username/Password → MFA Trigger → User receives alert → Attacker stuck
                                 (push notification, SMS, etc.)
```

When MFA is enabled, we face a barrier. However, social engineering provides an alternative path:

```
Attacker calls user → "Hi, I'm from IT" → "We need your MFA code" → User provides code → Access granted
```

### Why Passwords Alone Are Insufficient

This demonstrates a critical point: **in modern security architecture, having just a username and password is rarely enough**. MFA has become the standard, forcing attackers to develop more sophisticated techniques.

## Modern Solution: MFA Bypass with Evil Ginx

<img width="896" height="264" alt="image" src="https://github.com/user-attachments/assets/d5e30efb-954c-49e6-aa0a-0be88f3e164c" />


### The Evil Ginx Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   User clicks   │────▶│  Filter Rules   │────▶│  Our Phishing   │
│     email       │     │   (if passed)   │     │     Server      │
└─────────────────┘     └─────────────────┘     └────────┬────────┘
                                                          │
                                                          ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   User enters   │◀────│   MFA Prompt    │◀────│  User enters    │
│   MFA Code      │     │   Displayed     │     │  Username/Pass  │
└────────┬────────┘     └─────────────────┘     └─────────────────┘
         │                                                          
         ▼                                                          
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Session       │────▶│  Attacker       │────▶│    Profit!      │
│   Token Sent    │     │  Intercepts     │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

### How Evil Ginx Bypasses MFA

1. **User clicks the email link** and navigates through filtering rules
2. **User enters username and password** on our phishing page
3. **We capture credentials** while simultaneously triggering the legitimate MFA request
4. **MFA prompt appears to user** (seamlessly, in real-time)
5. **User confirms MFA** (push notification, SMS code entry, etc.)
6. **Service provider issues session token** to what the user believes is their device
7. **We intercept the session token** during transmission
8. **We use the session token** to access the service provider
9. **Account compromised**—we now have persistent access

### Key Differentiator

Unlike traditional phishing that only captures credentials, Evil Ginx operates in real-time with the authentication flow:
- The user experiences a normal login sequence
- MFA triggers naturally
- We capture the resulting session token
- No additional social engineering calls required

## Summary: The Complete Attack Surface

```
External → [Firewall] → [Email Gateway] → [Spam Filter] → [Mailbox Inspector (Future)]
    ↓                                                                         ↓
User Inbox → [Domain Filters] → [Vendor Filters] → Our Website
    ↓                                                                         
Credential Entry → MFA Trigger → Session Token Intercept → Account Compromise
```

### Key Takeaways for Social Engineers

1. **Layered defenses** require layered bypass techniques
2. **Future security** will include continuous mailbox inspection
3. **Outbound filtering** is as important as inbound protection
4. **MFA is now standard**—password-only access is rare
5. **Real-time MFA bypass** tools like Evil Ginx represent the evolution of phishing

### Key Takeaways for Defenders

1. **Implement domain age filtering**—block domains <30 days old
2. **Use vendor link protection** (Safe Links, Google Filter)
3. **Enable MFA everywhere**—it significantly raises the bar
4. **Train users** to recognize both phishing and MFA fatigue attacks
5. **Consider trust index models** for future email security

---
