# SASS

Here is a link to the [Sass documentation](https://sass-lang.com/documentation)

To install sass simply run `npm install sass -g`

And to use sass run `sass --watch ./sass/main.scss:./generated/css/style.css --style compressed`

## I) Architecture and syntax

### 1) 7-1 Model 7 directories (with partial files) and 1 scss file (main.scss) !

sass/

    bases/                  // general norms, font, spacing
        _base.scss
        _typography.scss
    components/             // small independant blocks
        _button.scss
        _input.scss
    layouts/                // big reusable containers
        _form.scss
        _headers.scss
        _nav.scss
    pages/                  // styles specifi to one page
        _about.scss
        _project.scss
    themes/                 // theme color
        _main_theme.scss
        _dark_theme.scss
    utils/                  // some variables, functions, mixins, placeholders
        _functions.scss
        _mixins.scss
        _placeholders.scss
        _variables.scss
    vendors/                // external libs
        _bootstrap.scss
        _material.scss
    main.scss               // the main files with all above partial files imported with @import "./bases/base"

### 2) BEM : `block__element--modifier`

```scss
.container {                // Block: standalone entity that is meaningful on its own
    color: red;
    &__title {              // Element: part of a block, semantically tied to its block
        font-weight: bold;
    }
    &&--orange {            // Modifier: flag that changes apparance or behavior
        color: orange;
    }
    &__description {
        font-size: 10px;
        &--orange {         // modifier ca also be applied on elements
            color: orange;
        }
    }
}
```

### 3) Nesting

```scss
.parent {               // Parent block
    color: black;
    .descendant {       // The descendant contained in the parent 
        color: green;
    }
    >.child {           // A direct child of the parent
        color: red;
    }
    +.adjacent {        // A block right after the parent
        color: purple;
    }
    &:focus {           // Change the pseudo-class of the parent
        color: orange;
    }
}
```

## II) Algorithmics

### 1) Variables

```scss
$mint: #15DEA5;                 // Color type
$default-font: 'Lucida';        // String type
$border-radius: 3px;            // Number type: integer, decimal, with unit, ...
$null-value: null;              // Null type
$isDisabled: true;              // Boolean type
$border: 1px solid #f5ebfc;     // List type
$red-map: (                     // Map type
    light: #e57373, 
    medium: #f44336, 
    dark: #b71c1c
);
```

### 2) Operators

```scss
1px == 1px;                 // true
1px == 1em;                 // false
1 != 1px;                   // true
"Helvetica" == Helvetica;   // true
100 > 50;                   // true
96px >= 1in;                // true

10s + 15s;                  // 25s
1in % 9px;                  // 0.0625in
-(10px - 15px);             // 5px
15px/30px + 1;              // 1.5

"Helvetica" + " Neue";      // "Helvetica Neue"
sans- + serif;              // sans-serif
"Elapsed time: " + 10s;     // "Elapsed time: 10s";

not false;                  // true
true and false;             // false
true or false;              // true
```

### 4) Condition

```scss
@if (hue($color) < 180) {
    $color: adjust-hue($color, 30);
} @else {
    $color: adjust-hue($color, -60);
}
```

### 3) Loop

```scss
@each $key, $value in $map {
    .btn--#{$key} {
        background-color: $value;
    }
}
```

### 4) Fonctions

Create your own function:

```scss
@function pastel($clr) {
    @return hsl(hue($clr), 100%, 90%);
}
```

Or use built-in ones:

```scss
hue($color)                 // Returns the hue of $color as a number between 0deg and 360deg.
darken($color, $amount)     // Decreases the HSL lightness of $color by $amount

length($string)             // Returns the number of characters in $string.
slice($string, $start-at,   // Returns the slice of $string starting at index $start-at 
    $end-at: -1)            // and ending at index $end-at (both inclusive)

append($list, $val)         // Returns a copy of $list with $val added to the end.
nth($list, $n)              // Returns the element of $list at index $n.

has-key($map, $key)         // Returns whether $map contains a value associated with $key.
map-get($map, $key)         // Returns the value in $map associated with $key
```

## III) Scss specificities

### 1) Mixins define style (class) that can be re-used

```scss
// $image is a mandatory parameter. $x and $y are optional with default values
// Can also take arbitrary number of arguments with `...`
@mixin replace-text($image, $x: 50%, $y: 50%) {
    text-align: left;
    
    background: {
        image: $image;
        repeat: no-repeat;
        position: $x $y;
    }
}

.mail-icon {
    @include replace-text(url("/images/mail.svg"), 0);
}
```

### 2) Extensions & Placeholders
```scss
%center {                   // This placeholder won't appear in the compiled css
	display: block;
	margin-left: auto;
	margin-right: auto;
}

.error {
    border: 1px #f00;
    background-color: #fdd;
    
    &--serious {
        @extend .error;     // Will add all the styles defined in .error
        @extend %center;    // Will add all the styles defined in %center    
        border-width: 3px;
  }
}
```

### 3) Media queries & content

```scss
$breakpoints: (mobile: 599px);

@mixin mobile-only {
    @media screen and (max-width: map-get($breakpoints, mobile)) {
        @content;
    }
}

.proj-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    @include mobile-only {
        grid-template-columns: 1fr;
    }
}
```

### 4) Autoprefixer

Externel collection of mixins to add vendor prefixes directly in sass/scss.

```batch
npm install autoprefixer postcss postcss-cli -g
npm run prefix
```

