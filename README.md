* [Quikster](#home)
* [Get started](#get-started)
* [Settings](#settings)
* [Automatic contrast](#automatic-contrast)
* [Font families](#font-families)
* [Font sizes](#font-sizes)
* [Mixins](#mixins)
* [Functions](#functions)
* [Examples](#extensions)


# Quikster

A starter framework for [](//www.sass-lang.com)that brings useful functions and mixins to start your web project. [see a demo](http://codepen.io/olivier3lanc/pen/mRQRJv) or [get started](#get-started)

## Get started

1. [Download](https://raw.githubusercontent.com/olivier3lanc/Quikster/master/scss/quikster/_quikster.scss)
2. Include `_quikster.scss` file at the very beginning of your SASS/SCSS project. `@import 'quikster'` or `@import '_quikster.scss';`
3. Edit your own settings at the top of the file

## Settings

List of all user parameters to be set at the beginning of the file.

### `$qtr_color_primary`

* **Description**: The main color set by the user from which Quikster starts to compute all others colors.
* **Variable type**: CSS color value.
* Examples:
    - `#30dfd9`
    - `rgb(48, 223, 217)`
    - `rgba(48, 223, 217, 0.5)`
    - `hsl(178, 73%, 53%)`


### `$qtr_smart_contrast`

* **Description**: Enable or disable smart contrast feature. This determines how behaves color contrast. How it works? Quikster calculates primary color luminance and computes contrasted colors accordingly.
* **Variable type**: Boolean.
* Examples:
    * `true`
        * Luminance > 50%
            * Contrasted colors are darker
            * Most contrasted color is black
            * Accented contrasted colors are lighter
            * Most accented contrasted color is white
        * Luminance =< 50%
            * Contrasted colors are lighter
            * Most contrasted color is white
            * Accented contrasted colors are darker
            * Most accented contrasted color is black
    * `false`
        * Luminance > 50%
            * Contrasted colors are lighter
            * Most contrasted color is white
            * Accented contrasted colors are darker
            * Most accented contrasted color is black
        * Luminance =< 50%
            * Contrasted colors are darker
            * Most contrasted color is black
            * Accented contrasted colors are lighter
            * Most accented contrasted color is white

### `$qtr_font_family_default`

* **Description**: Web safe font list that can be used as is or as fallback for custom fonts.
* **Variable type**: CSS list value.
* Examples:
    * `Arial, sans-serif`  
    * `"Times New Roman", serif`


### `$qtr_font_families`

* **Description**: Declarative SASS map where you set all your fonts. Learn more at [Font Families](#font-families) section.
* **Variable type**: SASS map.

Example:
```
/**
FONTS
---
Here you set your font families. Quikster supports local fonts, Google Fonts and web safe fonts
Add as much fonts as you want
Each font is identified with its number

For example:
font-family: qtr-font-family(1);
Will return
font-family: "Aaargh-webfont", Arial, sans-serif;
*/
$qtr_font_families: (
    //Add as much fonts as you want
    //A Local Font
    2: ( //{string} or {number} - ID of the Quikster font family
        type:                               'local', //{string} - Font type:'local'/'google'/'websafe'
        name:                               'Aaargh-webfont', //{string} - File name w/o extension, used as font family name
        path:                               '../fonts/', //{string} - Path or URL to the font directory containing the font files with the previously defined 'name'. Path source is the compiled CSS
        fallback:                           $qtr_font_family_default //{string} - If resource fails to load, this is the fallback system font family name. Each Quikster font family can have its own fallback font family
    ),
    //A Google Font
    1: ( //{string} or {number} - ID of the Quikster font family
        type:                               'google', //{string} - Valid Google Font family name
        name:                               'Montserrat', //{string} - Valid weight for this font family
        weight:                             'Bold', //{string} - If resource fails to load, this is the fallback system font family name. Each font family can have its own fallback font family
        fallback:                          '"Times New Roman", Georgia' //{string} - If resource fails to load, this is the fallback system font family name. Each Quikster font family can have its own fallback font family
    ),
    //A Websafe font
    3: ( //{string} or {number} - ID of the Quikster font family
        type:                               'websafe', //{string} - Font type: 'local'/'google'/'websafe'
        name:                               'Courier, Impact' //{string} - Font family names
    )
);
```

### `$qtr_font_size_unit`

* **Description**: Determines the font size unit (em, rem, px, etc).
* **Variable type**: CSS value.
* Examples:
    * `em`  
    * `rem`  
    * `px`


### `$qtr_font_size_source`

* **Description**: This is the default font size without any unit.
* **Variable type**: Number.
* Examples:
    - `1.2`  
    - `16`

### `$qtr_font_size_largest`

* **Description**: This is the largest font size available in your project.
* **Variable type**: Number.
* Examples:
    - `6`  
    - `72`


### `$qtr_font_size_smallest`

* **Description**: This is the smallest font size available in your project.
* **Variable type**: Number.
* Examples:
    - `0.5`
    - `12`

### `$qtr_screen_mini`

* **Description**: Media width breakpoint between extra-small and small devices. Quikster supports 5 screen widths: Extra-small, small, medium, large and extra-large. This is the break point between extra-small and small devices.
* **Variable type**: CSS value.
* Examples:
    - `34em`  
    - `28rem`  
    - `320px`

### `$qtr_screen_small`

* **Description**: Media width breakpoint between small and medium devices. Quikster supports 5 screen widths: Extra-small, small, medium, large and extra-large. This is the break point between small and medium devices.
* **Variable type**: CSS value.
* Examples:
    - `48em`  
    - `38rem`  
    - `640px`

### `$qtr_screen_medium`

* **Description**: Media width breakpoint between medium and large devices. Quikster supports 5 screen widths: Extra-small, small, medium, large and extra-large. This is the break point between medium and large devices.
* **Variable type**: CSS value.
* Examples:
    - `62em`  
    - `50rem`  
    - `920px`

### `$qtr_screen_large`

* **Description**: Media width breakpoint between large and extra-large devices. Quikster supports 5 screen widths: Extra-small, small, medium, large and extra-large. This is the break point between large and extra-large devices.
* **Variable type**: CSS value.
* Examples:
    - `75em`  
    - `60rem`  
    - `1200px`

### `$qtr_transition_time`

* **Description**: Set a default transition time for your project.
* **Variable type**: CSS value.
* Examples:
    - `300ms`  
    - `0.5s`


## Automatic contrast

**Readable color combinations for better readability.**

Whatever primary color `$qtr_color_primary` you set, Quikster automatically computes new colors with a great contrast ratio.

### Smart contrast

For always readable color combinations. **Get darker if primary color luminance is light, get lighter if primary color luminance is dark.**

* Primary color `qtr-color()`
* Smart contrast 1/6 `qtr-color(1)`
* Smart contrast 2/6 `qtr-color(2)`
* Smart contrast 3/6 `qtr-color(3)`
* Smart contrast 4/6 `qtr-color(4)`
* Smart contrast 5/6 `qtr-color(5)`
* Smart contrast 6/6(max) `qtr-color(6)` (always renders black or white)

### Accentuated contrast

To force color primary luminance. **Get darker if primary color luminance is dark, get lighter if primary color luminance is light.**

* Primary color `qtr-color()`
* Accentuated contrast 1/6 `qtr-color(-1)`
* Accentuated contrast 2/6 `qtr-color(-2)`
* Accentuated contrast 3/6 `qtr-color(-3)`
* Accentuated contrast 4/6 `qtr-color(-4)`
* Accentuated contrast 5/6 `qtr-color(-5)`
* Accentuated contrast 6/6(max) `qtr-color(-6)` (always renders black or white)

### Smart Contrast Max

The primary color and its computed smart contrasted colors allow the foreground to always keep a good readability in relation with the background. With current CSS, this text is always readable whatever color primary you set.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(6);
}
```

### Smart Contrast Max

The primary color and its computed smart contrasted colors allow the foreground to always keep a good readability in relation with the background. With current CSS, this text is always readable whatever color primary you set.

```
.myClass {
    color: qtr-color(6);
    background-color: qtr-color();
}
```


### Smart Contrast 1

First contrast level between text color and background color.

```
.myClass {
    color: qtr-color(1);
    background-color: qtr-color();
}
```


### Smart Contrast 1

First contrast level between text color and background color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(1);
}
```


### Smart Contrast 2

2/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color(2);
    background-color: qtr-color();
}
```


### Smart Contrast 2

2/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(2);
}
```


### Smart Contrast 3

3/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color(3);
    background-color: qtr-color();
}
```


### Smart Contrast 3

3/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(3);
}
```


### Smart Contrast 4

4/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color(4);
    background-color: qtr-color();
}
```


### Smart Contrast 4

4/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(4);
}
```


### Smart Contrast 5

5/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color(5);
    background-color: qtr-color();
}
```


### Smart Contrast 5

5/6 contrast level between text color and background color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(5);
}
```


### Accentuated Contrast Max

In opposition to the smart contrast, accentuated colors accentuate the primary color luminance.

* If luminance is below 50%, accentuated colors are darkened.
* If luminance is above 50%, accentuated colors are lightened.

```
/*
WARNING!
---
Using accentuated mode (by disabling smart contrast)
does not guarantee readability. According to your
primary color luminance (near 100% or 0%), accentuated contrast color
combinations with primary color may not assure a good readability
*/
.myClass {
    color: qtr-color();
    background-color: qtr-color(-6);
}
```

### Custom color 1

Quikster computes contrasted colors from a custom color.

`.myClass {
    color: red;
    background-color: qtr-color(5,red);
}`


### Custom color 1

Quikster computes contrasted colors from a custom color.

```
.myClass {
    color: qtr-color(5,red);
    background-color: red;
}
```



### Custom color 2

Quikster computes contrasted colors from a custom color.

```
.myClass {
    color: #123456;
    background-color: qtr-color(4,#123456);
}
```



### Custom color 2

Quikster computes contrasted colors from a custom color.

```
.myClass {
    color: qtr-color(4,#123456);
    background-color: #123456;
}
```



### Custom color 3

Quikster computes contrasted colors from a custom color.

```
.myClass {
    color: rgba(#654321,.6);
    background-color: qtr-color(5,rgba(#654321,.6));
}
```



### Custom color 3

Quikster computes contrasted colors from a custom color.

```
.myClass {
    color: qtr-color(5,rgba(#654321,.6));
    background-color: rgba(#654321,.6);
}
```



### Triadic 1

Quikster computes triadic colors from your primary color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(triadic1);
}
```



### Triadic 1

Quikster computes triadic colors from your primary color.

```
.myClass {
    color: qtr-color(triadic1);
    background-color: qtr-color();
}
```



### Triadic 2

Quikster computes triadic colors from your primary color.

```
.myClass {
    color: qtr-color(triadic2);
    background-color: qtr-color();
}
```



### Triadic 2

Quikster computes triadic colors from your primary color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(triadic2);
}
```



### Complementary

Quikster computes complementary color from your primary color.

```
.myClass {
    color: qtr-color();
    background-color: qtr-color(complement);
}
```



### Complementary

Quikster computes complementary color from your primary color

```
.myClass {
    color: qtr-color(complement);
    background-color: qtr-color();
}
```



## Font families

Quikster easily manages local fonts, Google Fonts and web safe fonts.

### Declaration 1

```
//SETTINGS
$qtr_font_families: (
    //Add as much fonts as you want
    //A Local Font
    1: (                                            //{string} or {number} - ID of the Quikster font family
        type:       'local',                        //{string} - Font type:'local'/'google'/'websafe'
        name:       'Aaargh-webfont',               //{string} - File name w/o extension of the font file
                                                    //This name will be used font family name
        path:       '../fonts/',                    //{string} - Path or URL to the font directory containing
                                                    //the font files with the previously defined 'name'.
                                                    //Path source is the compiled CSS file path
        fallback:   $qtr_font_family_default        //{string} - If resource fails to load,
                                                    //this is the fallback web safe font family name.
                                                    //Each Quikster font family can have its own fallback font family
    ),
    //A Google Font
    2: (                                            //{string} or {number} - ID of the Quikster font family
        type:       'google',                       //{string} - Font type:'local'/'google'/'websafe'
        name:       'Montserrat',                   //{string} - Valid Google Font family name
        weight:     'Bold',                         //{string} - Valid Google Font family weight
                                                    //Leaving empty '' assigns the default weight
        fallback:   '"Times New Roman", Georgia'    //{string} - If resource fails to load,
                                                    //this is the fallback web safe font family name.
                                                    //Each Quikster font family can have its own fallback font family
    ),
    //A web safe font
    3: (                                            //{string} or {number} - ID of the Quikster font family
        type:       'websafe',                      //{string} - Font type:'local'/'google'/'websafe'
        name:       'Courier, Impact'               //{string} - Web safe font family list
    )
);
```

### Usage 1

```
//USAGE EXAMPLE 1
.myClass {
    font-family: qtr-font-family(1);
}
.myClass2 {
    font-family: qtr-font-family(2);
}
.myClass3 {
    font-family: qtr-font-family(3);
}
```



### Compilation 1

```
//COMPILATION EXAMPLE 1
@import url("https://fonts.googleapis.com/css?family=Montserrat:Bold");
@font-face {
    font-family: "Aaargh-webfont";
    src: url("../fonts/Aaargh-webfont.ttf") format("truetype"),
         url("../fonts/Aaargh-webfont.woff") format("woff"),
         url("../fonts/Aaargh-webfont.svg") format("svg");
    font-weight: normal;
    font-style: normal;
}
//COMPILED CLASSES
.myClass {
    font-family: "Aaargh-webfont", Arial, sans-serif;
}

.myClass2 {
    font-family: "Montserrat", Arial, sans-serif;
}

.myClass3 {
    font-family: Courier, Impact;
}
```

### Declaration 2

```
//SETTINGS EXAMPLE 2
$qtr_font_families: (
    customStringID: (
        type:       'local',
        name:       'Aaargh-webfont',
        path:       'http://www.example.com/fonts/',
        fallback:   $qtr_font_family_default
    ),
    2: (
        type:       'google',
        name:       'Open Sans',
        weight:     '',
        fallback:   '"Times New Roman", Georgia'
    ),
    extra: (
        type:       'websafe',
        name:       'Courier'
    ),
    extra2: (
        type:       'websafe',
        name:       '"Comic Sans MS"'
    )
);
```



### Usage 2

```
//USAGE EXAMPLE 2
.myClass {
    font-family: qtr-font-family(customStringID);
}
.myClass2 {
    font-family: qtr-font-family(2);
}
.myClass3 {
    font-family: qtr-font-family(extra);
}
.myClass4 {
    font-family: qtr-font-family(extra2);
}
```

### Compilation 2

```
//COMPILATION EXAMPLE 2
@import url("https://fonts.googleapis.com/css?family=Open Sans");
@font-face {
    font-family: "Aaargh-webfont";
    src: url("http://www.example.com/fonts/Aaargh-webfont.ttf") format("truetype"),
         url("http://www.example.com/fonts/Aaargh-webfont.woff") format("woff"),
         url("http://www.example.com/fonts/Aaargh-webfont.svg") format("svg");
    font-weight: normal;
    font-style: normal;
}
.myClass {
    font-family: "Aaargh-webfont", Arial, sans-serif;
}

.myClass2 {
    font-family: "Open Sans", "Times New Roman", Georgia;
}

.myClass3 {
    font-family: Courier;
}

.myClass4 {
    font-family: "Comic Sans MS";
}
```



## Font sizes

Quikster provides 13 font sizes automatically computed from `$qtr_font_size_source`, `$qtr_font_size_largest` and `$qtr_font_size_smallest`.

### The largest font size `qtr-font-size(6)`

```
/**
*    How it works?
*    Quikster applies the largest font size
*    that is set in settings $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(6);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(6,raw) //returns the largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(6,raw)*2+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 6em;
}
.myClass2 {
    font-size: 12px;
}
```


### The 5/6 largest font size `qtr-font-size(5)`

```/**
*    How it works?
*    Quikster computes the 5th largest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(5);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(5,raw) returns the 5/6 largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(5,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 5.233em;
}
.myClass2 {
    font-size: 52.33px;
}
```


### The 4/6 largest font size `qtr-font-size(4)`

```/**
*    How it works?
*    Quikster computes the 4th largest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(4);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(4,raw) returns the 4/6 largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(4,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 4.4666em;
}
.myClass2 {
    font-size: 44.666px;
}
```


### The 3/6 largest font size `qtr-font-size(3)`

```/**
*    How it works?
*    Quikster computes the 3rd largest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(3);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(3,raw) returns the 3/6 largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(3,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 3.7em;
}
.myClass2 {
    font-size: 37em;
}
```


### The 2/6 largest font size `qtr-font-size(2)`

```/**
*    How it works?
*    Quikster computes the 2nd largest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(2);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(2,raw) returns the 2/6 largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(2,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 2.93em;
}
.myClass2 {
    font-size: 29.3em;
}
```


### The 1/6 largest font size `qtr-font-size(1)`

```/**
*    How it works?
*    Quikster computes the 1st largest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_largest
*/
.myClass {
    font-size: qtr-font-size(1);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(1,raw) returns the 1/6 largest font as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(1,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 2.16em;
}
.myClass2 {
    font-size: 21.6em;
}
```


### The default font size `qtr-font-size()`

```/**
*    This is the default font size based on $qtr_font_size_source
*    $qtr_font_size_base = $qtr_font_size_source;
*/
.myClass {
    font-size: qtr-font-size();
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(0,raw) returns the source / base font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(0,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_largest = 6
*/
.myClass {
    font-size: 1.4em;
}
.myClass2 {
    font-size: 14em;
}
```


### The 1/6 smallest font size `qtr-font-size(-1)`

```/**
*    How it works?
*    Quikster computes the 1st smallest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-1);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-1,raw) returns the 1/6 smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-1,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 1.275em;
}
.myClass2 {
    font-size: 12.75em;
}
```


### The 2/6 smallest font size `qtr-font-size(-2)`

```/**
*    How it works?
*    Quikster computes the 2nd smallest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-2);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-2,raw) returns the 2/6 smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-2,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 1.15em;
}
.myClass2 {
    font-size: 11.5em;
}
```


### The 3/6 smallest font size `qtr-font-size(-3)`

```/**
*    How it works?
*    Quikster computes the 3rd smallest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-3);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-3,raw) returns the 3/6 smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-3,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 1.025em;
}
.myClass2 {
    font-size: 10.25em;
}
```


### The 4/6 smallest font size `qtr-font-size(-4)`

```/**
*    How it works?
*    Quikster computes the 4th smallest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-4);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-4,raw) returns the 4/6 smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-4,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 0.9em;
}
.myClass2 {
    font-size: 9em;
}
```


### The 5/6 smallest font size `qtr-font-size(-5)`

```/**
*    How it works?
*    Quikster computes the 5th smallest font size
*    computed from the $qtr_font_size_source and the $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-5);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-5,raw) returns the 5/6 smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-5,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 0.775em;
}
.myClass2 {
    font-size: 7.75em;
}
```


### The smallest font size `qtr-font-size(-6)`

```
/**
*    How it works?
*    Quikster applies the smallest font size
*    that is set in settings $qtr_font_size_smallest
*/
.myClass {
    font-size: qtr-font-size(-6);
}
//Optionally add 'raw' as second argument to return only the number value
//qtr-font-size(-6,raw) returns the smallest font size as a number
//Allows to easily recompute
.myClass2 {
    font-size: qtr-font-size(-6,raw)*10+px;
}

/**
*   Render with current settings
*   $qtr_font_size_unit = em
*   $qtr_font_size_source = 1.4
*   $qtr_font_size_smallest = 0.65
*/
.myClass {
    font-size: 0.65em;
}
.myClass2 {
    font-size: 6.5em;
}
```


## Mixins

Quikster comes with some essential [SASS](//www.sass-lang.com) mixins.

### Screens

Quikster support 5 screen sizes:

* Extra-small `xs`
* Small `sm`
* Medium `md`
* Large `lg`
* Extra-large `xl`

Simply include screen sizes in argument list `@include qtr-screen(list of screen sizes)`.

```
/*
* COMBINATION OF SCREENS
* ---
*/
@include qtr-screen(xs,sm,md) {
    .myClass { }
}

// Equivalent to
@media (max-width: $qtr_screen_mini) {
    .myClass { }
}
@media (min-width: $qtr_screen_mini) and (max-width: $qtr_screen_small) {
    .myClass { }
}
@media (min-width: $qtr_screen_small) and (max-width: $qtr_screen_medium) {
    .myClass { }
}

// Renders with current settings
@media (max-width: 34em) {
    .myClass { }
}
@media (min-width: 34em) and (max-width: 48em) {
    .myClass { }
}
@media (min-width: 48em) and (max-width: 62em) {
    .myClass { }
}

/*
* ONLY FOR EXTRA-SMALL SCREENS
* ---
*/
@include qtr-screen(xs) {
    .myClass { }
}

// Equivalent to
@media (max-width: $qtr_screen_mini) {
    .myClass { }
}

// Renders with current settings
@media (max-width: 34em) {
    .myClass { }
}


/*
* ONLY FOR SMALL SCREENS
* ---
*/
@include qtr-screen(sm) {
    .myClass { }
}

// Equivalent to
@media (min-width: $qtr_screen_mini) and (max-width: $qtr_screen_small) {
    .myClass { }
}

// Renders with current settings
@media (min-width: 34em) and (max-width: 48em) {
    .myClass { }
}


/*
* ONLY FOR MEDIUM SCREENS
* ---
*/
@include qtr-screen(md) {
    .myClass { }
}

// Equivalent to
@media (min-width: $qtr_screen_small) and (max-width: $qtr_screen_medium) {
    .myClass { }
}

// Renders with current settings
@media (min-width: 48em) and (max-width: 62em) {
    .myClass { }
}


/*
* ONLY FOR LARGE SCREENS
* ---
*/
@include qtr-screen(lg) {
    .myClass { }
}

// Equivalent to
@media (min-width: $qtr_screen_medium) and (max-width: $qtr_screen_large) {
    .myClass { }
}

// Renders with current settings
@media (min-width: 62em) and (max-width: 75em) {
    .myClass { }
}


/*
* ONLY FOR EXTRA-LARGE SCREENS
* ---
*/
@include qtr-screen(xl) {
    .myClass { }
}

// Equivalent to
@media (min-width: $qtr_screen_large) {
    .myClass { }
}

// Renders with current settings
@media (min-width: 75em) {
    .myClass { }
}
```

### Background gradient

Simple CSS3 gradient `@include qtr-background-gradient($color1, $color2, $angle)`

```
/*
* BACKGROUND GRADIENT
* Simple CSS3 gradient
* ---
*/
//$color1 is the start color, $color2 is the finish color, $angle is the angle
.myClass {
    @include qtr-background-gradient($color1, $color2, $angle);
}

// Use case
.myClass {
    @include qtr-background-gradient(red, orange, -45deg);
}

// Renders with default values
.myClass {
    background: red; /* For browsers that do not support gradients */
    background: -webkit-linear-gradient(-45deg, red, orange); /* For Safari 5.1 to 6.0 */
    background: -o-linear-gradient(-45deg, red, orange); /* For Opera 11.1 to 12.0 */
    background: -moz-linear-gradient(-45deg, red, orange); /* For Firefox 3.6 to 15 */
    background: linear-gradient(-45deg, red, orange); /* Standard syntax */
}
```

## Functions

List of all available Quikster functions.

## `qtr-color($step, $color)`

* **Description**: Returns a computed contrasted color. All arguments are optional.. See [automatic contrast](#automatic-contrast) section for [examples](#automatic-contrast)  
* **Return value**: CSS value
* Arguments
    `$step` _required_
        * Type: Integer
        * Default `$step` = `0`
        * Values can be from -6 to 6, defines the contrast level. Level 6 is black or white according to the `$color` and `$smart_contrast`
    `$color` _optional_
        * Type: CSS color
        * Default: `$qtr_color_primary`
        * Useful when you need to get a contrasted color from a custom color. If set, returns a color contrasted with the defined `$step`

Basic examples:

* `qtr-color(6)` returns **the smartest contrasted color** (always black or white) from `$qtr_color_primary`
* `qtr-color(5)` returns **5/6 contrasted color** from `$qtr_color_primary`
* `qtr-color(4)` returns **4/6 contrasted color** from `$qtr_color_primary`
* `qtr-color(3)` returns **3/6 contrasted color** from `$qtr_color_primary`
* `qtr-color(2)` returns **2/6 contrasted color** from `$qtr_color_primary`
* `qtr-color(1)` returns **1/6 contrasted color** from `$qtr_color_primary`
* `qtr-color()` or `qtr-color(0)` returns `$qtr_color_primary`
* `qtr-color(-1)` returns **1/6 accentuated contrast color** from `$qtr_color_primary`
* `qtr-color(-2)` returns **2/6 accentuated contrast color** from `$qtr_color_primary`
* `qtr-color(-3)` returns **3/6 accentuated contrast color** from `$qtr_color_primary`
* `qtr-color(-4)` returns **4/6 accentuated contrast color** from `$qtr_color_primary`
* `qtr-color(-5)` returns **5/6 accentuated contrast color** from `$qtr_color_primary`
* `qtr-color(-6)` returns **the most accentuated contrast color** (always black or white) from `$qtr_color_primary`

Advanced examples:

* `qtr-color(6,#fe3abc)` returns the fully contrasted color from `#fe3abc`
* `qtr-color(-6,#fe3abc)` returns the fully accentuated contrast color from `#fe3abc`
* `qtr-color(3,#fe3abc)` returns the 3/6 contrasted color from `#fe3abc`
* `qtr-color(-3,#fe3abc)` returns the 3/6 accentuated contrast color from `#fe3abc`

## `qtr-font-family($id)`

* **Description**: Returns the specified font family list from the `$qtr_font_families` map in user settings. See [font families](#font-families) section for [examples](#font-families).
* **Return value**: CSS list

## `qtr-font-size($size, $return_type)`

* **Description**: Returns CSS font size value **with its font size unit** defined in parameters. All arguments are optional. See [font sizes](#font-sizes) section for [examples](#font-sizes)  
* **Return value**: CSS value
* Arguments
    * `size` _integer_ (-6 to 6 ) _required_ returns:
        * **The largest font size with its unit** according to the `$qtr_font_size_largest`
        * **The 5/6 largest font size with its unit** computed from `$qtr_font_size_largest` and `$qtr_font_size_source`
        * **The 4/6 largest font size with its unit** computed from `$qtr_font_size_largest` and `$qtr_font_size_source`
        * **The 3/6 largest font size with its unit** computed from `$qtr_font_size_largest` and `$qtr_font_size_source`
        * **The 2/6 largest font size with its unit** computed from `$qtr_font_size_largest` and `$qtr_font_size_source`
        * **The 1/6 largest font size with its unit** computed from `$qtr_font_size_largest` and `$qtr_font_size_source`
        * **The default font size with its unit** which is the same as `$qtr_font_size_source`
        * **The 1/6 smallest font size with its unit** computed from `$qtr_font_size_smallest` and `$qtr_font_size_source`
        * **The 2/6 smallest font size with its unit** computed from `$qtr_font_size_smallest` and `$qtr_font_size_source`
        * **The 3/6 smallest font size with its unit** computed from `$qtr_font_size_smallest` and `$qtr_font_size_source`
        * **The 4/6 smallest font size with its unit** computed from `$qtr_font_size_smallest` and `$qtr_font_size_source`
        * **The 5/6 smallest font size with its unit** computed from `$qtr_font_size_smallest` and `$qtr_font_size_source`
        * **The smallest font size with its unit** according to the `$qtr_font_size_smallest`
    * `$return_type`_optional_ _string_ if set to `raw` **returns the value as a number** without any font unit


```
/*
* EXAMPLES WITH RAW VALUES
* ---
* Assumes current settings
* $qtr_font_size_largest: 6
* $qtr_font_size_source: 1.4
* $qtr_font_size_smallest: 0.65
* $qtr_font_size_unit: em
*/

//RAW allows additional calculations in your code
20 * qtr-font-size(0,raw);
//Compiles 20 * 1.4
28

//RAW value to get a custom font size from and custom unit
.myClass {
    font-size: 20 * qtr-font-size(-6,raw) +px;
}
//Compiles 20 * 0.65 px
.myClass {
    font-size: 13px;
}
```



## Examples made with Quikster

Here are a list of ready to use CSS classes made with Quikster.

[Simple Grid](./scss/components/_grid.scss)

A simple and lightweight responsive CSS grid.

[Basic Fonts](./scss/components/_fonts.scss)

Assign default font families and font sizes to basic HTML tags.
