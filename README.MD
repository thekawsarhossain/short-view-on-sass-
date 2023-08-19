# Sass

#### What is Sass?

Sass stands for Syntactically Awesome Stylesheet; It's a scripting language, Sass is an extension to Css also Sass is a Css pre-processor.

#### Well now question comes that what is CSS preprocessor?

CSS preprocessors are scripting languages that extend the default capabilities of CSS. They enable us to use logic in our CSS cpde, such as variables, nesting, inheritance, mixins, functions and many more

### Let's talk more about on Sass

We get Sass in two flovar .sass and .scss

Now in .sass file we need to follow this syntex:

```sass
nav
    ul
        list-style: none

    li
        display: inline-block

    a
        display: block
        padding: 8px 12px
        text-decoration: none
```

its more like indented syntax.

And in .scss file we need to follow this:

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display: block;
    padding: 8px 12px;
    text-decoration: none;
  }
}
```

Now this looks like almost css syntex, So we will follow this for scss and will include some more spices in it.

#### Now let's talk about one of the killer feature of Sass $variables

In Sass we will be able to declare variables just like programming languages
To declare the variable we just need to add the dollor sign before the variables name and as value we will be able to use string, numbers, colors, booleans, lists, null

Here is an example how we can declare and use variables:

```scss
$my_font: Helvetica, sans-serif;
$my_color: crimson;
$myFontSize: 18px;
$myWidth: 680px;

body {
  font-family: $my_font;
  font-size: $myFontSize;
  color: $my_color;
}

#container {
  width: $myWidth;
}
```

And it would be look like this after transpile

```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: crimson;
}

#container {
  width: 680px;
}
```

But this feature is already avilable in css as called css custom properties, why do we need sass for this then ?
Well because of browser support a good amount of browser and their versions doesn't support css variable But in this case still sass variables are powerfull

#### Now let's talk about Sass Nesting

Nesting is the most powerfull thing in Sass
Let's undetand this using an example:
In css we need to use or write the same selector multiple times But using Sass we can avoid that
Here is how:

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 8px 12px;
  text-decoration: none;
}
```

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display: block;
    padding: 8px 12px;
    text-decoration: none;
  }
}
```

Now if we do a comparision we will see that in css we use same selector multiple times and using sass we just avoid using same selector and wrote the code in nested format.
First we declraed the parent selector and all the common selctors are in curly braces

Another good example is if a tag has multiple siblings and like we have to use them then again we have to do the same thing using same selector multiple times

```css
a:link {
  color: red;
}
a:visited {
  color: green;
}
a:hover {
  color: hotpink;
}
a:active {
  color: blue;
}
```

And here again if we do this same thing again using Sass it would be like this

```scss
a {
  &:link {
    color: red;
  }
  &:visited {
    color: green;
  }
  &:hover {
    color: hotpink;
  }
  &:active {
    color: blue;
  }
}
```

Also before the tags siblings we need to use & (ampersand) to achive using nesting

And by looking at these examples we can say that Sass is more cleaner syntex and easier to read.

#### Now let's talk about Nested Properties

So in Css many properties has the same prefix for example: font-size, font-weight, font-family these has same prefix font

text-decoration, text-transform, text-overflow these has the same prefix text

Now using nested properties we can write it like this:

```scss
body {
    font: {
        family: Helvetica, sans-serif
        size: 18px;
        weight: bold;
    }
    text {
        align: center
        transform: lowercase;
        overflow: hidden;
    }
}
```

Here we just keep the common things in curly braces

#### Now let's jump onto @import and Partials

Sass helps to keep the css code DRY, Here DRY means Don't Repeat Yourself

So by using this features what we do is we can create files for variables, colors and something else as needed and then import them in the main scss file and will be able to access all these varibales and colors and everything

And the format to import is `@import "fileName"`

By default, Sass transpile all the .scss file directly But to we dont need to compile partials So to make the difference between standard .scss and partials what we can do is we can use \_filename.scss

So basically Sass will nopt transpile filename that starts with an underscore

#### Now let's talk about @mixin

@mixin directive let's us tp create Css code that is to be reuses throughout the website

Here is an example:

```scss
@mixin important-text {
  color: red;
  font-size: 18px;
  font-weight: bold;
  border: 1px solid blue;
}

.danger {
  @include important-text;
  background-color: green;
}
```

Also remember in sass (-)hyphen and (\_)underscore are same

Also A mixin can include another mixin

```scss
@mixin special-text {
  @include important-text;
  @include link;
  @include special-border;
}
```

Also we can pass variables to a mixin

```scss
@mixin bordered($color, $width) {
  border: $width solid $color;
}

.myArticle {
  @include bordered(blue, 1px) // call mixin
;
}

.myNote {
  @include bordered(red, 1px) // call mixin
;
}
```

Also we can define default values

```scss
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}

.myArticle {
  @include bordered($width: 1px) // call mixin
;
}

.myNote {
  @include bordered($color: red) // call mixin
;
}
```

Also one of the common use case of mixin for vendor prefixes

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.myBox {
  @include transform(rotate(20deg));
}
```

We can make @mixin even powerfull using @if and @else
Here is how:

```scss
@mixin theme-switcher($theme) {
  @if $theme == "light" {
    background-color: #f5f5f5;
  } @else {
    background-color: #171c2a;
  }
}

.wrapper {
  @include theme-switcher(dark);
}
```

Not only in mixin we can use if else all over the sass file

#### Now let's talk about Sass Loop and Interpolation

We can loop in sass list
What is list ? in sass we can create list like this `$sizes: 32px, 48px, 72px`;

And then we can loop into this kidda list

```scss
$sizes: 32px, 48px, 72px;
@each $size in $sizes {
  .icon-#{size} {
    font-size: $size;
  }
}
```

here using @each syntex we can do the loop and will get item just like loop in javascript or some other language will get the item $size
And to do the interpolation we need to use this #(hash) sign and then in curly braces the dollor sign along with the variable

#### Now let's talk about Sass Functions

Function works just like regular functions

Here is how we can create an use an function

```scss
@function sum($numbers...) {
  $sum: 0;
  @each $number in $numbers {
    $sum: $sum + $number;
  }
  @return $sum;
}

.hello {
  width: sum(50px, 30px, 100px);
}
```

Also we can use lots of utility functions that makes our life easier

Here is an example:

```scss
$primary: #11141f;

.box {
  background: lighten($primary, 25%);
  color: darken($primary, 30%);
}
```

As we can see these functions are self explainatory

#### Now let's talk about Sass @extend

So Sass @extend lets is share a set of Css properties from one selector to another.
Here is an example:

```scss
.button-basic {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report {
  @extend .button-basic;
  background-color: red;
}

.button-sumit {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```
