# Overview of Email Registrars and Services

When setting up infrastructure for phishing campaigns, choosing the right email service provider is essential. Different email registrars and sending services offer varying features, pricing, and ease of use. Below is an overview of popular options and guidance for setting up Mailgun, the tool we'll use in this course.

## Popular Email Sending Services

- **Mailgun** – A powerful email automation service that allows you to send, receive, and track emails via API. It's widely used for marketing and transactional emails, making it a solid choice for phishing simulations.
- **Amazon SES (Simple Email Service)** – A scalable and cost-effective email sending service designed for developers and businesses. It integrates well with other AWS services.
- **GoDaddy Email** – A more traditional email hosting service, often used for business email accounts. Less API-focused but reliable for basic sending needs.
- **Google SMTP Server** – Allows you to send emails through Gmail or Google Workspace using SMTP. It's familiar and easy to set up but has sending limits that may not suit large campaigns.

There are many other email services available, each with its own strengths. The key is to choose one that fits your technical requirements and campaign goals.

## Why We're Using Mailgun

For this course, we'll use **Mailgun** because it offers:
- A free tier for the first 30 days, ideal for learning and testing.
- Robust API and SMTP support.
- Detailed analytics and tracking features.
- Flexibility to scale up if needed.

### Requirements for Mailgun
To follow along, you'll need:
1. A valid Mailgun account.
2. A credit card to associate with the account (required even for the free tier).

### Important Note on Pricing
Mailgun allows you to send emails for free during the first 30 days. After that period, you'll be charged based on usage. To avoid unexpected charges, remember to disable or delete your Mailgun account.

## Next Steps
1. Go to [Mailgun's website](https://www.mailgun.com) and sign up for an account.
2. Provide the necessary information and link a payment method to your account.
3. Once your account is set up, proceed to the next video, where we'll configure a sending profile and prepare for the hands-on portion of the course.
