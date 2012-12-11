css-style-guide
===============
CSS best practices for GF inspired by SMACSS

In order to make CSS flexible, maintainable and fail-safe, the concept of SMACSS (Scalable and Modular Architecture for CSS) has two core goals:

1. Increase the semantic value of a section of HTML and content
2. Decrease the expectation of a specific HTML structure

Syntax
------
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


Categorizing
------------
There are four types of categories for a project where all the styling rules belong:

1. Base
2. Layout
3. Module
4. State

Base rules: The default styles belong here. There are only single element selectors that say: Wherever the element is on the page, it should look like this.

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

Layout rules: The sections of a page holding one or more modules together. A layout style has only a single selector. This can be an ID for the general parts of the layout like footer, content, sidebar and footer. Other layout rules are prefixed with "l-":

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

Module rules: The modular and reusable parts of our design like lists or sidebar sections. Module selectors are the bulk of any project, so they get no module-prefix, but sub-modules like related elements and variations get their base modules name as prefix:

    /* Example Module */
    .example { }
    
    /* Example Sub-Module */
    .example.example-negative { }

State rules: They describe the look of a module or layout in a particular state like hidden or expanded. The state rules indicate a JavaScript dependency. State rules get prefixed with "is-".

    /* Callout Module with State */
    .callout.is-collapsed { }

We want to know instantly just by its name what a selector is about und which category it belongs to, so the selectors names MUST follow its categories naming convention.

Selectors
---------
Only include a selector that includes semantics.
Minimize the depth of applicability: The depth of applicability is the number of generations affected by a given rule. Minimize it to avoid too much dependency on a particular HTML structure, to improve maintenance, performance and readability.

Use:
* Class: The selector of choice. For performance reasons use class selectors as the most right selector.
* Child: Use child selectors to minimize the depth of applicability.

Avoid:
* ID: ID selectors are not necessary for styling as the performance benefit compared to class selectors is nearly non-existent, but IDs make styling more complicated due to increasing specificity.
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