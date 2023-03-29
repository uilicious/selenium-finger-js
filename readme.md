# The Finger (Selenium)

The Finger is a library that provides an alternate implementation to click on page elements using selenium.

## Setup

Install `selenium-finger` via NPM:

```
npm install selenium-finger 
```

## Usage

Import into your project.
```javascript
const { TheFinger } = require("selenium-finger")
```

Initialise webdriver, here's an example to setup webdriver using chromedriver
```javascript
let driver = await new Builder().forBrowser('chrome').build();
```

Create an instance of the finger, and pass in the webdriver instance.
```javascript
let finger = new TheFinger(driver)
// or you could name it something else
let I = new TheFinger(driver)
```

Clicking using the finger to click on a page element
```javascript
finger.click(By.id("login-button"))
```
