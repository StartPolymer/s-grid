[![Published on webcomponents.org][webcomponents-image]][webcomponents-url]

##&lt;s-grid&gt;

`s-grid` is a helper class useful for creating responsive, fluid grid layouts using CSS Custom Properties.
Because custom properties can be defined inside a `@media` rule, you can customize the grid layout
for different responsive breakpoints.

`s-grid` is up-to-date fork of [`app-grid`](https://github.com/PolymerElements/app-layout/tree/master/app-grid)

## New Features

- Grids can be nested using 4 class modifiers `s-grid-1`, `s-grid-2`, `s-grid-3`, `s-grid-4`
- CSS properties `--s-grid-1-direction` - `--s-grid-4-direction` for direction of an flexible items using `flex-direction` property

## Demo

[All demos][webcomponents-demo]

<!--
```
<custom-element-demo>
  <template>
    <script src="../webcomponentsjs/webcomponents-lite.js"></script>
    <link rel="import" href="../iron-flex-layout/iron-flex-layout.html">
    <link rel="import" href="../paper-styles/color.html">
    <link rel="import" href="s-grid-style.html">
    <link rel="import" href="s-grid-1-style.html">
    <link rel="import" href="s-grid-2-style.html">
    <next-code-block></next-code-block>
  </template>
</custom-element-demo>
```
-->
```html
<style include="s-grid-style s-grid-1-style s-grid-2-style">

:host {
  display: block;
  font-size: 20px;
  font-family: 'Roboto', 'Noto', sans-serif;

  --s-grid-1-expandible-item-items: 2;
  --s-grid-1-item-height: 25%;
  --s-grid-2-item-height: 25%;
}

li.item:nth-child(1),
li.item:nth-child(3) .item:nth-child(2) {
  background-color: var(--paper-blue-500);
  color: #fff;
}

li.item:nth-child(2),
li.item:nth-child(3) {
  background-color: transparent;

  height: 50%;
}

li.item:nth-child(4) {
  background-color: var(--paper-green-500);
  color: #fff;
}

li.item .item:nth-child(1) {
  background-color: var(--paper-red-500);
  color: #fff;
}

li.item .item:nth-child(2) {
  background-color: var(--paper-yellow-500);
}

ul {
  padding: 0;
  list-style: none;
}

.item {
  @apply(--layout);
  @apply(--layout-center-center);

  list-style: none;
  background-color: #fff;
  color: #000;
}

.item--expandible {
  @apply(--s-grid-1-expandible-item);
}

/* Tablet wide */
@media screen and (min-width: 600px) {
  :host {
    --s-grid-1-gutter: 16px;
    --s-grid-1-items: 2;
    --s-grid-1-item-height: 50%;
    --s-grid-2-item-height: calc((var(--s-grid-1-item-height) - var(--s-grid-1-gutter)) / 2);
  }

  li.item .item:nth-child(1) {
    margin-bottom: var(--s-grid-1-gutter);
  }
}

</style>

<ul class="s-grid s-grid-1">
  <li class="item">1</li>
  <li class="item s-grid s-grid-2">
    <div class="item">2</div>
    <div class="item">3</div>
  </li>
  <li class="item s-grid s-grid-2">
    <div class="item">4</div>
    <div class="item">5</div>
  </li>
  <li class="item">6</li>
  <template is="dom-repeat" items="[7, 8, 9, 10, 11, 12]">
    <li class="item item--expandible">[[item]]</li>
  </template>
</ul>
```

## Examples

Import `s-grid-style.html`, `s-grid-1-style.html` and include `s-grid-style`, `s-grid-1-style` in the style of an element's definition.
Then, add the class `s-grid`, `s-grid-1` to a container such as `ul` or `div`:

```html
<template>
  <style include="s-grid-style s-grid-1-style">

    :host {
      --s-grid-1-items: 3;
      --s-grid-1-item-height: 100px;
    }

    ul {
      padding: 0;
      list-style: none;
    }

    .item {
      background-color: white;
    }

    @media (max-width: 640px) {
      :host {
        --s-grid-1-items: 1;
      }
    }

  </style>
  <ul class="s-grid s-grid-1">
    <li class="item">1</li>
    <li class="item">2</li>
    <li class="item">3</li>
  </ul>
</template>
```

In this example, the grid  will take 3 columns per row and only 1 column if the viewport width is
smaller than 640px.

### Expandible items

In many cases, it's useful to expand an item more than 1 column. To achieve this type of layout,
you can specify the number of columns the item should expand to by setting the custom property
`--s-grid-1-expandible-item-items`. To indicate which item should expand, apply the mixin
`--s-grid-1-expandible-item` to a rule with a selector to the item. For example:

```html
<template>
  <style include="s-grid-style s-grid-1-style">
    :host {
      --s-grid-1-items: 3;
      --s-grid-1-item-height: 100px;
      --s-grid-1-expandible-item-items: 3;
    }

    ul {
      padding: 0;
      list-style: none;
    }

    /* Only the first item should expand */
    .item:first-child {
      @apply(--s-grid-1-expandible-item);
    }
  </style>
</template>
```

### Preserving the aspect ratio

When the size of a grid item should preserve the aspect ratio, you can add the `has-aspect-ratio`
attribute to the element with the class `s-grid`. Now, every item element becomes a wrapper around
the item content. For example:

```html
<template>
  <style include="s-grid-style s-grid-1-style">

    :host {
      --s-grid-1-items: 3;
      /* 50% the width of the item is equivalent to 2:1 aspect ratio*/
      --s-grid-1-item-height: 50%;
    }

    ul {
      padding: 0;
      list-style: none;
    }

    .item {
      background-color: white;
    }

  </style>
  <ul class="s-grid s-grid-1" has-aspect-ratio>
    <li class="item">
      <div>item 1</div>
    </li>
    <li class="item">
      <div>item 2</div>
    </li>
    <li class="item">
      <div>item 3</div>
    </li>
  </ul>
</template>
```

### Styling

Custom property                                             | Description                                                | Default
------------------------------------------------------------|------------------------------------------------------------|------------------
`--s-grid-1-direction` - `--s-grid-4-direction`             | Direction of an flexible items.                            | row
`--s-grid-1-gutter` - `--s-grid-4-gutter`                   | The space between two items.                               | 0px
`--s-grid-1-items` - `--s-grid-4-items`                     | The number of items per row or column.                     | 1
`--s-grid-1-item-height` - `--s-grid-4-item-height`         | The height of the items.                                   | auto
`--s-grid-1-expandible-item-items` - `--s-grid-4-expandible-item-items` | The number of items an expandible item should expand to. | 1
`--s-grid-1-total-right-gutter` - `--s-grid-4-total-right-gutter`       | Total right gutter(margin) of items. | var(--s-grid-1-gutter) * var(--s-grid-1-items)

## Installation

`bower i s-grid -S`

## License

MIT: [StartPolymer/license](https://github.com/StartPolymer/license)


[webcomponents-image]: https://img.shields.io/badge/webcomponents.org-published-blue.svg
[webcomponents-url]: https://webcomponents.org/element/StartPolymer/s-grid
[webcomponents-demo]: https://webcomponents.org/element/StartPolymer/s-grid/demo/demo/index.html
