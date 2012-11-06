Dev Meeting - Sass & Compass Talk
========
This repo contains the results of the live-coding session to introduce features of Sass and Compass.

- `stylesheets/bad.css` - our vanilla css file
- `sass/base.scss`  - port of `bad.css` to sass

A bash script was written to handle Sass/Compass/Ruby [installation](https://gist.github.com/3694114) 
**Usage**
    ./setup-sass.sh [-h|--help] [--with-rvm]

Here's a rundown of what was discussed:

Compass
-------
A command line utlity which includes helpful modules (e.g. CSS3 helpers)
The configuration file `config.rb` allows you to set input/output directories, minified/expanded output etc.

`compass compile` - Compile all sass files
`compass watch ` - Set observer to compile sass files upon saving

Sass
-------
Sass is a CSS Preprocess which extends CSS by adding programmatical syntax.

Variables - look like `$variable: something;`
Nesting

**Modules**
`@import 'module-name'` - allow importing of helper modules

Prepending an underscore to a module (e.g. `_mixins.scss`) will not generate a .css file. Importing these submodules in a sass file, you do not have to specify the underscore.

**Property Inheritance**
Use the `@extend` annotation. 

The placeholder selector (`%`) can be used if you do not want the selector to be included in the css file. This is helpful if the selector is ONLY being used to extend properties from.

**Operations**

Sass supports mathematical operations on properties:

    color: #010203 + #040506;
    color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);

**Loop Directives**

Sass supports `@for`, `@each`, and `@while` loops.

    @for $i from 1 through 3 {
        .grid_#{$i} {
            width: $column-width * $i;
        }
    }

**Control Directives**

Sass has support for `@if`, `@else` constructs

    @mixin button($type) {
        @if ($color == 'glossy') {
            // do clossy stuff
        }

        @else if ($color == 'matte') {
            // do matte stuff
        }
    }


**Mixin & Function Directives**

Function and mixin support. Use functions purely for value manipulation (e.g. you could write a function to convert px to em). Mixins affect purely styles.

    @function px-to-em ($target, $context:16px) {
        @return ($target / $context) * 1em;
    }


    @mixin opacity($opacity) {
        filter: alpha(opacity=#{$opacity});
        opacity: $opacity * 0.01;                      
    }

They are used differently:

    .transparent-pane {
        font-size: px-to-em(14px);

        @include opacity(0.9);
    }

There is also a ruby-like construct equivalent to `yield` that allows us to pass content blocks into mixins. Makes it easy for responsive css

    @mixin respond-to($media) {
        @if ($media == 'mobile') {
            @media only screen and (max-width: 480px) { @content }
        }
    }

    .container {
        width: 960px;

        @include respond-to('mobile') {
            width: 480px;
        }
    }









