# The Finger (Selenium)

The Finger is a library that provides an alternate implementation to click on page elements using selenium.

You can use The Finger as a replacement for selenium's `.click()` method:
```javascript
// instead of
await driver.findElement(By.id("login-btn")).click()

// you can use the finger
await finger.click(By.id("login-btn"))
```

## When to use The Finger, and how it works

The Finger handles edge cases that selenium click command might have difficulties with due to the way the UI element is structured, for example:
- button elements with a label element overlay what would cause "element click intercepted" error
- elements that rapidly re-render, causing "stale element reference" error 

The Finger works by scrolling the target element into view, finding the position of target element, and then using the `.actions()` method instead of the `.click()` method to move the mouse over the target element and trigger the mouse button.

This means that even if there's another element that is layered on top of the target element (which typically results in "element click intercepted" error using the `.click()` method), or if the element is re-rendered intermittently (which typically results in "stale element reference" error using the `.click()` method), the Finger will sucessfully scroll, move to, and click at the position of the target element similar to a human user.

Addtionally, the finger implicitly waits for the element to be rendered on page using automatic retries to find the element until the element is present or the command times out (default of 15 seconds).

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

## TODOs and request for contributions
 
- While this library is implemented for selenium-javascript, conceptually the same can be implemented for other browser automation libraries in other languages.
- Add options to the click command to :
  - configure the retry timeout