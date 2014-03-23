# Crossass Configuration

A dot-syntax configuration (Map) library for Sass.

```scss
// This is the same as:
// (
//     color: (
//         fg: black
//     )
// )
$include x-config-set('color.fg', black);

body {
    color: x-config-get('color.fg');  // black
}
// So you can also get the raw Map by the path.
// x-config-get('color') returns:
// (
//     fg: black
// )
```

## Features

* Dot-syntax configuration
* Default configuration support

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
@include x-config-set('color.fg', black, true);
@include x-config-set('color.bg', white, true);

// or assign values to a configuration path by using Map
// @include x-config-set('color', (fg: black, bg: white), true);
```

### Getting configuration setting

```scss
// your-project-file.scss

@import 'bower_components/crossass-config/scss/config';
@import 'your-partial-file';

body {
    color: x-config-get('color.fg');  // black
    background-color: x-config-get('color.bg');  // white
}
```

### Overriding default configuration

```scss
// your-project-file.scss

@import 'bower_components/crossass-config/scss/config';
@import 'your-partial-file';

// Overriding default configuration
@include x-config-set('color.fg', #666666);

body {
    color: x-config-get('color.fg');  // #666666
    background-color: x-config-get('color.bg');  // white
}
```

### Compatibility

x-config-get(), x-config-set() can be compatible with Sass variable.

```scss
@import 'bower_components/crossass-config/scss/config';

// Variables
$color-fg: black !default;
$color-bg: white !default;
$color: (
    fg: $color-fg,
    bg: $color-bg
) !default;

// x-config-set()
@include x-config-set('color', $color, true);

body {
    color: x-config-get('color.fg');  // black
    background-color: x-config-get('color.bg');  // white
}
```

### Map vs x-config-get(), x-config-set()

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

// x-config-set()
$include x-config-set('button.color.fg', white);
$include x-config-set('button.color.bg', blue);

// Map
.map {
    color: map-get( map-get( map-get( $config, 'button' ), 'color' ), 'fg' );
    background-color: map-get( map-get( map-get( $config, 'button' ), 'color' ), 'bg' );
}

// x-config-get()
.x-config {
    color: x-config-get('button.color.fg');
    background-color: x-config-get('button.color.bg');
}
```
