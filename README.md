css-style-guide
===============
CSS best practices for GF inspired by SMACSS

There are two core goals:

1. Increase the semantic value of a section of HTML and content
2. Decrease the expectation of a specific HTML structure

Syntax
------
* Indent: 4 spaces (no Tabs)
* Opening bracket on the same line as the rule set
* A Space before the opening bracket
* A Space behind the colon
* Color declarations in hex
* Properties grouped by types: 1. Box, 2. Border, 3. Background, 4. Text, 5. Other separated by a blank line

Example:

    .question {
        display: block;
        float: left;
        position: relative;
        
        border: 1px solid #333;
        
        font-size: 12px;
        text-transform: uppercase;
    }


Categorizing
------------
There are four types of categories where the styling rules belong:

1. Base
2. Layout
3. Module
4. State

Base rules: The defaults belong here. There should be only single element selectors that say that wherever the element is on the page, it should look like this.

Layout rules: The sections of a page holding one or more modules together.

Module rules: The modular and reusable parts of our design like lists or sidebar sections.

State rules: They describe the look of a module or layout in a particular state like hidden or expanded. The state rules indicate a JavaScript dependency.

Naming Conventions
------------------
We want to know instantly just by its name what a selector is about und which category it belongs to:
* Layouts: prefixed with "l-"
* States: prefix layout and style names with "is-"
* Modules: no prefix, but related elements and variations use their base modules name as prefix

Examples:

    /* Example Module */
    .example { }
    
    /* Example Sub-Module */
    .example.example-negative { }
    
    /* Callout Module with State */
    .callout.is-collapsed { }
    
    /* Inline layout */
    .l-inline { }

Selectors
---------
Only include a selector that includes semantics.
Minimize the depth of applicability: The depth of applicability is the number of generations affected by a given rule. Minimize it to avoid too much dependency on a particular HTML structure, to improve maintenance, performance and readability.

Use:
* Class: The selector of choice. For performance reasons use class selectors as the right most selector.
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