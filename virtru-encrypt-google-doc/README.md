# Protect & Share Google Docs with the Virtru SDK
An add-on for Google Docs adding the ability to encrypt & download or encrypt & email the contents of the document as an encrypted PDF, protected by Virtru.  Written in Google Apps Script leveraging the [Virtru SDK](https://developer.virtru.com).  

![](https://miro.medium.com/max/1280/1*Bw1zo_S0C-M9ambD7s1pRg.gif)

## Setup
This is a self-contained project, so you can simply copy & paste the contents of each file into a new Google Apps Script project.  Make sure to keep the same file names, as these are referenced within the code.  Alternatively, download the full project, edit locally, and push to Google Apps Script with [Clasp](https://developers.google.com/apps-script/guides/clasp).

This project follows [Google Apps Script HTML Service best practices](https://developers.google.com/apps-script/guides/html/best-practices) and externalizes client-side JS and CSS into their own files.  

The included files are:
- [Code.gs](./Code.gs)
  - Server-side code written in Google Apps Script.
- [virtruSidebar.html](./virtruSidebar.html)
  - Main client-side code.  Generates the sidebar and provides a container for all client-side functions.
- [JavaScript.html](./JavaScript.html)
  - Client-side JavaScript.  Is imported into and runs in the contenxt of virtruSidebar.html.
- [Stylesheet.html](./Stylesheet.html)
  - Styling for client-side code.
- [emailHTML.html](./emailHTML.html)
  - Provides the template for the email generated via the Encrypt & Email workflow.
- [appsscript.json](./appsscript.json)
  - Manifest file.
  
Once code has been copied into a new project, hit Run > Test as Add-On to test.
  
## Usage
Once deployed (or while testing) a new "Virtru Google Doc Protect & Share" option will be made available under the "Add-Ons" menu while viewing a Google Doc.  Selecting this option then "Start" will open the new Virtru sidebar.

### Select a Sharing Option
Users can select either of two functions:
- **Encrypt & Download**  
  - Generates an encrypted PDF (pdf.tdf3.html) and downloads to the user's machine.
- **Encrypt & Email**  
  - Generates an email to authorized recipients.  The encrypted PDF (pdf.tdf3.html) is included as an attachment. 

### Add Authorized Users
Users can add the email addresses (comma-separated) of other individuals with whom they'd like to share this file.  These identities will be added as authorized users on the access control policy.  Optional for "Download" function; required for "Email".

### Add Controls
The following policy controls are available for files both downloaded and emailed:
- **Expiration**  
  - Removes recipient access after the selected time frame.  Data owner maintains ability to decrypt file content.  
- **Disable Re-sharing**  
  - Authorized recipients are not able to add additional authorized users to the file.
- **Watermarking**  
  - Document is watermarked with recipient email address; recipients are unable to download the unprotected (plaintext) version of the file. 

### Add a Personalized Message (optional, email flow only)
Users can add an optional, personalized message to their email recipients.  

**NOTE:** The personalized message _will not be encrypted_.  

### Authenticate
File owners authenticate with their email addresses. A verification code will be emailed to the owner and must be copied into the Virtru auth widget.  List of all available authentication mechanisms [here](https://developer.virtru.com/docs/how-to-add-authentication).

