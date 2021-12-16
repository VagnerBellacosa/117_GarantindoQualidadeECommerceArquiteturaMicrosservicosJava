# End-to-end testing, simplified

No WebDriver required. No manual timeouts needed. Cross-browser testing out-of-the-box.

$ npm i -g testcafe

and [Create your first test today](https://testcafe.io/documentation/402635/getting-started)

## Why people love TestCafe

- ![1 Minute to Set Up](https://testcafe.io/img/lovetestcafe-minute.svg)

  ### 1 Minute to Set Up

  TestCafe does not require WebDriver or other testing software. It runs on Node.js and uses the browsers you already have.

- ![Clean code](https://testcafe.io/img/lovetestcafe-clean-code.svg)

  ### Clean code

  TestCafe frees you from the need to insert manual timeouts and use cumbersome boilerplate expressions. You’ll spend less time tracking down annoying issues and more time doing what matters most.

- ![Free and Open Source](https://testcafe.io/img/lovetestcafe-opensource.svg)

  ### Free and Open Source

  TestCafe is available for free and distributed under the MIT license. We are committed to our open-source community and are actively extending TestCafe's capabilities.

![qa-engineer-picture](https://testcafe.io/img/qa-guy.svg)

## Write tests with ease

TestCafe’s intuitive syntax makes teams more productive from day one.
Check the test below and see for yourself.

TestCafe 😊

```js
fixture `Pizza Palace`
    .page `https://testcafe-demo-page.glitch.me/`;

test('Submit a form', async t => {
    await t
        // automatically dismiss dialog boxes
        .setNativeDialogHandler(() => true)

        // drag the pizza size slider
        .drag('.noUi-handle', 100, 0)

        // select the toppings
        .click('.next-step')
        .click('label[for="pepperoni"]')
        .click('#step2 .next-step')

        // fill the address form
        .click('.confirm-address')
        .typeText('#phone-input', '+1-541-754-3001')
        .click('#step3 .next-step')

        // zoom into the iframe map
        .switchToIframe('.restaurant-location iframe')
        .click('button[title="Zoom in"]')

        // submit the order
        .switchToMainWindow()
        .click('.complete-order');
});
```

Selenium (JavaScript) 😕

```js
const {Builder, By, Key, until} = require('selenium-webdriver');

(async function pizzaPalace() {

    const driver = await new Builder().forBrowser('firefox').build();
    
    try {
        await driver.get('https://testcafe-demo-page.glitch.me/');

        // drag the pizza size slider
        const sourceEle = driver.findElement(By.className("noUi-handle"));
        const actions = driver.actions({async: true});
        await actions.dragAndDrop(sourceEle, {x:100, y:0}).perform();

        // select the toppings
        await driver.findElement(By.className("next-step")).click();
        await driver.findElement(By.css('label[for="pepperoni"]')).click(); 
        await driver.findElement(By.css('#step2 .next-step')).click();

        // fill the address form
        await driver.wait(until.elementLocated(By.css('.google-map')),10000);
        await driver.findElement(By.className("confirm-address")).click();   
        await driver.findElement(By.id('phone-input')).sendKeys('+1-541-754-3001');
        await driver.findElement(By.css('#step3 .next-step')).click();

        // zoom into the iframe map
        await driver.wait(until.elementLocated(By.css('.restaurant-location iframe')),10000);
        const restaurantLocationFrame = await driver.findElement(By.css('.restaurant-location iframe'));
        await driver.switchTo().frame(restaurantLocationFrame);
        await driver.wait(until.elementLocated(By.css('button[title="Zoom in"]')),10000);
        await driver.findElement(By.css('button[title="Zoom in"]')).click();

        // submit the order
        await driver.switchTo().defaultContent();
        await driver.findElement(By.className("complete-order")).click();

        // dismiss the confirmation dialog
        await driver.wait(until.alertIsPresent());
        const confirmationMessage = driver.switchTo().alert();
        await confirmationMessage.accept();
                
    } finally {
        await driver.quit();
    }
})();
```

## Test in every browser that matters

Don’t let Internet Explorer push you over the Edge. Run your tests in desktop browsers and headless browsers. Connect to remote testing servers, mobile devices and cloud browser farms.

- ![chrome](https://testcafe.io/img/browser-chrome.svg)
- ![firefox](https://testcafe.io/img/browser-firefox.svg)
- ![safari](https://testcafe.io/img/browser-safari.svg)
- ![edge](https://testcafe.io/img/browser-edge.svg)
- ![ie](https://testcafe.io/img/browser-ie.svg)
- ![opera](https://testcafe.io/img/browser-opera.svg)
- ![browserstack](https://testcafe.io/img/browser-browserstack.svg)
- ![lambdatest](https://testcafe.io/img/browser-lambdatest.svg)

## Deploy without fear

- 

  ### CI/CD-ready

  TestCafe integrates with all popular CI/CD solutions.

- 

  ### Concurrent test runs

  Run your tests in multiple browsers at once to save time and computing resources.

- 

  ### If something goes wrong...

  Use the built-in Debug Mode to pin-point the source of your frustration.

[Why TestCafe?](https://testcafe.io/documentation/402631/why-testcafe)

![laptop](https://testcafe.io/img/studio-v2-ui@2x.png)

## Automate Your Web Testing – 100% Code‑Free!

You can now visually record automated test scripts. Code-free tests lower the learning curve and improve productivity.

[Try TestCafe Studio IDE](https://www.devexpress.com/products/testcafestudio/)

## 