# Phishing Domain Strategy: Best Practices for Social Engineers

## The 30-Day Challenge: Domain Age Matters

When operating within modern security architecture, **domain age is critical**. Here's why:

### Why 30+ Days?

```
Domain Registration Timeline:
Day 0:  [New Domain]    → Blocked by most filters
Day 15: [Still New]     → Still高风险
Day 30: [Established]   → Passes age-based filtering
Day 60: [Trusted]       → Lower suspicion score
```

Many organizations now implement **domain age filtering** as a standard security practice. They simply block access to any domain registered less than 30 days ago. This means:
- Users cannot navigate to your site even if they click your link
- Email gateways may reject messages from new domains outright
- Your entire campaign fails before it begins

### The Ideal Scenario

```
┌─────────────────────────────────────────────────────────────┐
│                   30+ Day Domain Strategy                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Month 1-2:  Host legitimate-looking website                │
│              Build domain reputation                        │
│              Generate normal traffic                         │
│                                                             │
│  Month 3+:   Activate phishing campaign                     │
│              Domain now appears "trusted"                    │
│              Passes age-based filters                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**The ideal approach**: Let your domain "age" for 30-60 days before using it for social engineering. During this period:
- Host legitimate-looking content
- Generate normal traffic patterns
- Build domain reputation naturally
- Avoid any malicious activity that could trigger categorization

## Building Domain Trust

### Make It Look Real

Your domain shouldn't just exist—it should appear legitimate:

| Trust-Building Activity | Purpose |
|------------------------|---------|
| Regular content updates | Shows active management |
| SSL certificate | Establishes security credibility |
| Contact information | Appears professional |
| Privacy policy | Meets legal expectations |
| Normal traffic patterns | Avoids suspicion |

### Avoid Malicious Categorization

Security vendors constantly categorize domains. Once labeled malicious, your domain is effectively burned:

**Common categories that trigger blocking:**
- ❌ Phishing
- ❌ Malware
- ❌ Spam
- ❌ Suspicious
- ❌ Newly Seen (temporary but problematic)

**Safe categories:**
- ✅ Business
- ✅ Technology
- ✅ Education
- ✅ (Generic/Uncategorized)

## Advanced Techniques

### Domain Takeover: The Ultimate Strategy

If you can obtain a domain already owned by your target client:

```
Client-Owned Domain → Already Trusted → No Age Issues → Maximum Credibility
                          ↓
              All internal systems recognize it
                          ↓
              No external reputation checks trigger
                          ↓
                  IDEAL PHISHING VECTOR
```

This is the holy grail of phishing infrastructure. Since the domain belongs to the target organization:
- It passes all age-based filters automatically
- Internal systems inherently trust it
- Users see familiar domain extensions
- Security tools rarely flag internal domains

### Why Business Email Compromise (BEC) Works

BEC attacks bypass nearly all inbound security layers because:

```
Traditional Phishing:                BEC Attack:
[External Domain]                    [Compromised Internal Account]
       ↓                                           ↓
[Firewall]                           [Already Inside]
       ↓                                           ↓
[Email Gateway]                       [No Gateway Inspection]
       ↓                                           ↓
[Spam Filter]                          [No Spam Filter]
       ↓                                           ↓
[User's Inbox]                          [User's Inbox]
       ↓                                           ↓
[External Filters]                     [Internal Trust]
```

**BEC advantages:**
- Emails originate from legitimate internal accounts
- No gateway inspection triggers
- No spam filtering applies
- Users see familiar sender addresses
- Reply-to addresses match the domain
- Conversation threading works normally

This is why BEC attacks have become so prevalent—they bypass almost all technical controls by operating from inside the trust boundary.

## Practical Limitations and Workarounds

### The Reality Check

Let's be honest: maintaining domains for 30-60 days before using them isn't always feasible. You may need to:
- Launch campaigns quickly
- Respond to urgent client needs
- Test specific time-sensitive scenarios

### The Solution: Client Whitelisting

When you can't age domains properly, work closely with your client:

```
┌────────────────── Client Whitelisting Request ──────────────────┐
│                                                                   │
│  Please whitelist the following for our upcoming test:           │
│                                                                   │
│  ☐ Sender Email Address:  campaigns@[your-domain].com           │
│  ☐ Domain:                [your-domain].com                      │
│  ☐ Public IP:             xxx.xxx.xxx.xxx                        │
│  ☐ All URLs:              https://[your-domain].com/*           │
│                                                                   │
│  Duration: [Campaign Start] to [Campaign End]                    │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

### Whitelisting Checklist

Ensure your client configures their email gateway to:

- ✅ **Whitelist sender email address** - Bypasses sender-based filtering
- ✅ **Whitelist domain** - Allows all emails from your domain
- ✅ **Whitelist public IP** - Prevents IP-based blocking
- ✅ **Bypass spam filtering** - Ensures delivery to inbox
- ✅ **Disable link rewriting** - Prevents URL inspection

## Testing: The Critical Step

Never launch a campaign without thorough testing:

### Pre-Campaign Validation

```
Test Flow:
1. Send test email to client contact
2. Verify delivery location (inbox vs. spam vs. quarantine)
3. Click all links in the email
4. Document any filtering blocks encountered
5. Note any link rewriting by vendors
6. Confirm outbound access to your domain
7. Test on multiple devices and email clients
```

### What to Verify

| Check | Expected Result | Actual Result | Fix Needed? |
|-------|-----------------|---------------|-------------|
| Email arrives in inbox | Inbox delivery | | |
| Links work correctly | Direct to your site | | |
| No vendor rewriting | Original URLs intact | | |
| Images load | Full rendering | | |
| Mobile formatting | Responsive display | | |
| Outbound access | Reaches your domain | | |

## Summary: Domain Strategy Checklist

### Pre-Campaign Planning
- [ ] Can we obtain a client-owned domain? (Best option)
- [ ] Can we age a domain for 30+ days? (Second best)
- [ ] Is client whitelisting available? (Practical workaround)
- [ ] Have we tested delivery thoroughly? (Essential)

### Domain Management
- [ ] Domain registered >30 days ago
- [ ] Legitimate content hosted
- [ ] No malicious categorization
- [ ] SSL certificate installed
- [ ] Normal traffic patterns established

### Client Coordination
- [ ] Whitelist request submitted
- [ ] Test contacts identified
- [ ] Testing schedule defined
- [ ] Rollback plan established
- [ ] Success criteria documented

### Testing Protocol
- [ ] Test email sent
- [ ] Inbox delivery confirmed
- [ ] Links functional verified
- [ ] Outbound access confirmed
- [ ] All client systems validated

---

**Key Takeaway**: Domain strategy is often the difference between a successful campaign and one that never reaches its targets. Whether through domain aging, client-owned domains, or proper whitelisting, ensuring your infrastructure appears trustworthy to modern security tools is essential for social engineering success.
