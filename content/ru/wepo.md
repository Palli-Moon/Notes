WEPO - Web Programming II
====
Notes from the web programming II course (wepo) spring 2015.

###### Feb 2, 2015

## npm
### Installing
``` javascript
npm install -g <toolname>
```
The `-g` flag installs the tool globally, rather than for the current project only. It should be used sparingly, most tools should be installed on a project to project basis.

### package.json

A `package.json` file can be created in the project directory listing what packages the project uses.

If a `package.json` file exists, simply running `npm install` will install all the packages specified in the file.

Running the command `npm init` will allow npm to guide you through creating the `package.json` file opting for sensible default options.

By using the `--save-dev` flag when installing a tool with npm, it will automatically add it to the `package.json` dependency list. This is not always recommended since some packages may get updated frequently and manually writing in the version (or range of versions), may be preferred.


## Grunt
Grunt is a taskrunner that can create automated tasks for a project. Grunt should be specified in the `package.json` file and the cli can then be installed using the command below.
``` javascript
npm install -g grunt-cli
```
The Grunt cli is not the Grunt application in itself. It's only a *command-line interface*, used to run the Grunt application located in the project's directory. It should therefore be installed with the `-g` flag.

It is possible to run Grunt without installing the cli by running `node -e "require('grunt').tasks(['test']);"`, substituting `test` with the task(s) to run. For obvious reasons it is in most cases easier to just install the cli.

### The Gruntfile
The `Gruntfile` should then be created as `Gruntfile.js` or `Gruntfile.coffee` in the root of the project. The `Gruntfile` contains every task that should be runnable in the project. An example of a very basic `Gruntfile` with a jshint task would be:
``` javascript
module.exports = function(grunt) {
    grunt.loadNpmTasks('grunt-contrib-jshint');
    var taskConfig = {
        jshint: {
            src: ['**/*.js'],
            gruntfile: ['Gruntfile.js'],
            options: {}
        }
    };
    grunt.initConfig(taskConfig);
};
```
This Grunt task would run jshint (provided it's installed in the project) on every JavaScript file (`*.js`), in every folder (`**`) in the project.

## Notes
### File structure
When creating large JavaScript applications it's conventional to keep all the source code in a directory named `src`. This separates the application code from configure files like the `package.json` file, or `Gruntfile`. If the code is somehow compiled (or perhaps  concatenated/minified/uglified), the resulting code would then go to a `dist` folder on the same level as `src`. If the application has any unit tests available, they are typically located in a `test` folder.

### SemVer
Semantic versioning (SemVer) is a pattern for versioning projects. It contains three numbers written as `1.2.3` where `1` would be the **major** version, `2` the **minor** and `3` the **patch**. Services like Grunt use this heavily and most of them support using the `~` and the `^` prefixes. The `~` means any patch up to the next minor version, e.g. `~1.2.7` would allow any version between `1.2.7` and `1.3.0`. `^1.2.7` then means any minor version up to the next major version, or anything below `2.0.0`

Read more: http://semver.org/

### CDN
Content delivery networks (CDN) are away of including a library (especially JavaScript ones) into your project without actually downloading it. Services such as google provide hosting for these libraries and make it easy for people to add some jQuery, for instance, into their project quickly. This may make site loading a bit slower however and should therefore not be used as a long-term solution for large projects.

JavaScript CDN: https://cdnjs.com/

### Links
http://tech.pro/blog/1402/five-patterns-to-help-you-tame-asynchronous-javascript

###### Feb 5, 2015

## JavaScript libraries
### Underscore.js
[Undescore](http://underscorejs.org/) has a collection of utility functions adding functional aspects to JavaScript.

Underscore was recently forked and now has an alternate version called [lodash](https://lodash.com/), which may currently be in more active development.

[Some differences between the two libraries](http://benmccormick.org/2014/11/12/underscore-vs-lodash/).

The name comes from the fact that all the utility functions use the underscore (or low dash) in front of them. Example:
```javascript
_.each( arr, function(i) {
    sum += i;
}
```

### Template libraries
The two most active template libraries are currently [mustache](https://mustache.github.io/) and [handlebars](http://handlebarsjs.com/). They are used to set up a template for data to be injected into. In the below example the item between the double curly brackets `{{}}`

``` html
<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{body}}
  </div>
</div>
```

### Module libraries
Used to aid large projects in requiring dependencies properly. Examples of this are [RequireJS](http://requirejs.org/) and CommonJS.

###### Feb 10, 2015

## AngularJS
Angular apps typically start by declaring the global `angular.module("MyApp", [dependencies])`, where *dependencies* is an array of dependencies. This binds the JavaScript code to the html contained in the `ng-app="MyApp"` directive, usually defined on the `<html>` element. Angular uses these directives to enhance html elements. The module created at the top of the document is then used throughout the code i.e. `angular.module("MyApp").controller(...)`.

### $scope
The $scope objects acts as a sort of link between the Angular controller and the view. Using scope one can send information from the controller to the view.

``` javascript
# Javascript file
angular.module("MyApp").controller("testcontroller",
function testcontroller($scope) {
    $scope.message = "Hello";
});
```

``` html
# Html file
<div ng-controller="testcontroller">
    {{message}}
</div>
```

$scope can also carry more complex information, such as an object. The html end then uses a similar syntax as the handlebars templating library to display the data.

### Links
A few Angular related links.
* [A few short videos on Angular and other services](https://egghead.io/)
* [A todo app written in Angular](https://www.youtube.com/watch?v=WuiHuZq_cg4)
* [End to end tutorial](https://www.youtube.com/watch?v=Ja2xDrtylBw)
* [Some good Angular examples](http://www.angularjshub.com/examples/)
* [A tutorial on Angular and others](https://thinkster.io/)
* [Angular cheat sheet](http://www.cheatography.com/proloser/cheat-sheets/angularjs/)

###### Mar 2, 2015
## Unit Testing
Unit tests should be single responsibility, meaning each test should only test one thing. All statement of the following types should be tested:
* branch statements (if-else)
* loops
* assignments (especially calculations)

Ideally unit tests should have 100% code coverage, i.e. they should cover all code paths.

### Test tools
Karma is a test runner, while Jasmine is a test framework. 

```
npm install -g karma
```

PhantomJS is good for testing in a windowsless browser.

```
npm install -g phantomjs
```

Karma can be combined with [grunt](https://github.com/karma-runner/grunt-karma).

### Karma
What tests are run etc. is specified in the `karma.config.js` file.

The file can be generated with the command
```
karma init
```

### Jasmine
A [Jasmine](http://jasmine.github.io/) test suite often use the *.spec.js extension. It uses the `describe(description, function)` function to wrap the suite and a description should be written inside to describe it's purpose.

``` javascript
describe("Main test suite", function() {
	// Tests go here
});
```
Each test module should only test a single entity, such as a controller or a complex function.

Each test is then described using the `it(description, function)` function. A test could therefore look something like

``` javascript
it("Test if a is equal to b", function() {
	var a = 12;
	var b = a;
	expect(a).toBe(b);
}
```
The test itself simply checks if the values are what it expects them to be. A lot more functions exist in jasmine for testing.

`beforeEach(function)` and `afterEach(function)` can be used to run before and after each `it()`. This is a good place to create objects and other things that need initialization or cleanup. An example of this would be

``` javascript
var obj
beforeEach(function() {
	obj = new Obj();
}
```
If `beforeEach()` had not been used the `obj` object would have to have been created for each `it()`.

To check if a function has been called the `spyOn(object, "function-name")` function can be use in conjunction with `toHaveBeenCalled()` or `toHaveBeenCalledWidth(parameter, ...)` to check if it was called with the expected parameters.

The `spyOn()` function checks for event on the given function while `toHaveBeenCalled()` will pass as long as the function was actually called.