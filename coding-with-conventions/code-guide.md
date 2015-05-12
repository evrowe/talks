# HealthSparq Code Guide

The UI team has made an effort to standardize our coding style to make it easy for any UI developer to jump into any file in any UI application and be able to quickly and easily determine what's going on and make their own edits in a format that is consistent with what has already been written in that file. These standards also help to improve the overall readability of our files.

These standards are based largely on [MDO's Code Guide](http://codeguide.co/), but we have made some modifications to the guidelines set forth in that document. Those modifications are noted in the sections listed below.

## Global

### Tabs & Spacing

Use soft tabs, two spaces

### Reducing Markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML.

### JavaScript Generated Markup

Writing markup in a JavaScript file makes the content harder to find, harder to edit, and less performant. Avoid it whenever possible.

## HTML

### Syntax

- Nested elements should be indented once (two spaces).
- Always use double quotes, never single quotes, on attributes.
- Don't include a trailing slash in self-closing elements—the HTML5 spec says the're optional.
- Don't omit optional closing tags (e.g. `</li>` or `</body>`).

### Doctype

- Use the HTML5 doctype: `<!DOCTYPE html>`

### Language

- Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.

### IE Compatibility

IE compatibility mode. Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IE to use the latest supported mode with edge mode.

### Encoding

Character encoding. Quickly and easily ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document (generally UTF-8).

### Including CSS and JavaScript Resources

Per HTML5 spec, typically there is no need to specify a type when including CSS and JavaScript files as `text/css` and `text/javascript` are their respective defaults.

### Boolean Attributes

Boolean attributes should not have a value; they should simply exist or not, e.g., `<input type=”checkbox” checked>` vs. `<input type=”checkbox” checked=”checked”>`.

### Attribute Order

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`
- `title`, `alt`
- `aria-*`, `role`
-
Note: `data-*` attributes should be examined to determine their level of importance for understanding the HTML tag context. If the `data-*` attribute does not provide key information about the tag, it should be written after src, for, type or href attributes.

## CSS

### Syntax

- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Include spaces after commas within `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values. This helps differentiate multiple color values (comma, no space) from multiple property values (comma with space).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. They're only optional in some cases, and it's good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.
- Include the number `0` when assigning float values between `-1` and `1`, e.g. `0.25`. This isn't strictly required but some syntax highlighters won't highlight the value without it.

### Declaration Order

Declare your properties in alphabetical order; this makes it easier to determine whether a property has already been declared for later editing, and (nearly) eliminates the chance of duplicate property delcarations.

### Media Queries

Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document.

### Shorthand Notation

There is no default concerning whether shorthand is good or bad. Use common sense. Never write shorthand notation that needs to be overridden and don't duplicate standard notation if shorthand can save you time.

### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Be sure to write in complete sentences for larger comments and succinct phrases for general notes. When writing SCSS/SASS, always begin comments with double forward slash notation ( `//` ) vs. standard CSS comment notation ( `/**/` ).

### Class Names

- Keep classes lowercase and use dashes (not `_underscores` or `camelCase`). Dashes serve as natural breaks in related class (e.g., `.btn` and `.btn-danger`).
- Avoid excessive and arbitrary shorthand notation. `.btn` is useful for button, but `.s` doesn't mean anything.
- Keep classes as short and succinct as possible.
- Use meaningful names; use structural or purposeful names over presentational.
- Prefix classes based on the closest parent or base class.
- Use `.js-*` classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

### Selectors

- Use classes over generic element tag for optimum rendering performance.
- Selectors that target element IDs should be avoided but are ok in certain rare circumstances; however, code should be carefully examined as to whether this is a viable option, and refactoring may need to be considered.
- Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occurring components. Browser performance is known to be impacted by these.
- Keep selectors short and strive to limit the number of elements in each selector to three. If there is ever a need to write more than three parts of a selector, - consider refactoring the code.
- Scope classes to the closest parent only when necessary (e.g., when not using prefixed classes).

### Organization

See SMACSS ( [http://smacss.com/](http://smacss.com/) ).

### SASS/SCSS

- List extends first.
- List includes second.
- List plain old CSS rules third.
- Nested selectors go last and in the following order:
  - Pseudo-class selectors.
  - Class selectors.
  - Parent selectors.
  - Child selectors.
- Anywhere you need vendor prefixes for rules, use a mixin.
- Maximum nesting is three levels deep.
- Maximum nesting is 50 lines. If a nested block of Sass is longer than that, there is a good chance it doesn't fit on one code editor screen, and starts becoming difficult to understand. The whole point of nesting is convenience and to assist in mental grouping. Don't use it if it hurts that.
- No style rules in root stylesheet.
- Partials file names begin with an underscore.
- Create variables for all common numbers and numbers with meaning and colors. If you find yourself using a number other than 0 or 100% over and over, it likely deserves a variable. Since it likely has meaning and controls consistency, being able to tweak it en masse may be useful. If a number clearly has strong meaning, that's a use case for a variable as well.
- Nest and name your media queries.
- In your global stylesheet, `@import` a `_shame.scss` file last.

## JavaScript

### Syntax

Use white space to promote readability

Using only one `var` per scope (function) promotes readability and keeps your declaration list free of clutter (also saves a few keystrokes).

`var` statements should always be in the beginning of their respective scope. If a value can't be assigned to a variable at the point of declaration, still declare the variable but wait to assign the value until it's safe.

    /**
     * This is an example function
     *
     * returns {Date}
     */
    function example() {

      var exampleString = 'exampleString',
          exampleNumber = 100,
          exampleDate = new Date();

      if (exampleNumber > 1) {

        alert(exampleString + '!');
      }

      return exampleDate;
    }

Function names, like variable names, should begin with lowercase letters except when writing constructors.

    // Function example:
    function someFunction() {

    }

    // Constructor example:
    function SomeClass() {

    }

Consistency is key. When working on a project, follow any existing standards you may find within a file. Don't write code that looks different than the existing code.

Use consistent quotes. Single quotes are encouraged, as they need to be escaped far less frequently than double quotes in strings.

When writing conditional statements that evaluate some value's truthiness/falsiness, use the syntax: `if ( variable )` or `if ( !variable )`. Always evaluate for the best, most accurate result - the former is a guideline, not a dogma.

Naming conventions:

- camelCase: variable, function and method names
- PascalCase: constructors
- UPPERCASE: constants

### Documentation

HealthSparq's modern front-end applications include the ability to generate documentation with the JSDoc library. All high-level objects and their members should be documented. Low-level variables (local variables), including objects, don't need documentation but there is no reason they can't have it. Read up on JSDoc by visiting [http://usejsdoc.org/](http://usejsdoc.org/).

**Example:**

    /**
     * The instance of an Ember application that drives the site
     *
     * @namespace
     * @name App
     * @extends external:Ember.Application
     */
     App = Ember.Application.create({
       /**
        * Whether or not the application has been loaded
        *
        * @memberof App
        * @instance
        * @type {boolean}
        */
       isLoaded: false,
       /**
        * Some functionality that helps to load the application
        *
        * @memberof App
        * @instance
        */
       loadApplication: function() {

         // These local, low-level variables need no JSDoc style comments
         var requestUrl = '/load/application',
             options = {
               contentType: 'json'
             };

         return $.ajax(requestUrl, options).then(function(response) {

           // Do something with the response and then...

           App.set('isLoaded', true);
         });
       }
     });