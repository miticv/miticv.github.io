

# Why CSS is painfull

## Color Problem
cannot be variable - if changes need to find all instances to change
Same with fonts, sizes, colors etc.

## Duplication issues
No reusable sections in ss
Rounded corners repeats itelf:
```
border-radius: 5px;
-moz-border-radius: 5px;
-webkit-border-radius: 5px;
```

## Cascading Avalanches
Where cascaded rule is coming from
If change form id will need to change css also where it references it

## Lack of calculations
Cannot base value from any formula
Example: let font be  + 8px from other font...


## Problem with imports


# LESS
*.css is valid *.less file
=== LESS on client
use less.js from less.org that transforms it directly to the client:
```
<head>
 <link rel="stylesheet/less" type="text/css" href="css/my.less" />
 <script src="js/less.js" type="text/javascript"></script>
</head>
```
=== LESS on server
More comonly - caching, speed up the client, etc.

## 
Commnets:
```
//
/* */
```
Imports
```
@import "init";  //imports init.less
@import "colors";  //imports colors.less
```

## Variables

```
@myColor: #ffeedd;  //case sensitive, they are constants!!
@a: Black;  //Color
@b: 4px;    //Units
@c: 1.0em;  //Units
@f: Helvetica, sans serif;  //string
@border: 1px #000 Solid 0 0; //comlex type
```
## Operations

```
font-size: 4px + 4;
font-size: @someVar + 4;
font-size: 20px * .8;   //16px
width: (100% / 2) + 25%;   //75%
```

color functions
```
color: lighten(@color, 10%);   //@color need to be # value and not name to work
color: darken(@color, 10%);

color: saturate(@color, 10%);
color: desaturate(@color, 10%);

color: fadein(@color, 10%);
color: fadeout(@color, 10%);
color: fade(@color, 10%);

color: spin(@color, 10%);  //spin on color wheel
color: mix(@color, #246);  //mix 2 colors
```
Other:
```
@hue: hue(@color);
@sat: saturation(@color);
@sat: lightness(@color);
@sat: alpha(@color);
@sat: hsl(20%, 30%, 40%);

@sat: round(3.14);
@sat: ceil(3.14);
@sat: floor(3.14);
@sat: percentage(.14);
```

## Mixins
Feel like functions, overloads
It starts with a period:

```
.rounded-corners-all(@size: 5px) {   //5px is default value
     border-radius: @size;
    -moz-border-radius: @size;
    -webkit-border-radius: @size;
}

#form
{
  .rounded-corners-all(5px);
  .rounded-corners-all;    // use default value
}
```
variables inside mixins
```
#contact-module {
  @base-size: 24px;
  .fonts() {
    font-size: @base-size;
  }
}

#contact-form{
  @base-size: 18px;
  input{
   #contact-module > .fonts();   //this will use @base-size of 18px, since it is inside that scope (not 24px)
  }
}

```
use overloads:
```
.color(@color){
 color: @color;
}

.color(@color, @factor) {
  color: lighten(@color, @factor);
}

#form {
  .color(#888, 20%); // uses 2nd overload since we use 2 parameters
}
```
using guards:
```
.color(@color) when (alpha(@color) >= 50%){
  color: Black;
}

.color(@color) when (alpha(@color) < 50%){
  color: transparent;
}

#form {
  .color(@mainColor);  // will use 1st or 2nd overload depending on its alpha %
}
```
type guards
```
.width(@size) when (isnumber(@size)) {
 width: @size * 2;
}
.width(@size) when (ispercentage(@size)) {
 width: @size;
}

#form {
.width(50%); //uses 2nd overload
}

```
## Nested rules
using hierarchies
```
nav {
  font-size:14px;
  ul {                           //makes "nav ul {...}"
    list-style-type: none;
    li{                          //makes "nav ul li {...}"
      float: left;
      margin: 2px;
    }
  }
}
```
Combinator
```
a {
 text-decoration: none;
 &:hover {
  text-decoration: underline;
 }
}
```

# Namespaces
not emmmited in css but easier to manage
```
#my-forms{
 .set-button {  
  text-align: center;
 }
 .fonts() {
  font-size: 14px;
  font-family: "Open Sans", Verdana, Helvetica, sans-serif;
 }
}

#submit-button {
 #my-forms > .set-button;
 #my-forms > .fonts();
}
```
## Scoping

```
@size: 24px;  

#form {
   @size: 18px;
   
   .button {
     font-size: @size; //18px;
   }
}
```

## String interpolation

```
@root: "/images/";

#form {
   background: url("@{root}background.jpg");   //becomes url("/images/background.jpg");
}
```
## Using JavaScript
embed JS using backquote: `
```
@root: "/images/";
@app-root: `"@{root}".toUpperCase()`;

#form {
   background: url("@{app-root}background.jpg");   //becomes url("/IMAGES/background.jpg");
}
```


# SASS (and SCSS)
Semantically Awesome Style Sheet
It has 2 syntaxes
* SASS based on indention (not readable)
* CSCC better than above
Supported on server side (not client side) (node, .net etc)
* Chirpy
* nuget (CassAndCoffee)

## Variables

```
$myColor: #ffeedd;  //case sensitive, they are constants!!

#a: Black;  //Color
#b: 4px;    //Units
#c: 1.0em;  //Units
#f: Helvetica, sans serif;  //Lists
#border: 1px #000 Solid 0 0; //comlex type
```
## Operations

```
font-size: 4px + 4;
font-size: @someVar + 4;
font-size: 20px * .8;   //16px
color: #FFF / 4;         // #404040;
width: (100% / 2) + 25%;   //75%
```

Color:
```
color: lighten($color, 10%);   //@color need to be # value and not name to work
color: darken($color, 10%);

color: saturate($color, 10%);
color: desaturate($color, 10%);

color: fade_in($color, .1);  //change opacity
color: fade_out($color, .1);

color: invert($color);
color: complement($color,);
```
More
```
$quoted: quote($sometext);
$unquoted: unquote($sometext);

$value: if(true, $color1, $color2);

@var: round(3.14);
@var: ceil(3.14);
@var: floor(3.14);
@var: percentage(.14);
```
String interpolation
```
$root: "/images/";

#form{
  background: url("#{$root}background.jpg");   //becomes url("/images/background.jpg");
}
//also:
$name: "my-class";
.#{$name} {      //becomes #my-class {
   color: Blue;
}
```
## Rules
nesting:
```
nav {
  font-size:14px;
  ul {                           //makes "nav ul {...}"
    list-style-type: none;
    li{                          //makes "nav ul li {...}"
      float: left;
      margin: 2px;
    }
  }
}
```
parent selector:
```
a {
 text-decoration: none;
 &:hover {
  text-decoration: underline;
 }
}
```
Nested properties
```
.button {
  font:  {
    family: Verdana, Helvetica, sans-serif;
    size: 14px;
  }
}
//Results in:
.button {
  font-family: Verdana, Helvetica, sans-serif;
  font-size: 14px;
}
```

## Directives

import
```
@import "foo.scss"; //embeds in result
@import "foo";
@import "foo.css";
//nested import:
#main{
  @import "colors";
}

```
extend
supports multiple inheritance too
```
.button {
  color: Black;
}

.submit-button {
   @extend .button;     //copy styles from .button
   @extend a:hover;     // inherit from any rule
   border: 1px Black solid;
}
```
mixin
repitable sections (functions)
```
@mixin font-large {
   font: {
     size: 14px;
     family: san-serif;
     weight: bold;
   }
}
#form {
  @include font-large;
}
```
parametirezed:
```
@mixin rounded-corners-all($size: 5px) {   //5px is default value
     border-radius: $size;
    -moz-border-radius: $size;
    -webkit-border-radius: $size;
}

#form
{
   @include rounded-corners-all(5px);
   @include rounded-corners-all;    // use default value
}
```
functions (has return value)
```
$app-width: 900px;
@funxtion column-width($cols) {
   @return ($app-width / $cols) - ($cols * 5px);
}

.col2 {
  width: column-width(2);
}
.col3 {
  width: column-width(3);
}
```
### Control Directives
it is all creating fixed CSSs *not* dynamic ones according to screen size (responsive style)

@if
```
h1 {
  @if $size > 14px {
    color: Blue;
  }
  @else if $size < 14px {
    color: Red;
  }
  @else {
    color: Green;
  }
}
```
@for
```
$page-width: 1000px;
@for $col from 1 through 4 {
  .col#{$col} {
    width: $page-width / $col;
  }
}
```
@each
```
@each $item in first, second, third, fourth {
  .#{$item} {
    background-url: url(/images/#{$item}.jpg);
  }
}
```
@while
```
$i: 1;
@while $i < 5 {
 h#{$i} {
    font-size: $i * 4px;
    $i: $i + 1;
 }
}
```



