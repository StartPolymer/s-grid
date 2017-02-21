##&lt;s-grid&gt;

s-grid is a helper class useful for creating responsive, fluid grid layouts using custom properties.
Because custom properties can be defined inside a `@media` rule, you can customize the grid layout
for different responsive breakpoints.

Example:

Import `s-grid-style.html` and include `s-grid-style` in the style of an element's definition.
Then, add the class `s-grid` to a container such as `ul` or `div`:

```html
<template>
  <style include="s-grid-style">

    :host {
      --s-grid-columns: 3;
      --s-grid-item-height: 100px;
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
        --s-grid-columns: 1;
      }
    }

  </style>
  <ul class="s-grid">
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
`--s-grid-expandible-item-columns`. To indicate which item should expand, apply the mixin
`--s-grid-expandible-item` to a rule with a selector to the item. For example:

```html
<template>
  <style include="s-grid-style">
    :host {
      --s-grid-columns: 3;
      --s-grid-item-height: 100px;
      --s-grid-expandible-item-columns: 3;
    }

    ul {
      padding: 0;
      list-style: none;
    }

    /* Only the first item should expand */
    .item:first-child {
      @apply(--s-grid-expandible-item);
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
  <style include="s-grid-style">

    :host {
      --s-grid-columns: 3;
      /* 50% the width of the item is equivalent to 2:1 aspect ratio*/
      --s-grid-item-height: 50%;
    }

    ul {
      padding: 0;
      list-style: none;
    }

    .item {
      background-color: white;
    }

  </style>
  <ul class="s-grid" has-aspect-ratio>
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

Custom property                               | Description                                                | Default
----------------------------------------------|------------------------------------------------------------|------------------
`--s-grid-columns`                          | The number of columns per row.                             | 1
`--s-grid-gutter`                           | The space between two items.                               | 0px
`--s-grid-item-height`                      | The height of the items.                                   | auto
`--s-grid-expandible-item-columns`          | The number of columns an expandible item should expand to. | 1
