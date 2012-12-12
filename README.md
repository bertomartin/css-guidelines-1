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
* Properties grouped by types, separated by blank lines: 1. Box, 2. Border, 3. Background, 4. Text, 5. Other 

Example:

    .question {
        /* Box properties */
        display: block;
        float: left;
        position: relative;
        
        /* Border property */
        border: 1px solid #333;
        
        /* Text properties */
        font-size: 12px;
        text-transform: uppercase;
    }


## Categorizing ##

SMACSS introduces a directory structure of four types of categories for a project. Any styling rule belongs into one of these categories:

1. Base
2. Layout
3. Module
4. State

### Base rules ###

The base category is about the default styles. There are only single element selectors that say: Wherever the element is on the page, it should look like this.

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

Rules in the state category describe the look of a module or layout in a particular state like when it's hidden or expanded. The state rules indicate a JavaScript dependency. They get prefixed with "is-".

    /* Callout Module with State */
    .callout.is-collapsed { }

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

    .pod {
        border: 1px solid #333;
    }
    
    .pod > h3 {
        margin-top: 5px;
    }
    
    .pod > ul {
        margin-bottom: 5px;
    }
