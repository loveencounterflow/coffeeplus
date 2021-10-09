
# coffeeplus

Syntax definition for Sublime Text 3 that allows Sub-Grammars (such as SQL) for [Tagged Template
Literals](https://coffeescript.org/#tagged-template-literals) embedded in
[CoffeeScript](https://coffeescript.org) source



<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [What it Does](#what-it-does)
- [Installation](#installation)
- [To Do](#to-do)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## What it Does

* adds embedded language syntax highlighting
* for [Tagged Template Literals](https://coffeescript.org/#tagged-template-literals) embedded in
  [CoffeeScript](https://coffeescript.org) source
* this is one motivation behind tagged template literals, after all: *Tagged templates should allow the
  embedding of
  languages*—[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
* recognized as an identifier directly in front of a string literal, as in `sql"select * from t;"` and
  `sql"""select * from t;"""`
* case-insensitive prefix is recognized as language identifier
* easy to write a no-op function that returns the string as-is
* or use an actual templating function that is appropriately named
* case-insensitivity intended to lower the chances of name clashes:

  ```coffee
  # in case your variable is lower case and your templating function is in upper case:
  sql = SQL"select name, price from items order by price;"
  # in case your variable is upper case and your templating function is in lower case:
  SQL = sql"select name, price from items order by price;"
  ```

* minimal tagged literal function:

  ```coffee
  SQL = ( parts, expressions... ) ->
    R = parts[ 0 ]
    for expression, idx in expressions
      R += expression.toString() + parts[ idx + 1 ]
      # R += "#{expression}#{parts[ idx + 1 ]}"
    return R
  ```

  * The above function may be taken as a starting point to implement some interpolation functionality
  * but it's even easier to just say `SQL = String.raw` as `string.raw()` provides exactly this
    functionality

## Installation

* no package / package control provided so far
* manual installation only
  * git clone
  * symlink from package directory to <del>cloned repo</del> <ins>to the `coffeeplus`, `SQL` subdirectories;
    if there is a conflict with an installed `SQL` package, remove that one first</ins>
  * add `"color_scheme": "Packages/coffeeplus/coffeeplus-monokai-neue.tmTheme"` in
    `~/.config/sublime-text-3/Packages/User/Preferences.sublime-settings`
* file `coffeeplus/coffeeplus-monokai-neue.sublime-color-scheme` is loaded implicitly
* it updates the color theme with backgrounds for matched regions
* adapt backgrounds to your liking
* file `coffeeplus/coffeeplusbase.tmPreferences` is also loaded implicitly, it would [appear to be still
  needed](https://forum.sublimetext.com/t/toggle-comment-with-a-custom-sublime-syntax/18789) in order for
  the `toggle comment` functionality to work


## To Do

* [X] determine how to declare default syntax
* [X] doc: installation
* [ ] doc: how to add language definition
* [ ] use inheritance so language region definitions get into separate file
* [ ] provide ST3/4 package
* [ ] implement CS templating syntax (`#{...}`) to embed CS in SQL template literals
* [X] fix comment toggling via keyboard shortcut
* [X] remove `#` (hash/number-sign) from the list of recognized SQL comments


