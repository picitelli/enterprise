---
title: Rating
description: This page describes Rating.
demo:
  embedded:
  - name: Rating Example
    slug: example-index
  pages:
  - name: Readonly Example
    slug: example-readonly
  - name: Rounding Decimals Up Example
    slug: example-decimals
---

## Code Example

The rating component can be used to either display a rating or allow the end user to select a rating. Half star ratings can be displayed but not set. You can implement the rating control by using the below markup consisting of a block element (a `<div>`) with `class="rating"`, then any number of `<inputs>` followed by `<labels>` for the stars. The `<label>` element should contain an SVG image with the star. An `audible` class should also be added for accessibility. Under the hood, the rating component is actually a set of radio buttons.

Note that the name should be the same for all stars for it to function correctly.

```html
<div class="rating">
  <input type="radio" class="is-filled" name="rating-name" id="one-star-id1"/>
  <label for="one-star-id1">
    <svg class="icon" focusable="false" aria-hidden="true">
      <use xlink:href="#icon-star-filled"/>
    </svg>
    <span class="audible">1 out of 5 Stars</span>
  </label>

  <input type="radio" class="is-filled" name="rating-name" id="two-star-id1"/>
  <label for="two-star-id1">
    <svg class="icon" focusable="false" aria-hidden="true">
      <use xlink:href="#icon-star-filled"/>
    </svg>
    <span class="audible">2 out of 5 Stars</span>
  </label>

  <input type="radio" class="is-filled" name="rating-name" id="three-star-id1"/>
  <label for="three-star-id1">
    <svg class="icon" focusable="false" aria-hidden="true">
      <use xlink:href="#icon-star-filled"/>
    </svg>
    <span class="audible">3 out of 5 Stars</span>
  </label>

  <input type="radio" class="is-half" checked name="rating-name" id="four-star-id1"/>
  <label for="four-star-id1">
    <svg class="icon" focusable="false" aria-hidden="true">
      <use xlink:href="#icon-star-half"/>
    </svg>
    <span class="audible">4 out of 5 Stars</span>
  </label>

  <input type="radio" name="rating-name" id="five-star-id1"/>
  <label for="five-star-id1">
    <svg class="icon" focusable="false" aria-hidden="true">
      <use xlink:href="#icon-star-filled"/>
    </svg>
    <span class="audible">5 out of 5 Stars</span>
  </label>
</div>
```

## Accessibility

`aubible` labels are added for giving the star information.

## Testability

- Please refer to the [Application Testability Checklist](https://design.infor.com/resources/application-testability-checklist) for further details.

## Keyboard Shortcuts

- <kbd>Tab</kbd> will enter the rating group
- <kbd>Down</kbd> or <kbd>Right</kbd> decreases the rating
- <kbd>Up</kbd> or <kbd>Left</kbd> increases the rating
- <kbd>Space</kbd> toggles selected/unselected
- <kbd>Control + Arrow</kbd> moves through the options without updating content or selecting the rating
