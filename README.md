# waitForKeyElements()
A utility function for userscripts that detects and handles AJAXed content. 

Forked from [CoeJoder/waitForKeyElements.js](https://github.com/CoeJoder/waitForKeyElements.js) who in turn forked [the original](https://gist.github.com/BrockA/2625891) and CoeJoder improved the original a lot, including:
- does not require jQuery
- avoids [the quirks](https://www.thecodeship.com/web-development/alternative-to-javascript-evil-setinterval/) associated with `setInterval()`
- optionally takes a function instead of a string for querying elements on page

## Installation
Add the following to your userscript's metadata block:
```javascript
// @require https://raw.githubusercontent.com/niikoo/waitForKeyElements.js/master/waitForKeyElements.js
```
If your userscript was already installed, you'll have to reinstall it to pickup the change. See [documentation](https://sourceforge.net/p/greasemonkey/wiki/Metadata_Block/#require).

## Usage
### With selector string
```javascript
waitForKeyElements("div.comments", (element) => {
  element.innerHTML = "This text inserted by waitForKeyElements().";
});
```
### With selector function
```javascript
waitForKeyElements(() => {
  const iframe = document.querySelector('iframe');
  if (iframe) {
    const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
    return iframeDoc.querySelectorAll("div.comments");
  }
  return null;
}, callbackFunc);
```

## Additional Resources
If you need a more general purpose polling method, consider using the `wait()` function of [Greasemonkey Wrench](https://github.com/CoeJoder/GM_wrench), a toolbox of userscript utilities.
