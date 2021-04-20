# Framingo
A scss pack named framingo by Fryan

## Installation
### Import Basic
Import basic config files
```scss
@import '~framingo/src/config/index;
@import '~framingo;
```

### Config Files
All of these are required to import
```scss
@import '~framingo/src/config/_breakpoint.scss;
@import '~framingo/src/config/_color.scss;
@import '~framingo/src/config/_passphrase.scss;
@import '~framingo/src/config/_setting.scss;
@import '~framingo/src/config/_spacing.scss;
@import '~framingo';
```

## Custom config

### passphrase
```scss
$passphrase: 'fr'; // custom
```
### Breakpoint
```scss
$breakpoint-map: (
  'xs': 320, // custom
  'sm': 576, // custom extend bootstrap4
  'md': 768, // custom extend bootstrap4
  'lg': 992, // custom extend bootstrap4
  'xl': 1200, // custom extend bootstrap4
  'xxl': 1440, // custom
  'xxxl': 1600 // custom
) !default;
```

### Color
```scss
$colors: (
  'light': (
    'red': $color-red, // custom color
    // following items are required
    'font': rgb(80, 80, 80),
    'background': rgb(255, 254, 250),
    'contentBackground': mix(rgb(255, 254, 250), black, 90%),
    'borderColor': rgb(200, 200, 200),
  ),
  'dark': (
    'red': $color-red, // custom color
    // following items are required
    'font': rgba(255, 255, 255, .85),
    'background': rgb(19, 29, 36),
    'contentBackground': mix(rgb(19, 29, 36), white, 97%),
    'borderColor': rgba(255, 255, 255, .1),
  )
) !default;

// Define Color Map
// following items are required
$color-light-map: map-get($colors, 'light') !default;
$color-dark-map: '' !default;
@if map-has-key($colors, 'dark') {
  $color-dark-map: map-get($colors, 'dark');
}
```

### Setting
```scss
$settings: (
  // following item are required
  'inputHeight': 2.3em,
  'inputPadding': .3em .5em,
  'inputPaddingLg': .5em .8em,
  'inputRadius': .3rem,
  'inputBorderWidth': 1px
);
```

### spacing
```scss
$spacing-map: (
  // following items are required
  '1': .35rem,
  '2': .8rem,
  '3': 1.25rem,
  '4': 1.7rem,
  '5': 2.15rem
);
```

## Usage

### Variables
#### CSS Gloabl Var
```css
color: var(--${passphrase}--color-red);
```
#### Color
```scss
color: color(font);
background: color(background, light');
border-color: color(borderColor, l);
```

#### Breakpoint
```scss
breakpoint(xs);
```

#### Spacing
```scss
padding: spacing(3) spacing(2);
margin: spacing(1);
```

#### Setting
```scss
input {
    height: setting(inputHeight);
}
```

### Form
```html
<form class="{$passphrase} form loading">
    <span class="title">Title</span>
    <input type="text">
</form>
```

### Table
```html
<div class="{$passphrase} table">
    <table>
        <tHead>
            <tr>
                <th>HEAD1</th>
                <th>HEAD2</th>
        </tHead>
        <tBody>
            <tr>
                <td>Body1</td>
                <td>Body2</td>
            </tr>
        </tBody>
    </table>
</div>
```

### Breakpoint
Above the breakpoint
```scss
@include breakpoint-u(768px) {}
@include bku(md) {} 
@include bku(breakpoint(md)) {}
```
Below the breakpoint
```scss
@include breakpoint-d(768px) {}
@include bkd(768px) {}
@include bkd(breakpoint(md)) {}
```
Between breakpoints
```scss
@include breakpoint-b(576px, 768px) {}
@include bkb(sm, md) {}
@include bkb(breakpoint(sm), breakpoint(md)( {}
```

### Extend parent
#### ParentExtended
parent($parent, $parentExtend, $child);
```scss
body {
    $parent: &;
    .child {
        @include parent($parent, .modal-open, &) {
            color: red;
        }
    }
}
```
Export As
```css
body.modal-open .child { color: red; }
```

#### Language Extended
language($language-type: 'tw', 'en', 'cn');
```scss
.child{
    @include language('tw') {
        color: red;
    }
}
```
Export as
```css
html:lan(zh-Hant-TW) .child { color: red; }
```

#### Replace Extended
parent-replace($class, $class-replace);
```scss
.child.active{
    @include parent-replace(.active, '.inactive') {
        color: red;
    }
}
```
Export as
```css
.child.inactive { color: red; }
```

### Themify
themify(light') // Light, light, L, l, Dark, dark, D, d
```scss
.child {
    @include themify(light) { color :red };
    @include light { color :red };
    @inlcude theme(l) { color: red };
}
```
Export as
```css
@media(prefers-color-scheme: 'light') {
    body[data-prefers-color="auto"] .child { color: red; }
}
body[data-prefers-color="light"] .child {
    color: red;
}
```


### Animate
```scss
keyframe: {$passphrase}-animate-rolling 1s ease;
keyframe: {$passphrase}-animate-moveRight 1s ease;
keyframe: {$passphrase}-animate-moveLeft 1s ease;
keyframe: {$passphrase}-animate-moveTop 1s ease;
keyframe: {$passphrase}-animate-moveBottom 1s ease;
```

### transition
```scss
@include transition(.3s ease); // custom
@extend %transition; // global default .3s ease
```

### Loading
```scss
.background{ @extend %fr-loading-background; }
.background .loadingItem { @extend %fr-loading-circle; }
```

### MultipleSelector
```scss
$m: multipleSelector('.a, .b .c');
@debug $m; // return as array
```
```scss
str-split($string, $separator: string);
$m: str-split('.a, .b, .c, .d', ',');
@debug $m;
```
