# Easy e2e Testing with TestCafe

In the initial days of my career when I start to learn automation, Selenium was the wide spread tool that has some exciting features and there are lot of frameworks built on it with even more features and flexibility. When properly set up, they definitely provide us with reliable tests.

However, in an ever-changing world, we aren't just utilising all these cool features.

- Getting/installing drivers for browser support
- Creating capabilities and profiles
- Matching of driver and browser versions to avoid compatibility issues
- Grid configuration and separate launchers for running the tests in parallel

So, let's shift our focus to check the latest tools such as TestCafe to overcome these issues.

# TestCafe

[TestCafe](https://devexpress.github.io/testcafe/) is a new, open-source, [Node.js](https://nodejs.org/en/) based e2e testing framework. It's an excellent alternative to Selenium-based tools since it injects itself into the website as JS scripts, so it's more stable and faster. This allows TestCafe to run on any browser, including mobile devices and cloud services as well. It doesn't need Selenium to start your browser window, execute the tests in it and provide useful test report after the execution.

One of its main perks is that it takes about a minute to setup and to start testing (and it doesn't use WebDriver).

It works with most popular operating systems and browsers. Tests are written in JavaScript or TypeScript.

## Setup for Testing

First make sure you have Node.js version 4.x or higher installed. Before doing anything else, we need to create NodeJS package, i.e.just a directory containing a `package.json` file. We can easily do that in 2 steps.

1. Create an empty directory.
2. Run: `npm init` inside the new directory.

This should ask for a bunch of information. For those interested this is driven by [init-package-json](https://github.com/npm/init-package-json).

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--iVVoQ5bf--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/osmpiu2ep6v2po25thut.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--iVVoQ5bf--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/osmpiu2ep6v2po25thut.png)

After this, we need to add *TestCafe* library in the project.

```
npm install testcafe --save
```

## Architecting

One of the bests currently solutions to architecting a testing project is using the **Page Objects Pattern**. The goal behind this pattern is to abstract any page information away from the actual tests. Ideally, you should store all selectors or specific instructions that are unique for a certain page in a page objects file so that you still can run your test after you've completely redesigned your page.

The main advantage of this pattern is the **encapsulation of elements**, **methods and actions,**then we can reuse the code in any test and if we change the library that runs the tests, we can reuse the test structure.

To support this architecture, I recommend you create a directory to save the page objects files and another to save the tests files, like this:

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--tJNXBIjT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/jlvrsl2m43j935j8m6rm.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--tJNXBIjT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/jlvrsl2m43j935j8m6rm.png)

## The first test

The [TestCafe documentation](https://devexpress.github.io/testcafe/documentation/getting-started/) is pretty helpful, in fact, I learnt most of the things I know by just following through the docs.

A very helpful method you would be making use of most of the time whilst interfacing with testcafe is the `Selector` method. This method makes sure to select the elements within the DOM that you would love to test.

The test will be opening google and get the title of the tab. So, I have created a page (page-object/googlesearchpage.js) with elements needed in the page-object folder.

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--Kcs5netX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0xm1fmndbkt8zludjsha.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--Kcs5netX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0xm1fmndbkt8zludjsha.png)

On googlesearchpage.js, I have added an input element and a method to get title of the page. The next step is to create the test script file (tests/test.js) and import the methods from the page objects:

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--3duw5A5a--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0aceggtmx9a1entzze6g.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--3duw5A5a--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0aceggtmx9a1entzze6g.png)

Now add a script — `./node_modules/.bin/testcafe chrome tests` in the package.json file. Now the package.json will look like this:

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--fCzhzrd_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6xmc4ybczaj3vt6ha0dv.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--fCzhzrd_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6xmc4ybczaj3vt6ha0dv.png)

Done! Now we will be able to run the test. Open the terminal and execute:

```
npm run test:chrome
```

## Extending the tests

Now, i will try to extend the tests

1. Add one more method to googlesearchpage to search for a text
2. Create a new page in the page-object for the search results page.

Run the command `npm run test:chrome` once again in the terminal:

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--DHm9HLTx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/lgrqs25s4quybqwgmqxx.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--DHm9HLTx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/lgrqs25s4quybqwgmqxx.png)

Code for the extended tests is here: https://github.com/prasadmudedla/test-cafe-project.git

## Running in other browsers

Another important feature that *testcafe* have is that we can run the tests in a lot of browsers. You can see the available browsers [here](https://devexpress.github.io/testcafe/documentation/using-testcafe/common-concepts/browsers/).

To make the execution simpler, let's add some scripts in the package file at scripts section and run it using *npm run* function:

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--k967IMSc--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/qsea9ggzid7zfi9tjbce.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--k967IMSc--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/qsea9ggzid7zfi9tjbce.png)
package.json

## Extending TestCafe Functionality

You can visit GitHub to learn more about the [TestCafe ecosystem](https://github.com/DevExpress/testcafe#testcafe-ecosystem). If you need more functionality in test code, you can use any node.js module. TestCafe also provides the extended capabilities for [using portable and remote browsers](https://devexpress.github.io/testcafe/documentation/extending-testcafe/browser-provider-plugin/) and [customizing the test reports](https://devexpress.github.io/testcafe/documentation/extending-testcafe/reporter-plugin/).

And if you feel like making your own plugin, check out the [tips in the documentation](https://devexpress.github.io/testcafe/documentation/extending-testcafe/). You can also send a quick note to TestCafe developers to share your plugin with the community (via [GitHub issue](https://github.com/DevExpress/testcafe/issues) or [Twitter](https://twitter.com/DXTestCafe)).

Hopefully this article helps you avoid some of the mistakes I made when using these tools. Happy testing!

- [Testcafe](https://dev.to/tag/testcafe)
- [Automation](https://dev.to/tag/automation)
- [Automation Testing](https://dev.to/tag/automation-testing)
- [Automation Tools](https://dev.to/tag/automation-tools)
- [Ui Automation Testing](https://dev.to/tag/ui-automation-testing)

## 