# EmailJS Setup Verification Checklist

## Current Configuration
- **Service ID:** service_mb9b7cd
- **Public Key:** qZvnYlYBa9dPkypTE
- **Template 1 (Notification):** template_ys4974z
- **Template 2 (Auto-reply):** template_0328cm4

## Steps to Verify Setup

### 1. Check Email Service Connection
1. Go to https://dashboard.emailjs.com/admin
2. Click on "Email Services"
3. Verify that `service_mb9b7cd` is listed and shows "Connected"
4. If not connected, click on it and reconnect your email account

### 2. Verify Template 1 (Notification to You)
1. Go to "Email Templates"
2. Find template: `template_ys4974z` (Contact Us)
3. Click to edit and verify:
   - **To Email:** sireeshnasolutions@gmail.com
   - **From Name:** {{from_name}}
   - **Reply To:** {{from_email}}
   - **Subject:** New Contact Form Submission from {{from_name}}
   
4. Check that these variables exist in the template:
   - {{from_name}}
   - {{from_email}}
   - {{phone}}
   - {{service}}
   - {{message}}
   - {{current_date}}

### 3. Verify Template 2 (Auto-Reply to Customer)
1. Find template: `template_0328cm4` (Auto-Reply)
2. Click to edit and verify:
   - **To Email:** {{from_email}}
   - **From Name:** Sirishna Solutions
   - **Reply To:** sireeshnasolutions@gmail.com
   - **Subject:** Thank you for contacting Sirishna Solutions - We'll be in touch soon
   
3. Check that these variables exist in the template:
   - {{from_name}}
   - {{from_email}}
   - {{phone}}
   - {{service}}
   - {{message}}

### 4. Check Public Key
1. Go to "Account" → "General"
2. Verify the Public Key matches: `qZvnYlYBa9dPkypTE`
3. If different, update it in contact.html

### 5. Test Email Service
1. In EmailJS dashboard, go to your email service
2. Click "Send Test Email"
3. If test fails, you need to reconnect your email account

### 6. Common Issues and Solutions

#### Issue: "User not found" or "Service not found"
**Solution:** 
- Verify Service ID is correct
- Make sure the service is active and connected

#### Issue: "Template not found"
**Solution:**
- Check template IDs are exactly correct (case-sensitive)
- Ensure templates are saved and active

#### Issue: "Invalid public key"
**Solution:**
- Copy the public key again from EmailJS dashboard
- Update in contact.html line ~1333

#### Issue: "Email service not connected"
**Solution:**
1. Go to Email Services
2. Click on your service
3. Click "Reconnect" or "Connect"
4. Follow authentication steps for your email provider

#### Issue: Gmail blocking emails
**Solution:**
1. Enable "Less secure app access" in Gmail (if using Gmail)
2. Or use App Password instead of regular password
3. Or switch to a different email service in EmailJS

### 7. Alternative: Use Single Email Template
If you continue having issues, we can simplify to send just one email:

Change the code to send only the notification email:
```javascript
// Send only notification email
emailjs.send('service_mb9b7cd', 'template_ys4974z', templateParams)
    .then(function(response) {
        console.log('Email sent successfully!', response);
        alert('Thank you for contacting us! We will get back to you within 24-48 hours.');
        contactForm.reset();
        submitBtn.disabled = false;
        submitBtn.innerHTML = originalBtnText;
    })
    .catch(function(error) {
        console.error('Email sending failed:', error);
        alert('Oops! Something went wrong. Please try again or contact us directly.');
        submitBtn.disabled = false;
        submitBtn.innerHTML = originalBtnText;
    });
```

### 8. Check Browser Console for Specific Error
Look for error messages that say:
- "The public key is required"
- "Service is not found"
- "Template is not found"
- "Bad request"

This will tell you exactly what's wrong.

## Next Steps
1. Go through each verification step above
2. Note any issues you find
3. Fix them in the EmailJS dashboard
4. Try submitting the form again
5. Check the browser console for the specific error message
