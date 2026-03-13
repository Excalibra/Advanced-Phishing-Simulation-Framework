# Hardening Sender Email Configuration

Now that we've hardened our server, we can also harden our sender email configuration to improve deliverability and avoid detection by security solutions.

## Modifying Email Headers

When you send emails through GoPhish, default headers are automatically added that can reveal the source of the email or trigger security flags. By modifying these headers, we can make our phishing emails appear more legitimate.

### Step-by-Step Process

1. **Navigate to Sending Profiles**
   - Log into your GoPhish server
   - Go to "Sending Profiles" in the navigation menu
  
     <img width="960" height="474" alt="image" src="https://github.com/user-attachments/assets/09f722c9-db7c-4528-a042-151d0e203a46" />


   - Click "Edit" on your existing sending profile (e.g., "alerts Fish Island")
  

2. **Add Custom Headers**
   
   In the "Headers" section, add the following custom headers with the value set to "ignore" for each:

   ```
   Header Name: MIME-Version
   Value: ignore
   ```

   ```
   Header Name: Received
   Value: ignore
   ```

   ```
   Header Name: X-Mailer
   Value: ignore
   ```

   ```
   Header Name: X-Originating-IP
   Value: ignore
   ```

     <img width="957" height="473" alt="image" src="https://github.com/user-attachments/assets/764ee72e-9790-4eb6-989b-549f07ac4ff3" />
     
   > **Note:** These exact header names and values will also be provided in the course notes for easy reference.

## Why This Matters

Adding these custom headers helps:
- Remove default GoPhish headers that could identify the email source
- Conceal metadata that security solutions might flag
- Improve email deliverability to targets
- Reduce the likelihood of emails being blocked

## Best Practice

**Always add these headers for every sending profile you create.** Making this a standard part of your sending profile configuration will help harden your email infrastructure against detection and blocking.
