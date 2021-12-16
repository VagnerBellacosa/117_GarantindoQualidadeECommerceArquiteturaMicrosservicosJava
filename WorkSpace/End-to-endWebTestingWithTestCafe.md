# End-to-end web testing with TestCafe

[![Jennifer Proust (ג'ניפר פרוסט)](https://miro.medium.com/fit/c/96/96/1*FbbEjoC85JeO6gr5PJ0RzA.jpeg)](https://proustibat.medium.com/?source=post_page-----766ddbd74924-----------------------------------)  -  [Jennifer Proust (ג'ניפר פרוסט)](https://proustibat.medium.com/?source=post_page-----766ddbd74924-----------------------------------)  -  [Mar 7, 2019](https://medium.com/xebia-france/end-to-end-web-testing-with-testcafe-766ddbd74924?source=post_page-----766ddbd74924-----------------------------------) 

![img](https://miro.medium.com/max/1400/1*VjWsyasduivy_Hkr2LRq2A.png)

E2E tests are easy with TestCafe

# What you’ll learn

## Getting Started

What is [TestCafe](https://devexpress.github.io/testcafe/), how to install it and create your first test.

## Using TestCafe

Write a real test using a sample project: this will show you how to query elements, observe page state, interact with elements, use assertions. We’ll also learn how to organize our files with the page object pattern and using hooks.

## Running Tests

Browsers support, headless mode, device emulation, concurrency.

## Continuous Integration

Using [CircleCI](https://circleci.com/) to run tests and see results.

## Features

Some features you should know exist: intercepting HTTP requests**,** screenshots and videos, reporters, [TestCafe studio](https://www.devexpress.com/products/testcafestudio/).

Initially this article was a presentation, you can download the slides support [here](https://github.com/proustibat/xke-introduction-testcafe/raw/master/[XKE] - Introducing E2E testing with TestCafe.pdf). Sources are available on [Github](https://github.com/proustibat/xke-introduction-testcafe).

# Getting Started

## What is TestCafe

A node.js tool to automate end-to-end web testing. You can write tests in JS or TypeScript, run them and view results. The tool is free and open source. The v1.0.1 is out since February 2019.

## Requirements and installation

Of course be sure [Node](https://nodejs.org/) and [NPM](https://www.npmjs.com/get-npm) are installed (also [yarn](https://yarnpkg.com/) if you prefer). No webdriver is needed, just one command:

```
yarn add --dev testcafe
```

## Test Code Structure

Here is a basic test file. It contains a fixture: a category of tests. A fixture is defined by a name and a page function that targets the start page of our group of tests. TestCafe uses a proxy server, it injects scripts in the page then we can inspect the elements.

Each test receives a test controller as a parameter. The test controller is an object that allows us to access the test api. We’ll use it for actions and assertions.

We run the test with the following command:

```
testcafe chrome test.js
```

Then the test is ran in a chrome browser (you can choose another browser):

```
Running tests in:
- Chrome 72.0.3626 / Mac OS X 10.13.6Getting Started
✓ My first test1 passed (2s)
```

# The project we are going to test

A [React](https://reactjs.org/) app created with [create-react-app](https://github.com/facebook/create-react-app) and [material-ui](https://material-ui.com/):

![img](https://miro.medium.com/max/1400/0*xO6lCR9laS_0Kza6)

Home page with an enter button

![img](https://miro.medium.com/max/1400/0*bAoaN46nMaxOEq-W)

Posts page with a list of links

![img](https://miro.medium.com/max/1400/0*YOBUaquZsEsWznGm)

Article page with content of a post

![img](https://miro.medium.com/max/1400/0*xGRkeAPJUjzbUbUJ)

Add page to post a new article

The site is deployed on [xke-introduction-testcafe.surge.sh](https://xke-introduction-testcafe.surge.sh/)

# The tests we want

**First scenario:**

> As a user, when I’m on the home page, I can enter the app and links to articles. If I click on a link, I can see the article page.

**Second scenario:**

> As a user, from the home page, I can access the add page with a form in order to post a new article. I can post my article.

We will enable the **live mode** to watch for changes with the L option:

```
testcafe chrome e2e/**/* -L
```

## Let’s write our first scenario skeleton

e2e/index.js

The result in our terminal:

```
Live mode is enabled.
TestCafe now watches source files and reruns
the tests once the changes are saved.
                    
You can use the following keys in the terminal:
'Ctrl+S' - stops the test run;
'Ctrl+R' - restarts the test run;
'Ctrl+W' - enables/disables watching files;
'Ctrl+C' - quits live mode and closes the browsers.Watching the following files:
  /Users/proustibat/workspace/xebia/xke-introduction-testcafe/e2e/index.js
Running tests in:
 - Chrome 72.0.3626 / Mac OS X 10.13.6Navigation
 ✓ Access to a specific article from the home page1 passed (0s)
```

# Querying elements with Selector

Selector is a function that identifies a webpage element in the test. The selector API provides methods and properties to select elements on the page and get their state.

TestCafe uses standard CSS selectors to locate elements. It’s like when you use `document.querySelector` in JS (learn more by [reading the documentation](https://devexpress.github.io/testcafe/documentation/test-api/selecting-page-elements/selectors/using-selectors.html)).

In our test, we import `Selector` then we need to select the start button on our home page:

# Actions

Test API provides a set of actions that enable you to interact with the webpage.

Actions are implemented as methods in the test controller object and can be chained.

Multiple actions are available: Click, Right Click, Double Click, Drag Element, Hover, Take Screenshot, Navigate, Press Key, Select Text, Type Text, Upload, Resize Window ([read the documentation to learn more](https://devexpress.github.io/testcafe/documentation/test-api/actions/)).

# Observing page state

TestCafe allows you to observe the page state via:
\- Selector used to get direct access to DOM elements
\- ClientFunction used to obtain arbitrary data from the client side.

For example in our test, once we click on the button, we should be on the posts page, so we can access the title page and log its innerText as follows:

# Assertions

We now need assertions to check data or behaviors. The test controller provides an `expect` function that should check the result of performed actions.

The following assertion methods are available: Deep Equal, Not Deep Equal, Ok, Not Ok, Contains, Not Contains, Type of, Not Type of, Greater than, Greater than or Equal to, Less than, Less than or Equal to, Within, Not Within, Match, Not Match.

In our test, we want to check that the title is “Posts Page”:

# Finishing our tests

Now we learned the 4 main concepts of TestCafe: selectors, page state, actions and assertions. So we can complete our first test:

## What about our second test

Remember for our second test we want to start from the home page, enter the site by clicking the start button (like the first part of our first test). Then we want to verify the users navigate to the form page when they click on the add button. Finally they should be able to fill the form and submit it.

So the beginning of our test is the same as the first, and we need to do what is written in comments:

## Let’s begin with the well known part!

This is not new now, we are able to get elements, have them undergo some actions then check some other elements exist on the page:

To fill the form, we use the `typeText` method of the TestController. Submitting the form is not new, we just need to select the button then click it:

# The page object pattern

Now we need to talk about the organisation of our code. Writing our tests is repetitive: we go on a page, we check elements are present, we perform actions on it, then we check some elements are present, and so on.

During development process, markups, ids and classes can often change so we need to change Selectors everywhere it’s needed.

Fortunately, we can use the page object pattern:

- Page Model is a test automation pattern that allows you to create an abstraction of the tested page and use it in test code to refer to page elements.
- Keep page representation in the Page Model, while tests remain focused on the behavior.
- Improve maintainability.

Read TestCafe [documentation](https://devexpress.github.io/testcafe/documentation/recipes/use-page-model.html)

Now we will refactor our tests by creating page models.

## Creating home model

A model is a basic class. We define Selector in the constructor:

e2e/models/home.js

Now we can use our model in our tests by importing and instantiating it then accessing its selectors:

## Creating a posts page model

Following the same principle, we create a model for the posts page that contains selectors for its title, its links and its add button:

e2e/models/posts.js

Now we can use the model in our tests. Replace title and links selectors:

With:

Replace add button selector:

With:

## Creating article model

e2e/models/article.js

In our tests, replace:

With:

## Creating add page model

e2e/models/add.js

Use it in our tests by replacing:

with:

Note that we also chained actions. This is now more readable.

We now have 4 page models that represent the pages of our application. Each page contains its own Selectors.

Now we are going to do the same thing for actions.

## Adding actions to the model pages

TestCafe allows to use Test Controller outside of test code by importing it:

```
import { Selector, t } from ‘testcafe’;
```

Add this to our **add page model**:

Then use actions in our test:

Complete the add page model with:

Complete posts page model with:

Create a toast model as follows:

e2e/models/toast.js

# Our tests become even more simple

The first test was:

Then became:

Our second test was:

<iframe src="https://medium.com/media/e9fb23cea215ac2c7e7f5c372632739b" allowfullscreen="" frameborder="0" height="0" width="0" title="index.js" class="t u v mj aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 680px;"></iframe>

Then became:

<iframe src="https://medium.com/media/cc9c7d3730d2d49a648580459569a108" allowfullscreen="" frameborder="0" height="260" width="680" title="index.js" class="t u v mj aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 260px;"></iframe>

# Hooks

TestCafe allows you to specify functions that are executed before a fixture or test is started and after it is finished. Exactly like when you write unit tests.

- fixture.beforeEach( fn(t) )
- fixture.afterEach( fn(t) )
- test.before( fn(t) )
- test.after( fn(t) )

Note that test hooks override fixture hooks.

Remember we need to click start button in each of our tests. So we can use a fixture hook that will execute code before each test:

<iframe src="https://medium.com/media/5fa9534d098d22371acaf1327742579e" allowfullscreen="" frameborder="0" height="172" width="680" title="index.js" class="t u v mj aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 171.997px;"></iframe>

Then remove the corresponding lines from our tests.

# Debugging

## The debug method of TestController

TestCafe provides the `t.debug` method that pauses the test and allows you to debug using the browser’s developer tools.

Here we want to stop the scenario with a debugger after we enter title in the input and before we enter content in the textarea:

<iframe src="https://medium.com/media/80c2ae7bf5015136441bf32c7bcfb8ab" allowfullscreen="" frameborder="0" height="193" width="680" title="add.js" class="t u v mj aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 192.986px;"></iframe>

![img](https://miro.medium.com/max/60/0*ArkrbJGWQufy8DKJ?q=20)

![img](https://miro.medium.com/max/630/0*ArkrbJGWQufy8DKJ)

The debugger is visible in the console

![img](https://miro.medium.com/max/60/0*Jn_E6S2CG3BUbrZK?q=20)

![img](https://miro.medium.com/max/630/0*Jn_E6S2CG3BUbrZK)

The test has stop…

## Debugging with screenshots on failure

Use the following command to get screenshots [when the test failed](https://devexpress.github.io/testcafe/documentation/using-testcafe/command-line-interface.html#-s---screenshots-on-fails):

```
testcafe chrome e2e/**/* --screenshots ./screenshots --screenshots-on-fails
```

![img](https://miro.medium.com/max/60/0*WvSb5IeznBosATg8?q=20)

![img](https://miro.medium.com/max/630/0*WvSb5IeznBosATg8)

## Debugging with videos

Enables TestCafe to record videos of test runs and specifies the base directory to save these videos.

```
testcafe chrome e2e/**/* --video videos
```

Some options are available:

```
testcafe chrome e2e/**/* --video videos --video-options singleFile=true,failedOnly=true
```

See [documentation](https://devexpress.github.io/testcafe/documentation/using-testcafe/command-line-interface.html#--video-basepath) about videos

# Running Tests

## Browser support: installed browsers

Most of modern browsers locally installed can be detected: Google Chrome (Stable, Beta, Dev and Canary), Internet Explorer (11+), Microsoft Edge, Mozilla Firefox, Safari, Android browser, Safari mobile.

If these browsers are locally installed then TestCafe will detect it.

Run `testcafe --list-browsers` to list which browsers TestCafe automatically detects.

## Browsers support: remote device

To run tests on a remote mobile or desktop device, this device must have network access to the TestCafe server.

```
testcafe remote e2e/**/*
testcafe remote e2e/**/* --qr-code
```

![img](https://miro.medium.com/max/60/1*A8AK714SD12mhhHdKlUjeQ.png?q=20)

![img](https://miro.medium.com/max/630/1*A8AK714SD12mhhHdKlUjeQ.png)

## Browsers support: chrome device emulation

To do this, use the emulation browser parameter. Specify the target device with the device parameter:

```
testcafe "chrome:emulation:device=iphone 6/7/8" e2e/**/* --video artifacts/videos
```

<iframe src="https://cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FQPV4tlSxKRk&amp;url=http%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DQPV4tlSxKRk&amp;image=http%3A%2F%2Fi.ytimg.com%2Fvi%2FQPV4tlSxKRk%2Fhqdefault.jpg&amp;key=a19fcc184b9711e1b4764040d3dc5c07&amp;type=text%2Fhtml&amp;schema=youtube" allowfullscreen="" frameborder="0" height="480" width="854" title="XKE - Introduction to TestCafe - scenario 2 with iphone 6 7 8 emulation" class="t u v mj aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 382.188px;"></iframe>

## Browsers support: cloud testing services

TestCafe allows you to use browsers from cloud testing services.

The following plugins for cloud services are currently provided by the TestCafe team.

- Sauce Labs: [plugin](https://www.npmjs.com/package/testcafe-browser-provider-saucelabs)
- BrowserStack: [plugin](https://www.npmjs.com/package/testcafe-browser-provider-browserstack)

You can also create your own plugin: [see the doc](https://devexpress.github.io/testcafe/documentation/extending-testcafe/browser-provider-plugin/).

# Some other CLI options

Concurrent test execution:

```
testcafe -c 2 chrome e2e/**/*
```

Speed:

```
testcafe chrome e2e/**/* — speed 0.5
```

Multiple browsers with or without headless:

```
testcafe chrome:headless,firefox e2e/**/*
```

See the [documentation](https://devexpress.github.io/testcafe/documentation/using-testcafe/command-line-interface.html) for more options
You can also use a [.testcaferc.json](https://devexpress.github.io/testcafe/documentation/using-testcafe/configuration-file.html) file for the config.

# Reporters

Reporters are plugins used to output test run reports in a certain format.

TestCafe ships with the following reporters: spec (used by default), list, minimal, xUnit, JSON.

Here are some custom reporters developed by the community: NUnit, Slack, TeamCity.

Read the [documentation](https://devexpress.github.io/testcafe/documentation/using-testcafe/common-concepts/reporters.html) to know more

# Continuous Integration

## Prerequisites

Remember we should run `yarn start` before running our tests because we target `localhost:3000` as the start webpage.

Our goal is to test exactly the same code that will be deployed or not (depending on results). So we need to serve built content after we run `yarn build`.

We will use the [serve](https://www.npmjs.com/package/serve) package, so install it with `yarn add — dev serve`
Add a npm script to the package.json file:

```
“serve:build”: “serve -s build”
```

This will run our app on `localhost:5000`.

## Modify our tests to target build sources

In `e2e/index.js`, replace `localhost:3000` on our fixture page by `localhost:5000`. Then build the app with `yarn build`.

Serve the built content in a terminal with `yarn serve:build`then run testcafe in headless mode in another terminal:

```
testcafe chrome:headless e2e/**/*
```

## The all in one with the appCommand

For now we need 2 terminals to run our tests. This is not ideal.

The [appCommand](https://devexpress.github.io/testcafe/documentation/using-testcafe/command-line-interface.html#-a-command---app-command) of TestCafe executes the specified shell command before running tests.

So we can use it to serve our built app instead of running the `yarn serve:build` manually. Add this script to the package.json file:

```
“e2e:ci”: “testcafe chrome:headless e2e/*.js — app ‘yarn serve:build’”
```

Now we’re ready for [CircleCI integration](https://devexpress.github.io/testcafe/documentation/continuous-integration/circleci.html). If you don’t have any account, [create it](https://circleci.com/signup/) before going to the next step.

## Create config.yml in .circleci

```
version: 2.0
jobs:
 build:
   docker:
     - image: circleci/node:8-browsers
   working_directory: /home/circleci/project
   steps:
     - checkout
     - setup_remote_docker:
         docker_layer_caching: true
     # Download and cache dependencies
     - restore_cache:
         name: Restore Yarn Package Cache
         keys:
           - yarn-packages-{{ checksum "yarn.lock" }}
     - run:
         name: Install Dependencies
         command: yarn install --frozen-lockfile
     - save_cache:
         name: Save Yarn Package Cache
         key: yarn-packages-{{ checksum "yarn.lock" }}
         paths:
           - ~/.cache/yarn
     # Build
     - deploy:
         name: Build
         command: yarn build
     # End-to-end tests
     - run:
         name: Run e2e tests
         command: yarn e2e:ci
```

## Add your repo to CircleCI

On your dashboard click on “add projects” in the left bar menu
Find your repo, then click on “Set Up Project”:

![img](https://miro.medium.com/max/60/0*-owDG3VPKsudCESG?q=20)

![img](https://miro.medium.com/max/630/0*-owDG3VPKsudCESG)

## Start building the project on CircleCI

![img](https://miro.medium.com/max/60/0*qpT0BVDAXb-lHM2z?q=20)

![img](https://miro.medium.com/max/630/0*qpT0BVDAXb-lHM2z)

You should see your project running:

![img](https://miro.medium.com/max/60/0*0SHqPW644rnN9idd?q=20)

![img](https://miro.medium.com/max/630/0*0SHqPW644rnN9idd)

## Detailed workflow on CircleCI

![img](https://miro.medium.com/max/60/0*V16HQpVL1j3RZ6e9?q=20)

![img](https://miro.medium.com/max/630/0*V16HQpVL1j3RZ6e9)

![img](https://miro.medium.com/max/60/0*pKheXeomvaI01KiC?q=20)

![img](https://miro.medium.com/max/630/0*pKheXeomvaI01KiC)

## Use store_test_results

Add xunit reporter to the project:

```
yarn add — dev testcafe-reporter-xunit
```

Modify the CircleCI config:

```
# End-to-end tests
- run:
   name: Run e2e tests
   command: yarn e2e:ci
- store_test_results:
   path: /tmp/test-results
```

Modify the npm script as follows:

```
“e2e:ci”: “testcafe chrome:headless e2e/*.js — app ‘yarn serve:build’ -r xunit:/tmp/test-results/res.xml”
```

## See the summary on your dashboard

![img](https://miro.medium.com/max/60/0*eCsKR5D5MlE2h7dN?q=20)

![img](https://miro.medium.com/max/630/0*eCsKR5D5MlE2h7dN)

## Be proud! Add badges to your readme:

```
[![CircleCI](https://circleci.com/gh/proustibat/xke-introduction-testcafe/tree/master.svg?style=svg&circle-token=49a7ca92ed8ebbd224600c4c57b5718c12057102)](https://circleci.com/gh/proustibat/xke-introduction-testcafe/tree/master)[![Tested with TestCafe](https://img.shields.io/badge/tested%20with-TestCafe-2fa4cf.svg)](https://github.com/DevExpress/testcafe)
```

![img](https://miro.medium.com/max/60/0*qTdFk3kLX3GnIy7K?q=20)

![img](https://miro.medium.com/max/430/0*qTdFk3kLX3GnIy7K)

## Now CircleCI is running for each pull request

![img](https://miro.medium.com/max/60/0*8S8_BdlVE1THhu6q?q=20)

![img](https://miro.medium.com/max/630/0*8S8_BdlVE1THhu6q)

# Some features you should be aware of

## Intercepting HTTP requests

**Logging HTTP Requests:**

[RequestLogger](https://devexpress.github.io/testcafe/documentation/test-api/intercepting-http-requests/logging-http-requests.html#creating-a-logger) is a hook that can be attached to either a test or a fixture. It allows to record sent or received requests.

For example, here we record http request accessing an article with a get method. Then we can use assertions to check the status code of the response:

**Mocking HTTP Responses**

We can also mock requests with the [RequestMock](https://devexpress.github.io/testcafe/documentation/test-api/intercepting-http-requests/mocking-http-requests.html#mocking-cross-domain-requests) hook.

Here, I added Google Analytics to our project. We don’t want to send the page view event to our GA dashboard when the navigation comes from our tests. So we mock the request by intercepting it and sending a fake gif:

## Framework-Specific Selectors

TestCafe team and community develop libraries of dedicated selectors for the most popular frameworks. So far, the following selectors are available.

- React
- Angular
- AngularJS
- Vue
- Aurelia

[Read the documentation](https://devexpress.github.io/testcafe/documentation/test-api/selecting-page-elements/framework-specific-selectors.html)

# **TestCafe Studio**

## A cross-platform IDE

- Create, edit and maintain end-to-end tests in a visual recorder without writing code. See Record Tests.
- Generates a report with overall results and details for each test after completion.
- Code Editor with syntax highlight, code completion and parameter hints.
- Write code from scratch, convert recorded tests to JavaScript to edit them later.

![img](https://miro.medium.com/max/60/0*2mrTURJMi2MzZF-H?q=20)

![img](https://miro.medium.com/max/630/0*2mrTURJMi2MzZF-H)

## Recording our first test

## Running with remote

## Recording our second test

## Code editor

# Links:

- Tech doc: https://devexpress.github.io/testcafe/
- TestCafe Studio: https://docs.devexpress.com/TestCafeStudio
- Continue the tests by yourself: https://github.com/proustibat/xke-introduction-testcafe
- The tested web app: https://xke-introduction-testcafe.surge.sh/

Find all technical articles by Xebia on blog.xebia.fr

[Publicis Sapient Engineering](https://medium.com/xebia-france?source=post_sidebar--------------------------post_sidebar--------------)

Publicis Sapient Engineering (anciennement Xebia) est la…



Thanks to Vincent Arrocéna. 

- [E2e Testing](https://medium.com/xebia-france/tagged/e2e-testing)
- [End To End Testing](https://medium.com/xebia-france/tagged/end-to-end-testing)
- [Testcafe](https://medium.com/xebia-france/tagged/testcafe)
- [React](https://medium.com/xebia-france/tagged/react)
- [Test Automation](https://medium.com/xebia-france/tagged/test-automation)



[![Jennifer Proust (ג'ניפר פרוסט)](https://miro.medium.com/fit/c/72/72/1*FbbEjoC85JeO6gr5PJ0RzA.jpeg)](https://proustibat.medium.com/?source=follow_footer-----766ddbd74924-----------------------------------)WRITTEN BY[Jennifer Proust (ג'ניפר פרוסט)](https://proustibat.medium.com/?source=follow_footer-----766ddbd74924-----------------------------------)Follow

Senior frontend developer

[![Publicis Sapient Engineering](https://miro.medium.com/fit/c/160/160/1*dEcC7KB83eZWk15A1pP27Q.png)](https://medium.com/xebia-france?source=follow_footer-----766ddbd74924-----------------------------------)[Publicis Sapient Engineering](https://medium.com/xebia-france?source=follow_footer-----766ddbd74924-----------------------------------)Follow



Medium is an open platform where 170 million readers come to find insightful and dynamic thinking. Here, expert and undiscovered voices alike dive into the heart of any topic and bring new ideas to the surface. [Learn more](https://medium.com/about?autoplay=1&source=post_page-----766ddbd74924-----------------------------------)

[Make Medium yours.](https://medium.com/topics?source=post_page-----766ddbd74924-----------------------------------)

Follow the writers, publications, and topics that matter to you, and you’ll see them on your homepage and in your inbox. [Explore](https://medium.com/topics?source=post_page-----766ddbd74924-----------------------------------)

[Write a story on Medium.](https://medium.com/creator-tools?source=post_page-----766ddbd74924-----------------------------------)

If you have a story to tell, knowledge to share, or a perspective to offer — welcome home. It’s easy and free to post your thinking on any topic. [Start a blog](https://medium.com/creator-tools?source=post_page-----766ddbd74924-----------------------------------)