# Additional MFA Considerations in Social Engineering

When discussing multi-factor authentication (MFA) in the context of social engineering, there are several critical considerations to keep in mind. While MFA is a strong security mechanism, it is certainly not infallible. Below, we explore some of the most common and effective tactics used to bypass MFA through social engineering.

## Text Message-Based MFA (SMS)

If a client allows text message-based MFA, this opens up a potential vector for vishing (voice phishing) attacks. For example, after compromising an account, you can trigger the MFA process and then call the user to extract the code.

### Example Scenario:
1. Log into a compromised account.
2. Trigger the SMS-based MFA to send a code to the victim's phone.
3. Call the victim, posing as IT support:
   - *"Hi, I'm from the IT department. We've detected some suspicious activity on your account. You'll receive an MFA code in a few seconds. Can you please provide it so we can verify your account and ensure it hasn't been compromised?"*

This approach works because the request aligns with the victim's immediate experience. They receive the code just as you described, making the attack highly believable. Many people assume that an MFA code cannot be triggered without someone already having control of their account, which adds to the effectiveness of this tactic.

## SIM Swapping Attacks

Another method to bypass SMS-based MFA is SIM swapping. This attack involves tricking a mobile carrier into transferring the victim's phone number to a SIM card controlled by the attacker. Once successful, the attacker receives all SMS messages intended for the victim, including MFA codes. This technique is particularly effective because it exploits vulnerabilities in carrier verification processes rather than directly targeting the user.

## MFA Fatigue Attacks

A more recent and increasingly popular tactic is the MFA fatigue attack (also known as push bombing). This method targets push notification-based MFA, where users must approve an authentication attempt on their mobile device.

### How It Works:
- The attacker triggers multiple MFA push notifications in rapid succession.
- The victim receives a flood of these notifications, often becoming annoyed or confused.
- In many cases, the victim will eventually press "Accept" just to stop the notifications, unaware of the security implications.

This attack relies on the human tendency to seek convenience and avoid frustration. A single click of "Allow" is all it takes for the attacker to gain access.

## Conclusion

While MFA is a robust security measure, these examples demonstrate that it is not immune to social engineering. Techniques like vishing for SMS codes, SIM swapping, and MFA fatigue attacks highlight the importance of user awareness and additional safeguards. As you continue to explore social engineering strategies, keep these methods in mind and consider how they might be applied or mitigated in real-world scenarios.
