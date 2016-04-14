# JigSass Utils Border
[![NPM version][npm-image]][npm-url]  [![Dependency Status][daviddm-image]][daviddm-url]   

 > Border utility classes

A collection of dynamically generated border utility classes.

JigSass Utils Border works in tandem with
[JigSass Tools typography](https://txhawks.github.io/jigsass-tools-typography),
providing utility classes which add borders that don't mess up vertical rhythm.

Border utils can be limited to a certain state (i.e., `hover`, `focus`,  etc.)

The syntax for generating a border util is: `$modifier: '<width-in-pixels>[(<rhythm-units>,<border-style>,<border-color>)][:state]'`

Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions, e.g, bdb--1px(2,solid,#ccc) for setting border-bottom of 1px,
a padding-bottom of two typographic lines minus the border width, border-style
of solid and border-color or #ccc.

#### Available classes

  - `u-bd--<width>` (example: u-bd--2px, sets a border of 2 pixels around an element)
  - `u-bd--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px around an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bdt--<width>` (example: u-bd--2px, sets a border of 2 pixels above an element)
  - `u-bdt--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px above an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bde--<width>` (example: u-bd--2px, sets a border of 2 pixels at the horizontal end an element)
  - `u-bde--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px at the horizontal end of an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bdr--<width>` (example: u-bd--2px, sets a border of 2 pixels at the right end of an element)
  - `u-bdr--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px at the right end of an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bdb--<width>` (example: u-bd--2px, sets a border of 2 pixels below an element)
  - `u-bdb--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px below an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bds--<width>` (example: u-bd--2px, sets a border of 2 pixels at the horizontal start an element)
  - `u-bds--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px at the horizontal start of an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)


  - `u-bdl--<width>` (example: u-bd--2px, sets a border of 2 pixels at the left end of an element)
  - `u-bdl--<width>(<rhythm-units>,<style>,<color>)` (example: u-bd--1px(1,dotted,#ccc),
    sets a border of 1px at the left end of an element, padding of 1 rhythm unit minus 1px, a
    border-style of `dotted` and border color of `#ccc`)



## Installation

Using npm:

```sh
npm i -S jigsass-utils-border
```

## Usage
Import JigSass Utils Border into your main scss file near its very end, together with all
other utilities (utilities should always be the last to be imported).

```scss
@import 'path/to/jigsass-utils-border/scss/index';
```

Like all other JigSass Utils, JigSass Utils Border does not automatically generate any CSS
when imported. You would need to explicitly indicate that each individual border
class should actually be generated in each component or object it is used in
(clarification: This will include style declarations inside `.foo` and .`bar`):

```scss
// _c.foo.scss
.foo {
  @include jigsass-util(u-bds, $modifier: '2px(1,solid,#4c4)');

  ...
}
```

```scss
// _c.bar.scss
.bar {
  @include jigsass-util(u-bdb, $modifier: '1px(1,dotted,#4c4):hover');
  @include jigsass-util(u-bdb, $modifier: '2px(1,dotted,#4c4):hover', $from: large);

  ...
}
```

Doing so helps us a great deal with portability, as no matter where we import component or object
partials, the correct utility classes will be generated. Think of it as a poor man's dependency
management.

Developer communication is also assisted by including "dependencies" wherever they are required,
as anyone going through a partial, can easily understand how it should be marked up with just a
glance.

As far as bloat goes, just don't worry about it - the actual styles will only be generated once,
at the location in the cascade where the Jigsass Utils Border partial was imported into the main file.


JigSass Utils Border classes are responsive-enabled, using [JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/)
and the breakpoints defined in the [$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints) variable.

Based on the breakpoint arguments passed to `jigsass-util` when including a class,
responsive modifiers are generated according to the following logic:

```scss
.u-bd-<modifier>[-[-from-<breakpoint-name>][-until-<breakpoint-name>][-misc-<breakpoint-name>]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
@include jigsass-util(u-bd, $modifier: 1px);
```
will generate the `u-bd--1px` class, which is not limited to any media-query.

```scss
@include jigsass-util(u-bd, $modifier: '1px(1,solid)', $until: medium);
```

will generate the `u-bd--1px(1,solid)--until-medium` class, which will be in effect at
`(max-width: 37.49em)` and will override styles in the default class until that point.

```scss
@include jigsass-util(u-bd, $modifier: 2px(2):focus, $from: large, $misc: landscape);
```

will generate the `u-bd--2px(2):focus--from-large-when-landscape` class, which will go into
effect at `(min-width: 64em) and (orientation: landscape)` and will override styles in the default
class under these  conditions.




## Documentation

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-utils-border/](https://txhawks.github.io/jigsass-utils-border/)

## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have the user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Border in any way you see fit.

#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Border uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.



## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
```



**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-utils-border.svg
[npm-url]: https://npmjs.org/package/jigsass-utils-border

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-utils-border.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-utils-border
