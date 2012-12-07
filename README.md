css-style-guide
===============

css best practices inspired by SMACSS

Syntax
------

Indent: 4 spaces

Categorizing
------------

There are four types of categories:

1. Base: the defaults
2. Layout: the sections of a page holding modules
3. Module: the modular and reusable parts 
4. State: different states of modules and layouts. Indicate a JavaScript dependency.

Naming Conventions
------------------

We want to know instantly just by its name what a selector is about und which category it belongs to:

* Layouts: prefixed with "l-"
* States: prefix layout and style names with "is-"
* Modules: no prefix, but related elements and variations use their base modules name as prefix

Selectors
---------

Only include a selector that includes semantics.

Minimize the depth of applicability: The depth of applicability is the number of generations that are affected by a given rule. Minimize it to avoid too much dependency on a particular HTML structure, to improve maintenance, performance and readability.

Use:
* Class: The selector of choice. For performance reasons use class selectors as the right most selector.
* Child: Use child selectors to minimize the depth of applicability.

Avoid:
* ID: ID selectors are not necessary for styling as the performance benefit compared to class selectors is nearly non-existent, but IDs make styling more complicated due to increasing specificity.
* Element: Avoid element selectors because they are too generic when styles grow in complexity over time.
* Tag: Avoid tag selectors for common elements for performance reasons.
