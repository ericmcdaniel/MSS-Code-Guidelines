# MTS Code Guidelines
Version 1.3.0

![I honestly didn't think you could even USE emoji in variable names. Or that there were so many different crying ones.](http://imgs.xkcd.com/comics/code_quality.png)

## JavaScript
The JavaScript guidelines are based off of [idiomatic.js][idiomatic].

For lots of code examples that show the style we want, see the
[airbnb guide][airbnb].

The MSS Guidelines will be the same with the following additional rules applied.


### Test Facility
We will be using:

- Mocha / Chai for unit tests
- Selenium (WebdriverJS) / Mocha / Chai for functional tests
- PhantomJS / CasperJS for functional tests


### Idiomatic Style Manifesto
- #### Whitespace
    - 4-space soft indents are required.  This means four spaces or four spaces
      representing a tab.
    - Place 1 space before the leading brace and 1 space before the parentheses in control statements (if, else, while, for)
    ```javascript
    if (things) {
        alert('Look how nice that space is!');
    }
    ```
    - Place no spaces before the arguments list in a function declaration.
    ```javascript
    function makeSandwich(ham, cheese, egg) {
        return ham + cheese + egg;
    }
    ```
    - Set off operators with spaces
    ```javascript
    var value = a + b + c;

    var thirteen = 39 * 2 / 2 / 3;

    ```
    - User indendation when making long method chains (a la underscore/lodash, d3.js, etc.). Use a leading dot, which emphasizes that the line is a method call, not a new statement.
    ```javascript
    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
            .attr('width', (radius + margin) * 2).append('svg:g')
            .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
            .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
            .data(data)
            .enter().append('svg:svg')
            .classed('led', true)
            .attr('width', (radius + margin) * 2)
            .append('svg:g')
            .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
            .call(tron.led);
    ```
    - Leave a blank line after blocks and before the next statement.
    ```javascript
    // bad
    if (foo) {
        return bar;
    }
    return baz;

    // good
    if (foo) {
        return bar;
    }

    return baz;

    // bad
    var obj = {
        foo() {
        },
        bar() {
        },
    };
    return obj;

    // good
    var obj = {
        foo() {
           },

        bar() {
        },
    };

    return obj;
    ```
- #### Declarations
    - Assign variables where you need them, but place them in a reasonable place.

    *Why?* This will help others maintain context when reading long code blocks.

    ```javascript
    function doTwoThings() {
        var thingone = 1;

        thingone++;

        var thingtwo = true;

        if (thingtwo) {
            thingone++;
        }
    }
    ```
    - Use single quotes for strings!
    ```javascript
    var myNameIs = 'Slim Shady';
    ```
    - Object literals should look like this:
    ```javascript
    var objectLiteral = {
        foo: 'bar',
        baz: 'qux'
    };
    ```
    - Milliseconds should be assigned in multiples of 1000, and always use
      explicit order of operations.
    ```javascript
    var oneSecond = 1000 * 1,
        oneMinute = 1000 * 60,
        fiveMinutes = (1000 * 60) * 5;
    ```
    - Use a leading underscore _ when naming private properties.
    ```javascript
    // BAD! NO!
    this._things_
    this.things_
    this.THINGS

    // GOOD!
    this._things = 'private';
    ```


- #### Naming
    - Use camel-case for variable and function names
    ```javascript
    var thisVariableIsCamelCase = true;

    function doSomethingGreat(isGreat) {
        if (isGreat) {
            alert('Pretty good!');
        }
    }
    ```
    - Be descriptive with your function and variable names!
    ```javascript
    // BAD! wtf man
    var nState = nStateOnLoad();

    // GOOD!
    var navigationState = getNavigationState();
    ```
    - Prefix jQuery selection variables with '$'
    ```javascript
    // BAD!
    var navigationLinks = $('nav a');

    // GOOD!
    var $navigationLinks = $('nav a');
    ```

- #### Comments
    - Use JSDoc-style comments to describe methods and functionality
    ```javascript
    /**
     * make() returns a new element
     * based on the passed in tag
     *
     * @param {String} tag
     * @return {Element} element
     */

    function make(tag) {
        // some code
        return element;
    }
    ```
    - Please use single line comments to describe how your code works! Debugging issues can be very difficult if it's unclear how a block of code works or what certain conditionals are for. Be kind to future devs!
    ```javascript
    function make(template) {
        var $element,
            isFancy;

        // first, create a jQuery instance of the tag passed in
        $element = $(template);

        if (isFancy) {
            // if the element is supposed to be fancy, add a class
            $element.addClass('fancy');
        }

        return element;
    }
    ```

## HTML
- Write clean semantic HTML5 markup.
0. Use double quotes for attributes.
0. Use proper indention.
0. Selector Attributes
  Never use an ID as a styling hook.
  Prefix any JavaScript class hooks with `js-`. Example: `class="js-foo foo"`
0. Closing `<li>` elements.
  `<li>` elements should not be closed. [Further reading on this inline-block
  issue.][inline]


## CSS / Sass
0. The CSS / Sass guidelines are based off of [csswizardry/CSS-Guidelines][css].
0. We use [nomalize.css][normalize] as our style reset.


#### Our CSS / Sass overrides
0. Declarations.
  Declarations should be in aplhabetical order (**NOT** by relevance).


## Markdown
0. All lines that are not code blocks should wrap at or under 80 columns.
0. Should allow trailing whitespace, since that is a valid Markdown syntax.
0. Should have 2 blank lines above each H1 and H2 heading except for the
   heading at the top of the document.  This is optinal for other headings.
0. Should have 4 blank lines to separate the link reference at the bottom of
   the document.
0. Should use `0.` for ordered lists
0. Should use `-` for unordered lists
0. Secondary bullets must be indented four spaces to render correctly on
  Bitbucket.
0. Do not try to put code blocks as secondary bullets in a list.  They will not
  render correctly on both GitHub and BitBucket. More details on this to come
  in the future.

 ## Contributors
 **YOU!** - please contribute to these code guidelines! If you have any
 suggestions for improvement to these guidelines, *[create an issue][issue]* to
 discuss it or *create a [pull request][pr]* with your changes and discussion
 will occur on that PR.  Also review the [contributing guidelines](https://github.com/TurnerBroadcasting/mss-code-guidelines/blob/master/CONTRIBUTING.md).


 ### Original Authors
 - James Young [@jamsyoung](http://twitter.com/jamsyoung), [github](https://github.com/jamsyoung)
 - Matt Crutchfield [@mtcrutch](https://twitter.com/mtcrutch), [github](https://github.com/mtcrutch)


 ## Conflict Resolution
 We have included [JSHint][jshint] and [JSCS][jscs] RC files in this repository
 to validate javascript code against these guidelines.  When something is
 questioned, these files will always win.  When in doubt, run JSHint and JSCS
 with the `.jshintrc` and `.jscsrc` files in place and see if they find any
 problems.  It is recommended that you find plugins for your editor of choice to
 always validate your code against these files.

 ### Regarding the multiple suffixed files
 There are several `.jscs` and `.jshintrc` files with suffixes in this repo.  It
 is up to you to choose the most appropriate one for your project.  Hopefully the
 suffixes are clear, but just in case, here are some more details.

 - **.jscs**: A JavaScript Code Style config file for ECMAScript 5 code.

 - **.jscs-es6**: A JavaScript Code Style config file for ECMAScript 6 code.

 - **.jshintrc-browser**: A JS Hint config file for browser based ECMAScript 5
   code.

 - **.jshintrc-node**: A JS Hint config file for NodeJS 0.10.x ECMAScript 5 code.

 - **.jshintrc-node-es6**: A JS Hint config file for NodeJS 0.11.x+ and IO.js
   ECMAScript 6 code.





[airbnb]: https://github.com/airbnb/javascript
[css]: https://github.com/csswizardry/CSS-Guidelines
[idiomatic]: https://github.com/airbnb/javascript
[inline]: http://css-tricks.com/fighting-the-space-between-inline-block-elements/
[issue]: https://github.com/TurnerBroadcasting/MTS-Code-Guidelines/issues/new
[jscs]: https://github.com/mdevils/node-jscs
[jshint]: https://github.com/jshint/jshint/
[normalize]: http://necolas.github.io/normalize.css/
[pr]: https://github.com/TurnerBroadcasting/MTS-Code-Guidelines/compare/
