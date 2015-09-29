# MTS Code Guidelines
Version 1.3.0

![I honestly didn't think you could even USE emoji in variable names. Or that there were so many different crying ones.](http://imgs.xkcd.com/comics/code_quality.png)

## About these guidelines

The central goal of this document is to create readable, consistent code across
web applications in MSS. While each application has its own constraints and needs,
it is helpful to think of your application as not only a business-critical application,
but also a tool for learning for all future developers!

### Table of contents
- [Javascript](#Javascript)
    - [Whitespace](#Whitespace)
    - [Declarations](#Declarations)
    - [Naming](#Naming)
    - [Comments](#Comments)
    - [Functions](#Functions)
- [HTML](#HTML)
    - [Semantic Tags](#SemanticTags)
    - [Structural Elements](#StructuralElements)
    - [Data Attributes](#DataAttributes)
    - [ID's](#IDs)
    - [Syntax](#Syntax)
- [CSS / SASS](#CSS)
    - [BEM](#BEM)
    - [Mobile First!](#MobileFirst)
    - [Separate structure, visual styles, and theming](#SeparateStructure)
    - [Default visual/theme styles](#DefaultStyles)
- [Markdown](#Markdown)
- [Contributing!](#Contributors)
- [Conflict Resolution](#ConflictResolution)
- [Included Files](#IncludedFiles)
- [Authors](#Authors)
- [Helpful Links](#HelpfulLinks)

## <a name="Javascript"></a>JavaScript
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
- #### <a name="Whitespace"></a> Whitespace
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
    - User indendtation when making long method chains (a la underscore/lodash, d3.js, etc.). Use a leading dot, which emphasizes that the line is a method call, not a new statement.
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
- #### <a name="Declarations"></a> Declarations
    - Use only one variable declaration, at the top of your function. Chain together with commas

    *Why?* Your functions should be short, and keeping the vars in one place is a good way to keep inventory as you read the function.

    ```javascript
    function doTwoThings() {
        var thingOne = 1,
            thingTwo = true;

        thingOne++;

        if (thingTwo) {
            thingOne++;
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

- #### <a name="Naming"></a> Naming
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
    // BAD! WHYYYY!!!
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

- #### <a name="Comments"></a> Comments
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
    - Please use single line comments to describe how your code works! Debugging issues can be very difficult if it's unclear how a block of code works or what certain conditionals are for. Be kind to future developers!
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
- #### <a name="Functions"></a> Functions
    - The general approach when writing a function is that any future developer (including yourself in six months) can read it like a human and know what is happening. Comments should not be your crutch for sense-making- a combination of clear naming conventions, conditionals that read like sentences, and simple explanations in comments where needed will help keep code clear and maintainable. Example:

    ```javascript
    function makeSandwich(bread, meat, veggies) {
        // check if the sandwich has veggies, has meat, and determines sandwich potential
        var hasVeggies = Array.isArray(veggies) && veggies.length > 0,
            hasMeat = Array.isArray(meat) && meat.length > 0,
            weCanMakeASandwich = (bread && (hasVeggies || hasMeat)) ? true : false,
            message = 'No dude you can\'t make a sandwich';

        // sets defaults for meat and veggies
        meat = hasMeat ? meat : [];
        veggies = hasVeggies ? veggies : [];

        // if we can make a sandwich, tell us what it is all about
        if (weCanMakeASandwich) {
            message = 'Mmmm about to eat a ' + bread + ', ' + meat.join(', ') + veggies.join(', ') + ' sandwich';
        }

        return message;    
    }
    ```

    - We like this function for several reasons:
        - The variable declarations contain all of the conditions we need to guarantee success.
        - All conditionals are consolidated, in an intentional order.
        - By using Booleans as our primary success criteria, we can write very readable execution code later on.
        - Tweaking the names of the variables lets us have human-readable conditionals ("if we can make a sandwich").
            - Originally, we had named this variable "canWeMakeASandwich", which, while readable, created an awkward sentence out loud.
        - A single return statement helps us reason about what this function outputs and when.
        - Always think about what you return- in a lot of cases, we can use this for chaining purposes.

    - And now, a very very bad example:
    ```javascript
    function sandwich(ingredient1, ingredient2, veggies) {
        var message = '';

        // check if there is bread, or if there is only bread
        if (typeof ingredient1 === 'undefined') {
            message = "You can't make a sandwich without bread!";
            return message;
        } else if (typeof ingredient2 === 'undefined' && typeof veggies === 'undefined') {
            message = "You can't make a sandwich with only bread!";
            return message;
        }

        // if ingredient 2 exists but isn't an array, set it to empty
        if (typeof ingredient2 === 'undefined' || !Array.isArray(ingredient2)) {
            ingredient2 = [];
        }

        // if veggies exists but isn't an array, set it to empty
        if (typeof veggies === 'undefined' || !Array.isArray(veggies)) {
            veggies = [];
        }

        // if either ingredient 2 or veggies is an empty array
        if (ingredient2.length === 0 && veggies.length === 0) {
            message = "You don't have enough ingredients to make a sandwich, sir."
            return message;
        }

        // tell user what sandwich is being made
        message = 'Mmmm about to eat a ' + ingredient1;

        // if ingredient 2 exists, add to sandwich
        if (ingredient2.length > 0) {
            message = message + ' ' + ingredient2.join(', ');
        }

        // if there are veggies, add to sandwich
        if (veggies.length > 0) {
            message = message + ' ' + veggies.join(', ');
        }

        message = message + " sandwich.";

        // if the message is not an empty string, return a message
        return message == '' ? 'No dude you can\'t make a sandwich' : message;
    }
    ```

    - Some notes on this thing:
        - First, sorry!
        - The function name and arguments are not very descriptive. Is sandwich even a verb??? WTF is ingredient2???
        - All of the conditionals you see were 'conditional' on our understanding of the parameters needed for the function to succeed. **tldr; We started with one, and quickly ballooned into this tangled web of logic.**
        - While this function returns a slew of "useful" error messages, the basic question of "can i make a sandwich" does not require such verbose treatment. **tldr; KEEP IT SIMPLE**
        - The first fifteen some odd lines of conditionals in this function were accomplished in FOUR in the first function. This was done by creating readable, boolean variables to keep track of the essential information needed to run the function.
        - By using poorly named variables and doing explicit checks in a sequence of if/else conditionals, it is very easy to lost context for what is happening.
        - Assembling the message over multiple lines means that any future updates to the output of this function will most likely break the meaning.
        - Many return statements makes it difficult to tell when/if the function will stop executing and what will happen when it does.
        - Comments! The comments in this function do not add any value, mostly describing the exact code that follows. Sometimes not even that :)

## <a name="HTML"></a> HTML
- #### <a name="SemanticTags"></a> Semantic Tags:
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

- #### <a name="StructuralElements"></a> Structural Elements
    It is sometimes necessary to wrap HTML in tags that are structural, and have no direct impact on the content presented.
    This is totally fine, but keep it clean!

    In the example below, we have a UI that contains two buttons and a paragraph
    of text that is output based on some kind of user interaction. On a small screen (or small space), the buttons and
    the output text can stack vertically (think, display: block down the page).

    On a larger screen, however, we may want these groups of elements to go 50/50 to better occupy screen real-estate.

    In this type of case, we can semantically divide our html into two "ui-group"s, allowing us the flexibility required to make a nice app.

    ```html
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

- #### <a name="DataAttributes"></a> Data Attributes
    - Data attributes should be used to provide information to JavaScript to initialize or operate on that portion of the DOM. For instance, consider this fictional example that loads 20 comments from a particular service. At a high-level, all that is required to make the service calls are an **id** and a **count** for number of comments.

    ```html
    <div class="comments" data-comment-id="jks34" data-comment-count="20">
        ...
    </div>
    ```

    - In special cases, data attributes can be used for CSS display values. Consider this example:
    ```html
    <div class="city--label" data-city-name="Houston, TX"></div>

    <style>
        .city--label:before {
            content: attr(data-city-name);
        }
    </style>
    ```
- #### <a name="IDs"></a> ID's
    - Use ID's sparingly! Make sure there is only one per document! And never style them ;)

- #### <a name="Syntax"></a> Syntax
    - **Always** use semantic tags!
    - **Always** use doublequotes for attributes!
    - **Always** use proper indentation (keep your structure sane!)
    - **Always** make your HTML human-readable
    - **Never** use an #ID for styling hooks
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

## <a name="CSS"></a> CSS / SASS
0. The CSS / Sass guidelines are based off of [csswizardry/CSS-Guidelines][css].
0. We use [normalize.css][normalize] as our style reset.
0. <a name="BEM"></a> We favor BEM (Block Element Modifier) syntax where possible, and the wonderfully flat selector structure this gives us.
    - Blocks
    ```css
    .article {
        font-size: 1em;
    }

    .article--video {
        /* some video article styles */
    }
    ```
    - Elements
    ```css
    .article__title {
        font-size: 3em;
    }

    .article__byline {
        color: #c00;
        font-size: .8em;
        font-weight: bold;
    }
    ```

### Guidelines
- <a name="MobileFirst"></a> Default styling must be mobile/small-sized first.
```css
/* Poor */
.class {
    border: 1px solid #888;
    color: #ccc;

    @media (max-width: 359px) {
        border: none;
    }
}

/* Good */
.class {
    color: #ccc;

    @media (min-width: 360px) {
        border: 1px solid #888;
    }
}
```

- <a name="SeparateStructure"></a> Separate structural properties from visual properties using extends. This
    will allow us to easily swap visual skinning of elements without needing to
    override css definitions. This format also serves as a self-documenting table
    of contents.

```sass

    //
    // Robot Component
    //

    .robot {
        @extend %robot-structure;
        @extend %robot-visual;
        @extend %robot-theme;
    }

    .robot__head {
        @extend %robot__head-structure;
        @extend %robot__head-visual;
        @extend %robot__head-theme;
    }

    .robot--spacerobot {
        @extend %robot--spacerobot-theme;
    }

    //
    // Robot Block Styles
    //

    %robot-structure {
        display: block;
        height: 60px;
        width: 100px;
    }

    %robot-visual {
        box-shadow: 2px 2px 2px rgba(255,0,0,.6);
        transform: translateZ(1000px);
    }

    %robot-theme {
        background-color: $robot-titanium;
        border: 1px solid $robot-gold;
    }

    //
    // Robot Element Styles
    //

    %robot__head-structure {
        display: block;
    }

    %robot__head-visual {
        border-radius: 1000px;
    }

    %robot__head-theme {
        background-color: $robot-black;
    }

    //
    // Robot Modifier Styles
    //

    %robot--spacerobot-theme {
        background: url(/images/spacegraphic.png) repeat top left;
    }
```

Here's a list of structural properties vs visual properties:

| Structural    | Visual       |
| ------------- | ------------ |
| display       | background   |
| height        | border       |
| margin        | color        |
| padding       | transform    |
| position      | transition   |
| width         | opacity      |
| z-index       | visibility   |
|               | box-shadow   |

Depending on the application, here is a list of properties that
could be used to define a theme:

| Theme                             |
| --------------------------------- |
| background                        |
| border                            |
| box-shadow                        |
| color                             |
| font-family                       |
| text-transform                    |
| and more! (but nothing structural)|

- <a name="DefaultStyles"></a> Sometimes, however, an element will need some sort of default styling. When
    creating the default state, think of which one can be achieved using the least
    amount of selectors. In the example above, `element--light` requires one less
    definition, and would be a candidate for default styling.

Let's use sass to keep our code clean!

```sass
.robot {
    // include element--light as the default theming
    @extend .robot--model5000;

    margin: 0 auto;
    width: 50%;
}

.robot--model5000 {
    background-color: $robot-chrome;
    border: 1px solid $robot-spaceblack;
}

// Outputs:
//
// .robot {
//     margin: 0 auto;
//     width: 50%;
// }
//
// .robot--model5000, .robot {
//     background-color: #ddd;
//     border: 1px solid #121212;
// }
```

## <a name="Markdown"></a> Markdown
0. All lines that are not code blocks should wrap at or under 80 columns.
0. Should allow trailing whitespace, since that is a valid Markdown syntax.
0. Should have 2 blank lines above each H1 and H2 heading except for the
   heading at the top of the document.  This is optinal for other headings.
0. Should have 4 blank lines to separate the link reference at the bottom of
   the document.
0. Should use `0.` for ordered lists.
0. Should use `-` for unordered lists.
0. Secondary bullets must be indented four spaces to render correctly on
   Bitbucket.
0. Do not try to put code blocks as secondary bullets in a list.  They will not
   render correctly on both GitHub and BitBucket. More details on this to come
   in the future.

## <a name="Contributors"></a> Contributors
**YOU!** - please contribute to these code guidelines! If you have any
suggestions for improvement to these guidelines, *[create an issue][issue]* to
discuss it or *create a [pull request][pr]* with your changes and discussion
will occur on that PR.  Also review the [contributing guidelines](https://github.com/TurnerBroadcasting/mss-code-guidelines/blob/master/CONTRIBUTING.md).

## <a name="ConflictResolution"></a> Conflict Resolution
We have included [JSHint][jshint] and [JSCS][jscs] RC files in this repository
to validate javascript code against these guidelines.  When something is
questioned, these files will always win.  When in doubt, run JSHint and JSCS
with the `.jshintrc` and `.jscsrc` files in place and see if they find any
problems.  It is recommended that you find plugins for your editor of choice to
always validate your code against these files.

### <a name="IncludedFiles"></a> Regarding the multiple suffixed files
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

### <a name="Authors"></a> Authors
- James Young [@jamsyoung](http://twitter.com/jamsyoung), [github](https://github.com/jamsyoung)
- Matt Crutchfield [@mtcrutch](https://twitter.com/mtcrutch), [github](https://github.com/mtcrutch)
- Christian Hain [github](https://github.com/mtcrutch)
- Paul Borrego [github](https://github.com/mtcrutch)
- Chris Gonzalez [github](https://github.com/chrisgonzalez)

### <a name="HelpfulLinks"></a> Helpful Links

[AirBnB Style Guide](https://github.com/airbnb/javascript)  
[CSS Guidelines](https://github.com/csswizardry/CSS-Guidelines)  
[Idiomatic Javascript](https://github.com/airbnb/javascript)  
[Inline Block Problems!](http://css-tricks.com/fighting-the-space-between-inline-block-elements/)  
[GitHub Issues](https://github.com/TurnerBroadcasting/MTS-Code-Guidelines/issues/new)  
[JSCS](https://github.com/mdevils/node-jscs)  
[JSHint](https://github.com/jshint/jshint/)  
[Normalize CSS](http://necolas.github.io/normalize.css/)  
[Pull Requests](https://github.com/TurnerBroadcasting/MTS-Code-Guidelines/compare/)
