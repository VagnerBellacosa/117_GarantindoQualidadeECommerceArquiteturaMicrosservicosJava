# Writing reusable end-to-end tests with TestCafe

## 

February 27, 2020 3 min read 

![An image of the Node.js logo and the testcafe logo.](https://blog.logrocket.com/wp-content/uploads/2020/02/Nod-js-test-cafe.png)

End-to-end testing involves testing the flow of an application.

This usually involves testing the various ways a user will interact with an application.

It helps to ascertain that an application works as expected.

End-to-end testing or UI testing has seen more adoption over the years due to increasing complexities in developing frontend applications, which is accompanied by different teams contributing to the same codebase.

As a result, there are lapses that might not necessarily be covered by pre-established testing methods such as unit testing or integration testing, which gives rise to the need for end-to-end testing.

In this article, we’ll be using TestCafe as our tool of choice. Other frameworks worth mentioning are [cypress.io](https://www.cypress.io/), [nightmarejs](http://www.nightmarejs.org/) and [selenium](https://selenium.dev/).

## How to run TestCafe

We will be diving deeper into TestCafe by looking at:

- Ways to structure our test
- Writing reusable functions
- Doing clean up after testing
- Executing assertions

To get started, you need to have Node.js installed on your local machine.

If you don’t, here’s the link to their [official website](https://nodejs.org/en/).

Once you’re done installing Node.js, you will need to install TestCafe as well.

I’ll add `-g` flag to install it globally so I don’t have to install it for every project.

Here’s the command to get that done:

```
npm install -g testcafe
```

We will be using https://en.wikipedia.org/ as our website of choice.

Let’s create a script to run our test write-in:

```
mkdir testcafe-sample
cd testcafe-sample 
touch test.js
```

Inside Test.js:

```
import { Selector, ClientFunction } from 'testcafe';

const getLocation = ClientFunction(() => document.location.href);
fixture `My first fixture`
    .page `https://www.wikipedia.org/`;
    test('users can search', async t => {
      await t
      .click(Selector('#searchInput'))
      .typeText(Selector('#searchInput'), 'vikings')
      .click(Selector('button[type=submit]'))
      .expect(getLocation()).contains('en.wikipedia.org/wiki/Vikings');
    });
```

We run this by running the following command in our terminal:

```
testcafe chrome test.js
```

![An example of the output of a test on TestCafe to a console .](https://blog.logrocket.com/wp-content/uploads/2020/02/writing-reusable-tests-testcafe.png)

We selected things on the page via CSS selectors passed to the Selector function.

We also have the `ClientFunction` that exposes us to native APIs like `window.location`, among others.

We have tested that a user can search.

We will also be testing that a user can log into an existing account.

I have created a sample account for the purposes of this article.

Here is the code that makes this happen:

```
   test('users can login to an existing account', async t => {
      await t
      .click(Selector('button[type=submit]'))
      .click(Selector('#pt-login'))
      .expect(getLocation()).contains('UserLogin'); //asserts that we are on the login page.
      await t
      .click(Selector('#wpName1'))
      .typeText(Selector('#wpName1'), 'Johnny Dowe')
      .click(Selector('#wpPassword1'))
      .typeText(Selector('#wpPassword1'), '96#CMqi@_in8*wR')
      .click(Selector('button#wpLoginAttempt'))
      .expect(getLocation()).contains('search');
    });
```

It’s important to mimic the flow that a normal user would follow when using our application, so we will extract this into a separate function.

```
const login = t => {
await t
      .click(Selector('button[type=submit]'))
      .click(Selector('#pt-login'))
      .expect(getLocation()).contains('UserLogin'); //asserts that we are on the login page.
      await t
      .click(Selector('#wpName1'))
      .typeText(Selector('#wpName1'), 'Johnny Dowe')
      .click(Selector('#wpPassword1'))
      .typeText(Selector('#wpPassword1'), '96#CMqi@_in8*wR')
      .click(Selector('button#wpLoginAttempt'))
      .expect(getLocation()).contains('search');
}
```

Similarly, we can have a function that helps a user log out after performing an action on our application.

Here, we’ll use Wikipedia as a reference.

The flow:

login ![➡️](https://s.w.org/images/core/emoji/13.1.0/svg/27a1.svg) perform some action ![➡️](https://s.w.org/images/core/emoji/13.1.0/svg/27a1.svg) logout

Let’s say we want to write some code to contribute to Wikipedia — the pseudocode will look like this using our reusable functions:

```
test('users should be able to contribute', async t => {
      await login(t);
      /*
      some code to contribute to wikipedia
      */
      await logout(t);
    });
```

We can see reusability in action and we have a flow whenever we want to perform an action.

We’ll assume a few things to run this example.

First, we’ll assume that we’re running the application on a desktop.

We can simulate a mobile environment by resizing the window to what will be obtainable in a mobile phone.

Here is a sample code that can do this:

```
fixture`some description`
  .page`some url`
  .beforeEach(async t => {
    await t.resizeWindow(375, 667);
  });
```

I have used a sample account that might get deactivated upon running this test suite several times due to security measures set in by Wikipedia.

You can create your own account and run the script with the new details.

The tests script might fail when you are running because of the way Wikipedia has laid out their website, so the selectors may not apply.

The error message are always reported in the console.

Here is what it will most likely look like:

![An image displaying errors logged into the console found through an end-to-end test.](https://blog.logrocket.com/wp-content/uploads/2020/02/aversion-error.png)

## Conclusion

In this post, we’ve gone over how to write end-to-end tests on web applications using the `Testcafe` intuitive API.

There are still quite a few things that I didn’t touch on related to TestCafe, but I hope this gives you insight on how to get started with TestCafe.

Here is a [repository](https://github.com/gbols/testcafe) that contains all the code for reference purposes.

## [LogRocket](https://logrocket.com/signup/): Full visibility into your web apps

[![LogRocket Dashboard Free Trial Banner](https://blog.logrocket.com/wp-content/uploads/2017/03/1d0cd-1s_rmyo6nbrasp-xtvbaxfg.png)](https://logrocket.com/signup/)

[LogRocket](https://logrocket.com/signup/) is a frontend application monitoring solution that lets you replay problems as if they happened in your own browser. Instead of guessing why errors happen, or asking users for screenshots and log dumps, LogRocket lets you replay the session to quickly understand what went wrong. It works perfectly with any app, regardless of framework, and has plugins to log additional context from Redux, Vuex, and @ngrx/store.

In addition to logging Redux actions and state, LogRocket records console logs, JavaScript errors, stacktraces, network requests/responses with headers + bodies, browser metadata, and custom logs. It also instruments the DOM to record the HTML and CSS on the page, recreating pixel-perfect videos of even the most complex single-page apps.

## 200’s only ![img](https://blog.logrocket.com/wp-content/uploads/2019/10/green-check.png) Monitor failed and slow network requests in production

Deploying a Node-based web app or website is the easy part. Making sure your Node instance continues to serve resources to your app is where things get tougher. If you’re interested in ensuring requests to the backend or third party services are successful, [try LogRocket](https://logrocket.com/signup/). [![LogRocket Network Request Monitoring](https://blog.logrocket.com/wp-content/uploads/2019/12/network-request-filter-2-1.png)](https://logrocket.com/signup/)https://logrocket.com/signup/

[LogRocket](https://logrocket.com/signup/) is like a DVR for web and mobile apps, recording literally everything that happens while a user interacts with your app. Instead of guessing why problems happen, you can aggregate and report on problematic network requests to quickly understand the root cause.

LogRocket instruments your app to record baseline performance timings such as page load time, time to first byte, slow network requests, and also logs Redux, NgRx, and Vuex actions/state. [Start monitoring for free](https://logrocket.com/signup/).

[Try it for free](https://logrocket.com/signup/).

### 