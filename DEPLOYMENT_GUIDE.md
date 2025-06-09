# Deployment Guide: GitHub Pages + EmailJS

## Step 1: Deploy to GitHub Pages

### Option A: GitHub Web Interface (Easiest)
1. Go to [github.com](https://github.com) and create a new repository
2. Name it something like `cashiers-house-log`
3. Upload all files from your `/Cashiers` folder
4. Go to Settings > Pages
5. Source: Deploy from a branch
6. Branch: main
7. Your site will be live at: `https://yourusername.github.io/cashiers-house-log`

### Option B: Command Line
```bash
cd /Users/kylemcmillin/Desktop/Cashiers
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/cashiers-house-log.git
git push -u origin main
```

## Step 2: Setup EmailJS

### 1. Create EmailJS Account
- Go to [emailjs.com](https://www.emailjs.com)
- Sign up for free account
- Verify your email

### 2. Add Email Service
- Click "Add New Service"
- Choose Gmail (recommended) or Outlook
- Follow OAuth setup to connect your email
- Note your **Service ID** (e.g., `service_abc123`)

### 3. Create Email Template
- Go to "Email Templates" > "Create New Template"
- Template Name: `Cashiers House Log`
- Use this template:

```
Subject: McMillin Cashiers House - {{type}} Log

Dear McMillin Family,

{{name}} has completed a {{type}} at the Cashiers House.

Details:
• Name: {{name}}
• Time: {{timestamp}}
• Tasks Completed: {{completed_tasks}}/{{total_tasks}}

{{#if checklist}}
Completed Tasks:
• {{checklist}}
{{/if}}

{{#if comments}}
Comments/Notes:
{{comments}}
{{/if}}

This information has been automatically recorded.

Best regards,
McMillin Cashiers House Log System
```

- Set "To Email": Use `{{to_email}}`
- Save template and note your **Template ID** (e.g., `template_xyz789`)

### 4. Get Public Key
- Go to "Account" > "General"
- Copy your **Public Key** (e.g., `user_abc123xyz`)

## Step 3: Update Configuration

Edit `script.js` and replace:
```javascript
EMAILJS: {
    SERVICE_ID: 'your_actual_service_id',      // From step 2.2
    TEMPLATE_ID: 'your_actual_template_id',    // From step 2.3
    PUBLIC_KEY: 'your_actual_public_key'       // From step 2.4
}
```

## Step 4: Test & Deploy

1. **Test Locally**: Open `index.html` in browser, fill out form
2. **Commit Changes**: 
   ```bash
   git add .
   git commit -m "Add EmailJS configuration"
   git push
   ```
3. **Test Live**: Visit your GitHub Pages URL and test email sending

## Troubleshooting

### Email Not Sending?
1. Check browser console for errors
2. Verify EmailJS credentials are correct
3. Make sure Gmail account allows "Less secure apps" if using Gmail
4. Check EmailJS dashboard for usage/errors

### GitHub Pages Not Working?
1. Check repository is public
2. Verify Pages is enabled in Settings
3. Wait 5-10 minutes for deployment
4. Check Actions tab for build errors

## Cost Breakdown
- **GitHub Pages**: Free
- **EmailJS**: Free (200 emails/month)
- **Custom Domain** (optional): ~$10-15/year

Your site will be live at: `https://yourusername.github.io/repository-name`

## Next Steps (Optional)
- Add custom domain
- Set up Google Sheets integration
- Add form validation
- Implement offline support