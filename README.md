# CSS-Guidelines #

CSS best practices for GF inspired by SMACSS

In order to make CSS flexible, maintainable and fail-safe, the concept of SMACSS (Scalable and Modular Architecture for CSS) has two core goals:

1. Increase the semantic value of a section of HTML and content
2. Decrease the expectation of a specific HTML structure

## Syntax ##

* Indent: 4 spaces (no Tabs)
* Opening bracket on the same line as the rule set
* A Space before the opening bracket
* A Space behind the colon
* Color declarations in hex
* Use short syntax where possible
* Zero-values have no unit
* Properties grouped by types, separated by blank lines: 1. Box, 2. Border, 3. Background, 4. Text, 5. Other 

Example:

    .question {
        display: block;
        float: left;
        position: relative;
        margin: 0;
        
        border: 1px solid #333;
        
        font-size: 12px;
        text-transform: uppercase;
    }


## Categorizing ##

SMACSS introduces four types of categories for a project. Any styling rule belongs to one of these categories:

1. Base
2. Layout
3. Module
4. State

### Base rules ###

The base category is about the default styles. There are only single element selectors (and their pseudo-elements) that say: Wherever the element is on the page, it should look like this.

    body, form {
        margin: 0;
        padding: 0;
    }
    
    a {
        color: #309;
    }
    
    a:hover {
        color: #03F;
    }

### Layout rules ###

The layout category is about the sections of a page holding one or more modules together. A section has only a single selector. This could be an ID selector for the general parts of the layout like header, content, sidebar and footer. Other layout rules are prefixed with "l-" to make clear they are about the composition of the layout:

    /* fluid layout */
    #content {
        width: 80%;
        float: left;
    }
    
    #sidebar {
        width: 20%;
        float: right;
    }
    
    /* fixed layout */
    .l-fixed #article {
        width: 600px;
    }
    
    .l-fixed #sidebar {
        width: 200px;
    }   

### Module rules ###

Into the module category belong all modular and reusable parts of our design like lists, content items or different sidebar sections. Module selectors are the bulk of any project, so they get no module-prefix, but sub-modules like related elements and variations get their base modules name as prefix:

    /* Example Module */
    .example { }
    
    /* Example Sub-Module */
    .example.example-fault { }

### State rules ###

There are two kinds of state rules: Global states and module states.

Global states describe the look of modules or layouts in a particular state like when it's hidden or expanded. The state rules indicate a JavaScript dependency. They get prefixed with "is-". They have a single class selector, so it might be necessary to use !important here to override other more complex rule sets.

Module states are for a specific state for a particular module. The state class name should include the module name in it. The state rule should also reside with the module rules and not with the rest of the global state rules.

    /* Navigation Module with global state */
    .navigation.is-collapsed { }
    
    /* Navigation Module with specific state */
    .is-navigation-active

We want to know instantly just by its name what a selector is about und which category it belongs to, so the selectors names MUST follow its categories naming conventions.

## Selectors ##

Only use a selector that includes semantics.
Minimize the depth of applicability: The depth of applicability is the number of generations affected by a given rule: For example

    body.article > #main > #content > #intro > p > b
has a depth of applicability of 6 generations.

    .article #intro b
looks shorter, but based on the same HTML-structure as above it still has 6 generations - It has a big dependency on this particular HTML-structure. One of our goals is to decrease the expectation of a specific HTML structure, so a better solution would be to rename the #intro:

    .article-intro b
This reduces the depth of applicability to the half.

Minimize the number of affected nodes in a selector chain to avoid too much dependency on a particular HTML structure, to improve maintenance, performance and readability.

Use:
* Class: The selector of choice. For performance reasons use class selectors especially for the most right selector.
* Child: Use the child selector ">" to minimize the depth of applicability.

Avoid:
* ID: ID selectors for styling are not necessary as the performance benefit compared to class selectors is nearly non-existent, but IDs make styling more complicated due to increasing specificity.
* Element: Avoid element selectors because they are too generic when styles grow in complexity over time.
* Tag: Avoid tag selectors for common elements for performance reasons.

bad:

    #sidebar div, #footer div {
        border: 1px solid #333;
    }
    
    #sidebar div h3, #footer div h3 {
        margin-top: 5px;
    }
    
    #sidebar div ul, #footer div ul {
        margin-bottom: 5px;
    }
    
good:

    .box {
        border: 1px solid #333;
    }
    
    .box > h3 {
        margin-top: 5px;
    }
    
    .box > ul {
        margin-bottom: 5px;
    }

## !important ##

The use of !important should be avoided. It breaks our cascade, inheritance and specificity order and leads into a maintenance nightmare.

(The only possible exception where the use of !important could be appropriate is in state rules - see above)

## File Organization ##

* Place all Base rules into their own file
* Depending on the type of layouts you have, either place all of them into a single file or major layouts into separate files.
* Put each module into its own file.
* Depending on size of project, place sub-modules into their own file.
* Place global states into their own file.
* Place layout and module states into the module files

A sample directory structure (using SASS):

    +-layout/
    | +-grid.scss
    | +-alternate.scss
    +-module/
    | +-callout.scss
    | +-bookmarks.scss
    | +-button.scss
    | +-button-compose.scss
    +-base.scss
    +-states.scss
    +-site-settings.scss
    +-mixins.scss
