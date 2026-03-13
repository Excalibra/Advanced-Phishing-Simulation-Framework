# Advanced Email Template Creation in GoPhish

In this section, we'll explore advanced techniques for creating sophisticated email templates that closely mimic legitimate corporate communications. By leveraging HTML, you can create highly convincing phishing emails that bypass visual inspection.

## Creating an Advanced Email Template

### Step 1: Add a New Template

1. Navigate to **Email Templates** in GoPhish
2. Click "New Template"
3. Name your template (e.g., "Test 2")
4. Set the subject line (e.g., "Encrypted Email")

### Step 2: Import HTML

Copy and paste your pre-built HTML code into the HTML editor. The code for this example:

```html
<html>

<center>
Hi {{.FirstName}},
<br>
<br>
An email from <b>ceo@myco.com</b> requires additional authentication to view.
<br>
<br>
<b>Subject:</b> An Update to your HR Benefits
<br>
<br>
<div style="background-color: #0067b8; width: 275px; height: 60px;"><font color="white"><a href="{{.URL}}" style="text-decoration:none; color:white; text-align:center; padding-top: 20px; display: table-cell;">Click to view the encrypted message</font></a></div>
<br>
<i>Due to your organization's security policy, you may receive encrypted emails when an email contains sensitive data such as Personally Identifiable Information (PII)</i>

<br>
<hr class="solid" /><a>
<br>
My Co<br />
1234 My Co Lane<br />
<b>Office:</b> 111-111-1111 <b>Fax:</b> 111-111-1111 </a>
<br>
</center>
<p><a>{{.Tracker}}</a></p>


</html>
```


### Step 3: Preview Your Template

Use the "Preview" button to see how your email will render when received. The preview shows:

- Personalized fields (e.g., "Hi {{.FirstName}}")
- Formatted content boxes
- Styled buttons
- Corporate letterhead elements

<img width="1278" height="655" alt="image" src="https://github.com/user-attachments/assets/db568733-897f-4d73-8d27-84928b171b50" />


## Understanding the HTML Structure

Let's break down the key components of our example template:

### Basic HTML Framework

```html
<html>
<center>
  <!-- Email content goes here -->
</center>
</html>
```

> **Note:** While the `<center>` tag isn't considered best practice in modern HTML, it's simple and effective for email formatting.

### Personalization Fields

To insert dynamic data from your GoPhish groups:

```
Hi {{.FirstName}}
```

Available fields include:
- `{{.FirstName}}` - Recipient's first name
- `{{.LastName}}` - Recipient's last name  
- `{{.Email}}` - Recipient's email address
- `{{.URL}}` - The generated tracking URL

### Formatting Elements

**Line Breaks:**
```html
<br>
```

**Bold Text:**
```html
<b>CEO at myco.com</b>
```

### Creating Interactive Elements

The button in our example is created using a `<div>` with custom styling:

```html
<div style="background-color: #0067b8; width: 275px; height: 60px;"><font color="white"><a href="{{.URL}}" style="text-decoration:none; color:white; text-align:center; padding-top: 20px; display: table-cell;">Click to view the encrypted message</font></a></div>
```

**Key style properties explained:**
- `background-color`: Sets button color (hex value)
- `width/height`: Defines button dimensions
- `text-decoration: none`: Removes underline from links
- `padding-top`: Centers text vertically within the button
- `display: table-cell`: Enables vertical text alignment

### Additional Formatting

**Italic Text:**
```html
<i>Due to your organization's security policy...</i>
```

**Horizontal Rule (Line):**
```html
<hr class="solid">
```

## Best Practices for HTML Email Templates

1. **Test Responsiveness**: Be cautious with hard-coded dimensions as they may display differently across devices and email clients

2. **Use W3Schools as a Resource**: [W3Schools](https://www.w3schools.com) offers excellent references for HTML and CSS

3. **Mimic Real Emails**: Study legitimate corporate emails from your target organization to replicate their style and formatting

4. **Keep It Simple**: Complex formatting can sometimes trigger security flags; balance sophistication with simplicity

## Development Workflow

For efficient template creation:

1. **Use a Code Editor**: VS Code or similar editors provide syntax highlighting and auto-completion
2. **Preview Locally**: Save your HTML file and open it in a browser to see changes in real-time
3. **Iterate Quickly**: Toggle between your editor and GoPhish, copying and pasting as you refine
4. **Test Thoroughly**: Send test emails to yourself to verify rendering across different email clients

## Key Takeaways

- HTML templates give you complete control over email appearance
- Personalization fields make emails feel authentic to recipients
- Proper formatting (buttons, colors, fonts) increases credibility
- Resources like W3Schools can help you expand your HTML skills
- VS Code or similar editors streamline the development process

By mastering HTML email templates, you can create highly convincing phishing simulations that test your organization's security awareness effectively.
