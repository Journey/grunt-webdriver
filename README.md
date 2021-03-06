# grunt-webdriver [![Build Status](https://travis-ci.org/christian-bromann/grunt-webdriver.png)](https://travis-ci.org/christian-bromann/grunt-webdriver)

> grunt-webdriver is a grunt plugin to run selenium tests with BusterJS and webdriverjs

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out
the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains
how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as
install and use Grunt plugins. Once you're familiar with that process, you may
install this plugin with this command:

```shell
npm install grunt-webdriver --save-dev
```

One the plugin has been installed, it may be enabled inside your Gruntfile
with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-webdriver');
```

## The "webdriver" task

### Overview
In your project's Gruntfile, add a section named `webdriver` to the data
object passed into `grunt.initConfig()`.

_Run this task with the `grunt webdriver` command._

```js
grunt.initConfig({
  webdriver: {
    dev: {
      url: '<start-url>',
      tests: ['<path-to-your-testfiles>']
    }
  },
})
```

### Options

#### browser
Type: `String`<br>
Default: *chrome*<br>
Options: *chrome* | *firefox* | *opera* | *safari* | *phantomjs*

Defines the browser. If [PhantomJS](http://phantomjs.org/index.html) (`>v1.8`) is installed, you
can run your Selenium tests in a headless browser. These tests are much faster as standard
browser tests.

#### reporter
Type: `String`<br>
Default: *dots*<br>
Options: *dots* | *specification* | *quiet* | *xml* | *tap* | *html* | *teamcity*

Reporters visualize progress and results of test runs. Some are desired for continious integration
tests. Find more information in the BusterJS [documentation](http://docs.busterjs.org/en/latest/modules/buster-test/reporters/#buster-test-reporters).

#### output
Type: `String`<br>

Define a path to save the test output from the buster reporters.

#### logLevel
Type: `String`<br>
Default: *silent*<br>
Options *silent* | *verbose*

Set log level of webdriverjs API

#### binary
Type: `String`<br>
Default: standard MacOSX browser path (e.g. Chrome: /Applications/Google Chrome.app/Contents/MacOS/Google Chrome)

Specify the binary path for the indicated browser __(important for windows user)__

### Usage Examples

#### Required Options
In this example, the minimum required options are used to execute a simple
test script.

```js
grunt.initConfig({
  webdriver: {
    dev: {
      url: 'http://github.com',
      tests: './test/github-test.js'
    }
  },
})
```

The corresponding *Hello World* test script, using webdriverjs API to search the
grunt-webdriver repository on GitHub. See more functions and test examples
in the [webdriverjs](https://github.com/Camme/webdriverjs) repository.

```js
'use strict';

exports.name = "Simple Github Test";

exports.setUp = function(){
    // ...  
};

exports.tests = [{
    
    name: "checks if title contains the search query",
    func: function(done) {

        var query = 'grunt-webdriver';
        exports.driver
            .click('.search a')
            .setValue('.search-page-input',query)
            .click('#search_form .button')
            .getTitle(function(title) {
                buster.assertions.assert(title.indexOf(query) !== -1);
            })
            .end(done);
        
    }}
];

exports.tearDown = function() {
    // ...
}
```

## Contributing
Please fork, add specs, and send pull requests! In lieu of a formal styleguide, take care to maintain the existing coding style.

## Release History
* 2013-03-13   v0.1.1   first working version, without special features
* 2013-03-14   v0.1.2   bugfixing, enhanced task option, improved test case
* 2013-03-15   v0.1.3   added support for phantomjs, implemented reporter option
* 2013-03-16   v0.1.4   save result of busterjs reporters to a file, use travis for CI testing
* 2013-03-16   v0.1.5   added support for setUp function
* 2013-03-16   v0.1.6   fixed webdriverjs version

