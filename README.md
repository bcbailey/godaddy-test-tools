# godaddy-test-tools

`gulp` tools for testing node libraries with mocha and istanbul as well as linting using [`godaddy-style`](https://github.com/godaddy/javascript).

### Usage
```
npm install --save-dev godaddy-test-tools
```

... add the package to your `gulpfile.js`
```js
'use strict';

var gulp = require('gulp');
require('godaddy-test-tools')(gulp, {
  // change any of the options listed below as needed
});

// define other gulp tasks or override already defined tasks as desired
```

... or `gulpfile.babel.js` if you are using ES6
```js
import testTools from 'godaddy-test-tools';
import gulp from 'gulp';

testTools(gulp, {
  // change any of the options listed below as needed
});

```

Running `gulp help` will show all the tasks and a description (if provided) for each of the tasks.


### Options
 - es6: Specifies that your code is written in ES6 (+ JSX). You must also name your gulpfile `gulpfile.babel.js`. Defaults to `false`.
 - reporter: The reporter to use for mocha. default: `process.env.MOCHA_REPORTER || 'spec'`
 - sourceFiles: The source files that will be watched and code coverage. default: `lib/**/*.js`
 - unitTestFiles: A glob-able path(s) to all the unit test files. default: `test/unit/**/*.js`
 - integrationTestFiles: A glob-able path(s) to all the integration test files. defaut: `test/integration/**/*.js`
 - functionalTestFiles: A glob-able path(s) to all the functional test files. defaut: `test/functional/**/*.js`
 - istanbul: Options for [`gulp-istanbul`](https://www.npmjs.com/package/gulp-istanbul)
 - watchFiles: default: `[sourceFiles, unitTestFiles, integrationTestFiles, functionalTestFiles]`
 - lint:
    - filenameConvention: example: `{ type: (kebob, snake, camel), exclude: /regex/, files: ['lib/**/*.js', 'test/**/*.js'] }`
    - files: a list of glob-able file paths to include in the lint checks.
        default:
        ```js
          [
            sourceFiles,
            unitTestFiles,
            integrationTestFiles,
            functionalTestFiles,
            'index.js',
            'main.js',
            'gulpfile.js',
            'gulpfile.babel.js',
            'config/**/*.json',
            'config/**/*.js',
            'lib/**/*.json',
            'test/**/*.json'
          ]
        ```
    - eslint: the argument passed to [`gulp-eslint`](https://www.npmjs.com/package/gulp-eslint). default: `require.resolve('godaddy-style/dist/es5/.eslintrc')`.
    - jshint: the argument passed to [`gulp-jshint`](https://www.npmjs.com/package/gulp-jshint). default: `require.resolve('godaddy-style/dist/.jshintrc')`.
    - jscs: the argument passed to [`gulp-jscs`](https://www.npmjs.com/package/gulp-jscs). default: `require.resolve('godaddy-style/dist/es5/.jscsrc')`.
      - reporter: optional: [fail, failOnError]
      - files: specify which files should be ran through jscs
          default:
          ```js
            [
              options.sourceFiles,
              options.unitTestFiles,
              options.integrationTestFiles,
              options.functionalTestFiles,
              'index.js',
              'main.js',
              'gulpfile.js',
              'gulpfile.babel.js',
              'config/**/*.js'
            ]
          ```
    - default: change the default linter from `eslint`
    - linters: change which linters are run when calling `gulp lint`
    - eslintFailOnError: failure after the first lint error is found.
        default: fail after all files have been linted

This tool defaults to a specific folder structure, but the options above
allow for configuring that as needed:

```
your-project/
  build/
    coverage/
  lib/
  test/
    unit/
    integration/
    functional/
```

Additionally, this project will send system notifications through
[`node-notifier`](https://www.npmjs.com/package/node-notifier) when
there are errors in your tests and when tests have run successfully unless
you pass the `--no-notify` option.
