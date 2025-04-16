[![Endpoint Badge](https://img.shields.io/endpoint?url=https%3A%2F%2Fobservability.browserstack.com%2Fprojects%2FTest%2BObservability%2BSamples%2Fbuilds%2Fwdio-cucumber-samples%2F235&link=https%3A%2F%2Fobservability.browserstack.com%2Fprojects%2FTest%2BObservability%2BSamples%2Fbuilds%2Fwdio-cucumber-samples%2F235)](https://www.abc.com)

[**BrowserStack Test Observability**](https://www.browserstack.com/test-observability) is a next generation tool which brings together test reporting, precision debugging, flaky test detection and more... all on the same easy to use dashboard.

Test Observability works regardless of if your tests run on BrowserStack, your local machine, or other cloud infrastructure platforms.

![example-test-observability](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMWY0N2NhMjQ2NmRlMzE2ZDljYWYzZmI3Mzc4OGIyMmZmZTgwOWZmMSZjdD1n/Kyd7wYJAANRu6vS2R8/giphy.gif)  


Overview
========
- **Rich Build Insights**: Get better visibility into every single build, and your entire test suite with advanced analytics. Make better decisions with historical data on what tests are failing, flaky or slow.

- **Timeline Debugging**: Time-travel through your test runs with consolidated logs from multiple sources in one single dashboard.

- **Flaky Test Detection**: Automatic detection of flaky tests. Fix flakiness with intelligent suggestions.

- **Seamless Test Re-Runs**: Trigger test re-runs for individual tests or entire builds directly from BrowserStack Test Observability.

- **Smart Failure & Error Analysis**: Spend less time on debugging, as Test Observability intelligently identifies errors and tags tests with their causes of failure.

- **Effortless Integration**: Test Observability integrates with your existing test suite in minutes via the [wdio-browserstack-service](https://webdriver.io/docs/browserstack-service), with zero-code changes necessary.


Getting Started
===============
1. [Sign up](https://www.browserstack.com/users/sign_up?ref=observability) for a free BrowserStack account (no credit card needed!) if you don't already have one.

2. Copy your username and access key from your [account settings](https://www.browserstack.com/accounts/profile).

3. Install the [`@wdio/browserstack-service`](https://webdriver.io/docs/browserstack-service). Add it as a devDependency in your package.json, via:

```
npm install @wdio/browserstack-service --save-dev

# Use v7.30.1 or later if using WebdriverIO v7 or earlier.
# Use v8.x.x or later if using WebdriverIO v8.
```

4. Configure your `wdio.conf.js` file with code snippets from below depending on where your tests run - on any local or alternative cloud infrastructure, or on BrowserStack. 

5. Run your tests as usual, and visit the [Test Observability dashboard](https://observability.browserstack.com/) to instantly start analyzing and debugging your tests!

You can also [`Read more`](https://www.browserstack.com/docs/test-observability/quick-start/webdriverio#Tests_running_locally_or_elsewhere) in the BrowserStack documentation about how to get started with Test Observability.


Using Test Observability if your tests do not run on BrowserStack
----------------
You can use Test Observability even if you do not want to run your tests on the BrowserStack infrastructure. Your tests could be running on a CI or on your laptop or even on other cloud service providers like Sauce Labs, however, Test Observability will still work and give you all the intelligent test reports, debugging capabilities and advanced analytics you need!

You can set your config in the following manner if you do not want to run tests on BrowserStack Automate or App Automate (BrowserStack infrastructure), but still want to use Test Observability (note that `user` and `key` are now defined under the scope of the `browserstack` service). Ensure that the `testObservability` flag is set to `true`, and specify a static `projectName` and `buildName` under `testObservabilityOptions`. Test Observability will automatically recognize new builds of the same project/build name and start populating the dashboard with your builds when you run your tests.

```js
// wdio.conf.js
export const config = {
    // ...
    services: [
        ['browserstack', {
            testObservability: true,
            testObservabilityOptions: {
                user: process.env.BROWSERSTACK_USERNAME,
                key: process.env.BROWSERSTACK_ACCESS_KEY,
                projectName: "Your project name goes here",
                buildName: "The static build job name goes here e.g. Nightly regression"
            }
        }]
    ],
    // ...
};
```


Using Test Observability if your tests are already running on BrowserStack
----------------

If you are already running tests on BrowserStack, you likely already have the @wdio/browserstack-service set up. Ensure that the `testObservability` flag is set to `true`, and specify a static `projectName` and `buildName` under `testObservabilityOptions`. Test Observability will automatically recognize new builds of the same project/build name and start populating the dashboard with your builds when you run your tests.

```js
// wdio.conf.js
export const config = {
    // ...
    user: process.env.BROWSERSTACK_USERNAME,
    key: process.env.BROWSERSTACK_ACCESS_KEY,
    services: [
        ['browserstack', {
            testObservability: true,
            testObservabilityOptions: {
                projectName: "Your project name goes here",
                buildName: "The static build job name goes here e.g. Nightly regression"
            },
            browserstackLocal: true
        }]
    ],
    // ...
};
```

