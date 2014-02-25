# Crossass Configuration

A dot-syntax configuration (Map) library for Sass.

```scss
$include x-config('color.fg', black);

body {
    color: x-config('color.fg');
}
```

## Features

* Dot-syntax configuration
* Default configuration support
* Straight-forward overriding

## Requirement

* [Sass](http://sass-lang.com/) 3.3.0+

## Installation

```sh
bower install crossass-config
```

or just copy ```crossass-config``` folder into your project.

## Usage

### Import

```scss
@import 'bower_components/crossass-config/scss/config';
```

or

```scss
@import 'your-folder/crossass-config/scss/config';
```

### Default configuration setting

```scss
// _your-partial-file.scss

// Default configuration settings
// Passing true to the 3rd parameter,
// the value is assigned to the configuration path as the default
@include x-config('color.fg', black, true);
@include x-config('color.bg', white, true);

// or assign values to a configuration path by using Map
// @include x-config('color', (fg: black, bg: white), true);
```

### Getting configuration setting

```scss
// your-project-file.scss

@import 'bower_components/crossass-config/scss/config';
@import 'your-partial-file';

body {
    color: x-config('color.fg');  // black
    background-color: x-config('color.bg');  // white
}
```

### Overriding default configuration

```scss
// your-project-file.scss

@import 'bower_components/crossass-config/scss/config';
@import 'your-partial-file';

// Overriding default configuration
@include x-config('color.fg', #666666);

body {
    color: x-config('color.fg');  // #666666
    background-color: x-config('color.bg');  // white
}
```

### Compatibility

x-config() can be compatible with Sass variable.

```scss
@import 'bower_components/crossass-config/scss/config';

// Variables
$color-fg: black !default;
$color-bg: white !default;
$color: (
    fg: $color-fg,
    bg: $color-bg
) !default;

// x-config()
@include x-config('color', $color, true);

body {
    color: x-config('color.fg');  // black
    background-color: x-config('color.bg');  // white
}
```

### Map vs x-config()

```scss
@import 'bower_components/crossass-config/scss/config';

// Map
$config: (
    button: (
        color: (
            fg: white,
            bg: blue
        )
    )
);

// x-config()
$include x-config('button.color.fg', white);
$include x-config('button.color.bg', blue);

// Map
.map {
    color: map-get( map-get( map-get( $config, 'button' ), 'color' ), 'fg' );
    background-color: map-get( map-get( map-get( $config, 'button' ), 'color' ), 'bg' );
}

// x-config()
.x-config {
    color: x-config('button.color.fg');
    background-color: x-config('button.color.bg');
}
```

### !default vs x-config()

```scss
// _your-partial-file-1.scss

// Variable with !default
$var-fg: black !default;

// x-config()
@include x-config('x-config-fg', black, true);
```

```scss
// _your-partial-file-2.scss

// Variables with !default
$var-fg: white !default;
$var-bg: black !default;

// x-config()
@include x-config('x-config-fg', white, true);
@include x-config('x-config-bg', black, true);
```

```scss
// your-project-file.scss

@import 'bower_components/crossass-config/scss/config';
@import 'your-partial-file-1';
@import 'your-partial-file-2';

// Variables
.var-color {
    color: $var-fg;  // black
    background-color: $var-bg;  // black
}

// x-config()
.x-config-color {
    color: x-config('x-config-fg');  // white
    background-color: x-config('x-config-bg');  // black
}
```
