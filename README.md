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

    var thirteen = (39 * 2) / 6;

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
            .enter()
            .append('svg:svg')
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

        // first, create a jQuery instance of the html template string passed in
        $element = $(template);

        if (isFancy) {
            // if the element is supposed to be fancy, add a class
            $element.addClass('fancy');
        }

        return element;
    }
    ```

## HTML
- #### Semantic Tags:
Use semantic tags in the way they were intended!  
Here is a brief glossary of terms:

    ```html
    <section>

    - A meaningful division of content - every major group
    of content in between a header and footer
    ```

    ```html
    <header>

    - The header for a section
    ```

    ```html
    <footer>

    - The footer for a section
    ```

    ```html
    <article>

    - A full article
    ```

    ```html
    <nav>

    - Navigation! Main site navigation, contextual navigation -
    used for accessing site contents
    ```

    ```html
    <aside>

    - Elements that exist outside of the normal page
    flow/reading flow. Sidebars, related content, etc.
    ```

    ```html
    <cite>

    - A citation- used for references or bylines
    ```

    ```html
    <figure>

    - An image, illustration, or graph that is used as
    a meaningful piece of content
    ```

    ```html
    <figcaption>

    - The contextual caption for a <figure>
    ```

- Example markup using semantic tags:

    ```html
    <!-- EXAMPLE MARKUP -->
    <section class="recent-articles">
        <header>Most Recent Article</header>

        <nav>
            <a href="#allthearticles">Load all articles</a>
        </nav>

        <article>
            <h2>The Most Important Article</h2>

            <figure>
                <img src="/someimage.jpg" />

                <figcaption>Fig. 1 - This image explains everything!</figcaption>
            </figure>

            <cite>By Antonio Banderas</cite>

            <p>
                This is the article copy. It's pretty short because
                this is an example, and not for the internet at large.
                Remember, words are important!
            </p>
        </article>

        <footer>
            <a href="#signup">Sign up for our newsletter!</a>
        </footer>
    </section>
    ```

- #### Structural elements
    It is sometimes necessary to wrap HTML in tags that are structural, and have no direct impact on the content presented.
    This is totally fine, but keep it clean!

    In the example below, we have a UI that contains two buttons and a paragraph
    of text that is output based on some kind of user interaction. On a small screen (or small space), the buttons and
    the output text can stack vertically (think, display: block down the page).

    On a larger screen, however, we may want these groups of elements to go 50/50 to better occupy screen real-estate.

    In this type of case, we can semantically divide our html into two "ui-group"s, allowing us the flexibility required to make a nice app.

    ````html
    <section class="admin-tool">
        <div class="ui-group">
            <button>Button 1</button>
            <button>Button 2</button>
        </div>

        <div class="ui-group">
            <p>
                This is a read-out of some kind of
                admin tool. Clicking those buttons
                affects the text!
            </p>
            <a href="#reload">Reload That Text!</a>
        </div>
    </section>
    ```

- #### Syntax
    - **Always** use semantic tags!
    - **Always** use doublequotes for attributes!
    - **Always** use proper indentation (keep your structure sane!)
    - **Always** make your html human-readable
    - **Never** use an #id for styling hooks
    - **Never** use **tables** for layout
    - Closing `<li>` elements.
      `<li>` elements should not be closed. [Further reading on this inline-block
      issue.][inline]
    - Each new tag should exist on its own line!
    ```html
    <!-- BAD! NO! -->
    <div class="thing">
        <section><h1>Title</h1>
        <a href="thing">Things are happening <span>here</span></a></section>
    </div>

    <!-- Ah! Room to breathe, and now the structure is apparent. -->
    <div class="thing">
        <section>
            <h1>Title</h1>

            <a href="thing">
                Things are happening
                <span>here</span>
            </a>
        </section>
    </div>
    ```
    - Separate independent but loosely related snippets of markup with a single empty line, for example:

        **EXCEPTION:** For inline block styling, items may need to live on the same line. Acceptable
        deviance is inserting html comments to eliminate the inline-block space.

    ```html
    <!-- THIS IS FINE, SINCE THESE TITLES AND PARAGRAPH ARE RELATED -->
    <div class="thing">
        <h1>Title</h1>
        <h2>Title 2</h2>
        <p>Things</p>
    </div>

    <!-- THIS IS ALSO FINE, GROUPS HEADLINES TOGETHER, AND SEPARATES THE PARAGRAPH -->
    <div class="thing">
        <h1>Title</h1>
        <h2>Title 2</h2>

        <p>Things</p>
    </div>

    <!-- THIS IS NOT FINE! DISTINGUISHES THESE ELEMENTS UNNECESSARILY -->
    <div class="thing">

        <h1>Title</h1>

        <h2>Title 2</h2>

        <p>Things</p>

    </div>

    <!-- SEPARATES LARGER "CHUNKS" OF HTML FOR EASE OF TRACKING -->
    <div class="thing">
        <nav>
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
        </nav>

        <h2>Title</h2>

        <figure>
            <img src="image.jpg"/>
            <figcaption>Caption for the image</figcaption>
        </figure>
    </div>
    ```

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
