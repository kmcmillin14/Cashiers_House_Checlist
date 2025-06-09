# McMillin Cashiers House - Setup Instructions

## Overview
This system provides a professional logging interface for guest arrivals and departures at the McMillin Cashiers House. The system automatically sends email notifications and stores data in Google Sheets.

## Setup Requirements

### 1. Google Sheets Integration

1. **Create a new Google Sheet:**
   - Go to [Google Sheets](https://sheets.google.com)
   - Create a new spreadsheet
   - Add headers in row 1: `Timestamp | Type | Guest Name | Event Time`

2. **Create Google Apps Script:**
   - In your Google Sheet, go to `Extensions > Apps Script`
   - Replace the default code with:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSheet();
  const data = JSON.parse(e.postData.contents);
  
  sheet.appendRow([
    new Date(),
    data.type,
    data.name,
    new Date(data.timestamp)
  ]);
  
  return ContentService
    .createTextOutput(JSON.stringify({success: true}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. **Deploy the web app:**
   - Click `Deploy > New Deployment`
   - Choose type: `Web app`
   - Execute as: `Me`
   - Who has access: `Anyone`
   - Click `Deploy`
   - Copy the web app URL

4. **Update the configuration:**
   - Open `script.js`
   - Replace `YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE` with your web app URL

### 2. Email Integration

**Option A: EmailJS (Recommended for client-side)**

1. Sign up at [EmailJS](https://www.emailjs.com/)
2. Create an email service
3. Create an email template with variables: `{{name}}`, `{{type}}`, `{{timestamp}}`
4. Update `script.js` to use EmailJS API

**Option B: Custom Backend**

Create a backend service that accepts POST requests and sends emails using services like:
- SendGrid
- Mailgun
- AWS SES
- Nodemailer

### 3. File Structure
```
Cashiers/
├── index.html          # Main application
├── styles.css          # Styling
├── script.js           # JavaScript functionality
└── setup-instructions.md  # This file
```

## Features

- **Dual Forms**: Separate arrival and departure logging
- **Professional Design**: Clean, responsive interface
- **House Instructions**: Built-in reference for opening/closing procedures
- **Email Notifications**: Automatic emails to specified recipients
- **Data Storage**: Google Sheets integration for record keeping
- **Mobile Friendly**: Responsive design works on all devices

## Email Recipients
The system is configured to send notifications to:
- kpm0027@auburn.edu
- eyedr90@aol.com
- idr90@aol.com

## Usage

1. Open `index.html` in a web browser
2. Fill out either the Arrival or Departure form
3. System automatically:
   - Records the entry in Google Sheets
   - Sends email notifications to all recipients
   - Shows confirmation message

## Testing

Before deployment, test the system by:
1. Submitting a test arrival/departure
2. Checking the Google Sheet for the new entry
3. Verifying email notifications are received

## Security Notes

- The Google Apps Script should be deployed with public access for the forms to work
- Consider implementing additional validation if needed
- Monitor the Google Sheet for any unauthorized entries

## Support

For technical issues or modifications, refer to:
- Google Apps Script documentation
- EmailJS documentation
- The console logs in your browser's developer tools