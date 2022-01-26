# Rose Registration Automation Tool
This script will:
- automatically fill in a PIN
- randomly refresh the waiting screen
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
// In the array below, enter up to 10 CRNs. If you have less than 10, use two single quotes
const classes = [0, 0, 0, 0, 0, 0, 0, 0, '', ''];
// Enter your registration PIN below. This information doesn't leave your device
const pin = 111111;

// -------------------------------------------------------------------------------------
// IMPORTANT: Do not change any of the code below and make sure you've copied everything
//            We're not responsible for registration failures based on this script
// -------------------------------------------------------------------------------------

var url = window.location.pathname;
if (url.includes('P_AltPin') || url.includes('P_CheckAltPin') || url.includes('P_Regs')) {
    if (document.querySelector('#apin_id') !== null) {
        console.log('trying pin...');
        document.querySelector("#apin_id").value = pin;
        document.querySelector("body > div.pagebodydiv > form > input[type=submit]").click();
        timeTrack();
    } else {
        if (!document.querySelector('.dataentrytable')) {
            console.log('found waiting page, refreshing soon...');
            timeTrack();
        } else {
            if (!cookieCheck('completedRegistration')) {
                console.log('found registration page, trying to autofill courses...');
                for (var i = 0; i < 10; i++) {
                    document.querySelectorAll('.dedefault > input[name="CRN_IN"]')[i].value = classes[i];
                }
                console.log('courses filled, adding cookie and submitting...');
                document.cookie = 'completedRegistration=true ';
                document.querySelector('input[value="Submit Changes"]').click();
            } else {
                alert('Course autofill complete!');
                console.log('Thanks for using this tool! Learn more at https://csse132.rhit.cf/registration');
            }
        }
    }
}

function timeTrack() {
    var now = new Date();
    var timeUntil = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 7, 30, 0, 0) - now;
    console.log(timeUntil);
    if (timeUntil < 0) {
        console.log('registration time, loading the next page...');
        setTimeout(function () {
            location.reload();
        }, 200);
    }
    if (timeUntil > 10000) {
        setTimeout(function () {
            location.reload();
        }, Math.floor(Math.random() * 10000));
    }
    setTimeout(function () {
        location.reload();
    }, timeUntil);
}

function cookieCheck(search) {
    let decodedCookie = decodeURIComponent(document.cookie);
    let ca = decodedCookie.split(';');
    for (let i = 0; i < ca.length; i++) {
        let c = ca[i].split('=');
        if (c[0].substring(0, 1) == ' ') {
            c[0] = c[0].substring(1);
        }
        if (c[0] === search) {
            return c[1];
        }
    }
    return false;
}
```

Click the save button and you're finished! Open the registration page and the script will do the rest. Questions can be directed to [this email address](mailto:hello@canon.click).
