# This an exhaustive cheatsheet for sass and its good practices

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

### 2) BEM `amazing-block__element--modifier`

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

