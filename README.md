# JUnit Reporter for Cypress

Produces JUnit-style XML test results.

## Installation

```shell
$ npm install cypress-junit --save-dev
```

or as a global module
```shell
$ npm install -g cypress-junit
```

## Usage
```javascript
// cypress.json
{
  "reporter": "cypress-junit",
  "reporterOptions": {
    "mochaFile": "./path_to_your/[hash].xml",   
    "toConsole": true,
    "outputs": true
  }
}
```

### Results Report
### System out and system err
The JUnit format defines a pair of tags - `<system-out/>` and `<system-err/>` - for describing a test's generated output
and error streams, respectively. It is possible to pass the test outputs/errors as an array of text lines:
```js
it ('should report output', function () {
  this.test.timings.consoleOutputs = [ 'line 1 of output', 'line 2 of output' ];
});
it ('should report error', function () {
  this.test.timings.consoleErrors = [ 'line 1 of errors', 'line 2 of errors' ];
});
```
### Attachments
enabling the `attachments` configuration option will allow for attaching files and screenshots in [JUnit Attachments Plugin](https://wiki.jenkins.io/display/JENKINS/JUnit+Attachments+Plugin) format.

Attachment path can be injected into the test object
```js
it ('should include attachment', function () {
  this.test.timings.attachments = ['/absolut/path/to/file.png'];
});
```

If both attachments and outputs are enabled, and a test injects both consoleOutputs and attachments, then
the XML output will look like the following:
```xml
<system-out>output line 1
output line 2
[[ATTACHMENT|path/to/file]]</system-out>
```

### Full configuration options

| Parameter | Effect |
| --------- | ------ |
| mochaFile | configures the file to write reports to |
| includePending | if set to a truthy value pending tests will be included in the report |
| properties | a hash of additional properties to add to each test suite |
| toConsole | if set to a truthy value the produced XML will be logged to the console |
| useFullSuiteTitle | if set to a truthy value nested suites' titles will show the suite lineage |
| suiteTitleSeparedBy | the character to use to separate nested suite titles. (defaults to ' ') |
| testCaseSwitchClassnameAndName | set to a truthy value to switch name and classname values |
| rootSuiteTitle | the name for the root suite. (defaults to 'Root Suite') |
| testsuitesTitle | the name for the `testsuites` tag (defaults to 'Mocha Tests') |
| outputs | if set to truthy value will include console output and console error output |
| attachments | if set to truthy value will attach files to report in `JUnit Attachments Plugin` format (after console outputs, if any) |
| antMode | set to truthy value to return xml compatible with [Ant JUnit schema][ant-schema] |
| antHostname | hostname to use when running in `antMode`  will default to environment `HOSTNAME` |
| jenkinsMode | if set to truthy value will return xml that will display nice results in Jenkins |

[travis-badge]: https://travis-ci.org/michaelleeallen/mocha-junit-reporter.svg?branch=master
[travis-build]: https://travis-ci.org/michaelleeallen/mocha-junit-reporter
[npm-badge]: https://img.shields.io/npm/v/mocha-junit-reporter.svg?maxAge=2592000
[npm-listing]: https://www.npmjs.com/package/mocha-junit-reporter
[ant-schema]: http://windyroad.org/dl/Open%20Source/JUnit.xsd

## Fork
this GIT is forked from `michaelleeallen/mocha-junit-reporter`