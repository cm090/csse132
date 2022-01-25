# Rose Registration Automation Tool
This script will:
- automatically fill in a PIN at random intervals
- input CRNs as soon as the registration page opens

## Requirements
- Chromium-based browser (Chrome, Edge, Brave, Opera, etc.)
- Chrome web store
- Basic JavaScript knowledge

## Getting Started
Allow the script to interface with the registration website by installing
[Injector (chrome.google.com)](https://chrome.google.com/webstore/detail/injector/bfdonckegflhbiamlmidciapolfccmmb)

Click on the extension to access the setup page

Click the plus button and enter 
`bxess-prod-hv.rose-hulman.edu`

Above the textbox on the right, use the dropdown menu to select JavaScript

Paste the following code into the textbox and make changes based on the comments
```
const classes = [0, 0, 0, 0, 0, 0, 0, 0];
const pin = 123456;
for(var i = 0; i < document.querySelectorAll('input.form-control').length; i++) {
  document.querySelectorAll('.dedefault > input[name="CRN_IN"]')[i].value = classes[i];
}
document.querySelectorAll('input[value="Submit Changes"]').click();
```

Click the save button and you're finished! Open the registration page and the script will do the rest. Questions can be directed to [this email address](mailto:hello@canon.click).
