# Domain Registrar Options for Phishing Campaigns

Before you can launch phishing campaigns, you need a domain name that will host your phishing pages and serve as the sender address for your emails. In this course, we use **Amazon Route 53** as our domain registrar, but there are many other options available. This section provides an overview of popular domain registrars and the requirements for using Route 53.

---

## Popular Domain Registrars

There are countless domain registrars to choose from, each offering similar services and competitive pricing. Here are some of the most widely used options:

- **GoDaddy** – One of the largest and most well-known registrars, offering a wide range of domain extensions and additional services like hosting and email.
- **Namecheap** – Popular for its low prices, free WHOIS privacy, and user-friendly interface.
- **Amazon Route 53** – A scalable and reliable DNS web service from AWS. It integrates seamlessly with other AWS services, making it a great choice if you're already using AWS infrastructure.
- **Register.com** – A long-standing registrar with robust domain management tools and customer support.

### Key Considerations

- **Pricing:** Domain registration costs are generally similar across registrars, but prices can vary for specific TLDs (e.g., .com, .org, .io). Shop around if you're looking for the best deal.
- **Features:** Some registrars include free WHOIS privacy, DNS management, or email forwarding. Evaluate what's included before purchasing.
- **Integration:** If you plan to use other cloud services (like AWS EC2), choosing a registrar that integrates well with those services can simplify setup.

---

## Why We Use Amazon Route 53 in This Course

For this course, we use **Amazon Route 53** because:

- It integrates seamlessly with **Amazon EC2**, where our phishing server is hosted.
- It offers reliable and fast DNS propagation.
- It provides a unified console for managing domains, DNS records, and other AWS resources.

### Requirements for Using Route 53

To follow along with the course, you'll need:

1. **An Amazon AWS Account** – If you don't already have one, you can sign up at [aws.amazon.com](https://aws.amazon.com).
2. **A Payment Method** – You'll need to link a credit card etc. to your AWS account to purchase a domain. Domain prices vary depending on the TLD (e.g., `.com` domains typically cost around $12–$15 per year).

---

## Next Steps

1. If you haven't already, take a moment to create an **Amazon AWS account** and link your payment method.
2. Once your account is set up, you'll be ready to purchase a domain through Route 53 and configure it for your phishing infrastructure.

In the next document, we'll walk through the process of registering a domain in Route 53 and setting up the necessary DNS records.

---

*Note: While we use Route 53 in this course, the concepts and steps are similar across most domain registrars. Feel free to use whichever registrar you're most comfortable with.*
