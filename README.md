
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
* recognized as an identifier directly in front of a string literal, as in `sql"select * from t;"` and
  `sql"""select * from t;"""`
* case-insensitive prefix is recognized as language identifier
* easy to write a no-op function that returns the string as-is
* or use an actual templating function that is appropriately named
* case-insensitivity intended to lower the chances of name clashes:

  ```coffee
  sql = ( ... ) -> ...
  sql = SQL"select name, price from items order by price;"
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

## Installation

* no package / package control provided so far
* manual installation only
  * git clone
  * symlink from package directory to cloned repo
  * add `"color_scheme": "Packages/coffeeplus/coffeeplus-monokai-neue.tmTheme"` in
    `~/.config/sublime-text-3/Packages/User/Preferences.sublime-settings`
* file `coffeeplus/coffeeplus-monokai-neue.sublime-color-scheme` is loaded implicitly
* it updates the color theme with backgrounds for matched regions
* adapt backgrounds to your liking


## To Do

* [ ] determine how to declare default syntax
* [ ] doc: installation
* [ ] doc: how to add language definition
* [ ] use inheritance so language region definitions get into separate file


