## Changelog
### 2.0.0
  - Major refactor of the guidelines

### 1.3.0
  - Added a CONTRIBUTING.md file that details how to structure Git commits in a
    Conventional ChangeLog format.

  - Added an ES6 compliant .jscsrc file - .jscsrc-es6.

  - Added an ES6 compliant .jshintrc-node file - .jshintrc-node-es6.

### 1.2.0
  - Changed a few options in JSHint and JSCS.
    - JSCS `maximumLineLength` is now set to `260`
    - JSHint `singleGroups` is now set to `false`

  - Removed the `.jshintrc` file.  Should use either `.jshintrc-browser` or
    `.jshintrc-node`.

### 1.1.0
  - Updated .editorconfig to support .go files and rearranged order

### 1.0.0
This is a major version change since some projects that previously passed with
0.16.0 may now fail.  Refer to issue #33 for more details.

  - Updated to work with JSHint 2.6.3 and JSCS 1.11.3.

  - Deprecated the global .jshintrc and split it into a browser specific one and
    a node specific one.

  - Updated to work with new options that are available in JSHint 2.6.3.

  - Moved all deprecated JSHint options out and now use JSCS instead.

### 0.16.0
  - Add .jsdoc-conf.json

### 0.15.0
  - Add .editorconfig file

### 0.14.0
  - Added new JSCS rule requireSpaceBeforeObjectValues.  Requires jscs-1.6.2

### 0.13.0
  - Added rules for scss-lint

### 0.12.4
  - Changed JSHint rule - `unsued` to `"vars"`.  Using `"strict"` or `true` was
    unrealistic.

### 0.12.3
  - Changed JSHint rule - `unused` to `false`.  Using `"vars"` was unrealistic.
  - Upping `maxparams` from `6` to `10`.

### 0.12.2
  - Change JSHint rule - unused

### 0.12.1
  - Added JSCS rule - requireSpaceAfterLineComment

### 0.12.0
  - Added section for conflict resolution
  - moved changelog into CHANGELOG.md

### 0.11.2
  - Add details about RC files

### 0.11.1
  - Closes issue #13 - Set name of repository to MTS...

### 0.11.0
  - Added reference to the [airbnb guide][airbnb]
  - Changed title of page to be space delimited, not dash delimited
  - Changed [idiomatic.js][idiomatic] link reference to use a label instead of
    being inline
  - Alphabetized the link references at the bottom of this document
  - Added Markdown section.
  - Changed this document to match the Markdown guidelines.

### 0.10.0
  - Added Changelog and version number

### 0.9.0
  - Added if/else example in JavaScript code example

### 0.8.0
  - Change to Contributors
  - Added Original Authors

### 0.7.1
  - Fixed typo

### 0.7.0
  - Fixed typo
  - Clarity on JavaScript milliseconds
  - More details on HTML for quotes and whitespace

### 0.6.0
  - Changed Maintainers to Contributors
  - Markdown cleanup

### 0.5.0
  - Updates to JavaScript code example
  - Added details for JavaScript object literals
  - Added details for JavaScript milliseconds

### 0.4.0
  - Updates to HTML guidelines
  - Updates to CSS / SASS guidelines

### 0.3.0
  - Added HTML guidelines
  - Added CSS / SASS guidelines

### 0.2.0
  - Added exceptions over idiomatic for unit testing

### 0.1.0
  - Initial version
