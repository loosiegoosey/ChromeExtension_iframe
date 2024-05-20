## Overview

Overview
The "Chrome Extension Betting History" project is a Chrome extension designed to interact with betting history information on a specific webpage. The extension listens for changes on LinkedIn web pages and executes monitoring scripts on specified bet IDs within an iframe.

##
## Features

Features
- **LinkedIn Page Detection**: Automatically activates on `linkedin.com` pages.
- **Bet ID Monitoring**: Periodically checks specific bet IDs on an iframe within a webpage.
- **Data Interactions**: Manipulates DOM elements based on bet ID availability.

##
## Installation Instructions

Installation Instructions
1. **Clone the repository**:
    ```sh
    git clone https://github.com/WangStar1031/ChromeExtension_iframe.git
    ```
2. **Navigate to the Extension Folder**:
    ```sh
    cd ChromeExtension_iframe/bettinghistory
    ```
3. **Load the extension into Chrome**:
    1. Open Chrome and go to `chrome://extensions/`.
    2. Enable "Developer mode" using the toggle on the top-right corner.
    3. Click on "Load unpacked" and select the `bettinghistory` folder.

##
## Usage Examples

Usage Examples
Once the extension is installed and initialized, it will automatically start monitoring the betting IDs on LinkedIn pages.

1. Navigate to `https://www.linkedin.com`.
2. The extension will activate, indicated by the extension icon in the Chrome toolbar.
3. Open the console to see debug information regarding the monitored bet IDs.

### Example Code Snippet
Here is a snippet from the `mornitoring.js` file demonstrating how bet IDs are monitored:
```javascript
var arrIDs = [15051590487, 15047347079, 15047369723, 15047391757];
var mainChecked = [];

for (var i = 0; i < arrIDs.length; i++) {
    mainChecked.push(false);
}
var interval = setInterval(setZeroValue, 100);

function setZeroValue() {
    for (var i = 0; i < arrIDs.length; i++) {
        if (mainChecked[i] == true)
            continue;
        var id = arrIDs[i];
        var $row = $('tr[data-betid="' + id + '"]', $('iframe').get(0).contentWindow.document);
        if ($row.length == 0)
            continue;

        // Additional actions to be performed on the $row can be added here.
    }
}
```

##
## Code Summary

Code Summary
- **`background.js`**: Contains the main logic to detect page changes and apply rules when a LinkedIn page is loaded.
    ```javascript
    chrome.runtime.onInstalled.addListener(function() {
        chrome.declarativeContent.onPageChanged.removeRules(undefined, function() {
            chrome.declarativeContent.onPageChanged.addRules([{
                conditions: [new chrome.declarativeContent.PageStateMatcher({
                    pageUrl: { hostEquals: 'www.linkedin.com' },
                    })
                ],
                actions: [new chrome.declarativeContent.ShowPageAction()]
            }]);
        });
    });
    ```
- **`mornitoring.js`**: Monitors specific bet IDs within an iframe, performing actions on matching elements.
- **`js/jquery.min.js`**: Minified jQuery library used for DOM manipulation within the extension.

##
## License

License
The project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

---

Happy coding! If you encounter any issues, please open an issue on the [GitHub repository](https://github.com/WangStar1031/ChromeExtension_iframe/issues).