# CSS Basics Visual Cheatsheet

> Every concept from folders 01–13 - syntax + explanation at a glance.

---

## 01 - Selectors

### Universal Selector `*`

It works for the entire document, selecting all elements. It is represented by an asterisk (`*`). When you use the universal selector, it applies the specified styles to every element on the page, unless there are more specific selectors that override those styles.

```css
* {
    color: rgb(10, 119, 192);
    background-color: rgb(255, 253, 249);
}
```

---

### Element Selector

Targets specific HTML elements by their tag name. The styles apply to all instances of that element in the document, unless more specific selectors override them.

> CSS properties are applied in order of **specificity**. The more specific a selector is, the higher priority it has. The `h1` selector is more specific than `*`, so its styles take precedence for `h1` elements.

```css
h1 {
    color: rgb(42, 42, 42);
}

button {
    background-color: rgb(10, 119, 192);
    color: rgb(255, 255, 255);
}
```

---

### ID Selector `#id`

Targets a specific element based on its unique ID attribute. Represented by `#` followed by the ID name. Overrides any styles from less specific selectors.

> The ID selector takes precedence over both the universal selector and the element selector because it is more specific than both.

```css
#innerHeading {
    color: rgb(255, 255, 255);
}
```

---

### Class Selector `.class`

Targets elements based on their class attribute. Represented by `.` followed by the class name. Can be reused on many elements (unlike ID).

> In general we don't give the same ID to multiple elements, but we **can** give the same class to multiple elements.  
> If the element selector already sets `color`, the class `color` will not show - but `background-color` will show if the element selector doesn't define one.

```css
.paragraph {
    color: rgb(61, 69, 64);
}

.myClass {
    background-color: rgb(10, 119, 192);
    color: rgb(255, 168, 168);
}
```

---

### Specificity Order (low → high)

| Selector | Specificity |
|---|---|
| `*` | 0-0-0 |
| element | 0-0-1 |
| `.class` | 0-1-0 |
| `#id` | 1-0-0 |
| inline style | highest |

---

## 03 - Text Properties

### text-align

It works according to the parent element - if we apply `text-align` to a div, all text inside that div will be aligned accordingly. In CSS3 we have two new values: `start` (aligns left in LTR) and `end` (aligns right in LTR).

```css
#left   { text-align: left;   }
#center { text-align: center; }
#right  { text-align: right;  }
#start  { text-align: start;  } /* CSS3 */
#end    { text-align: end;    } /* CSS3 */
```

---

### text-decoration

We can combine multiple values at the same time and also specify the color. A specific use case: to remove the underline from links, use `text-decoration: none`.

```css
#underline   { text-decoration: underline;              }
#overline    { text-decoration: overline;               }
#linethrough { text-decoration: line-through;           }

/* combine multiple values + color */
#combined    { text-decoration: underline overline red; }

/* remove underline from links */
#link        { text-decoration: none;                   }
```

---

### font-weight

We can also specify the font weight using numbers, where 400 is normal and 700 is bold. We can use any number between 100 and 900, where 100 is the lightest and 900 is the boldest.

```css
#normal   { font-weight: normal;  } /* 400 */
#bold     { font-weight: bold;    } /* 700 */
#bolder   { font-weight: bolder;  }
#lighter  { font-weight: lighter; }
#numeric  { font-weight: 600;     } /* any value 100–900 */
```

---

### font-family

We can specify a specific font family (e.g. Arial, Helvetica) or use multiple families as a **fallback mechanism** in case the first one is not available on the user's system.

We can use `@font-face` to define a custom font - we need to specify the font-family name and the source of the font file, and optionally the font weight and style.

```css
/* generic families */
#serif      { font-family: serif;      }
#sans-serif { font-family: sans-serif; }
#monospace  { font-family: monospace;  }

/* specific font + fallback chain */
#specific-font {
    font-family: Arial, Helvetica, sans-serif;
}

/* custom font via @font-face */
@font-face {
    font-family: "Softique Demo Bold";
    src: url("SoftiqueDemo-Bold.otf") format("opentype");
    font-weight: normal;
    font-style: normal;
}

#custom-font {
    font-family: "Softique Demo Bold", Arial, sans-serif;
}
```

---

## 04 - Units, Line-Heights & Text-Transforms

### Units - `px` (Absolute)

Pixels (`px`) represent a **fixed size** on the screen. 1px is equal to one dot on the screen. It does **not** scale with the user's settings or the viewport size. Default font size in most browsers is **16px**.

```css
#px { font-size: 16px; }
```

---

### Units - `em`, `rem`, `%` (Relative)

- **em** - Relative to the font size of the **parent element**. If the parent has font-size 16px, then 1em = 16px. When the parent's font size changes, 1em changes accordingly.
- **rem** - Relative to the font size of the **root element** (`html`). If the root has font-size 16px, then 1rem = 16px. Stays consistent regardless of nesting level.
- **%** - Relative to the font size of the **parent element**. If the parent has font-size 16px, then 100% = 16px. Like em, it scales with the parent.

```css
#em      { font-size: 1em;   }
#rem     { font-size: 1rem;  }
#percent { font-size: 100%;  }
```

---

### line-height

The `line-height` property controls the amount of space between lines of text. It can be set using various units (px, em, rem, %).

A common practice is to use a **unitless value** which acts as a multiplier of the font size - e.g. `line-height: 1.5` means 1.5 �- the font size.

```css
#lh-normal     { line-height: normal; }
#lh-number     { line-height: 1.5;    } /* unitless multiplier - most common */
#lh-length     { line-height: 24px;   }
#lh-percentage { line-height: 150%;   }
```

---

### text-transform

The `text-transform` property controls the capitalization of text:

- `uppercase` - Transforms all characters to uppercase.
- `lowercase` - Transforms all characters to lowercase.
- `capitalize` - Transforms the first character of each word to uppercase.
- `none` - No transformation applied.

```css
#uppercase  { text-transform: uppercase;  }
#lowercase  { text-transform: lowercase;  }
#capitalize { text-transform: capitalize; }
#none       { text-transform: none;       }
```

---

## 06 - Box Model (Height, Width, Border, Padding & Margin)

The content is made up of four parts:
- **Content** - where text and images are displayed (innermost)
- **Padding** - space between the content and the border
- **Border** - the line that surrounds the padding
- **Margin** - space outside the border, separating the element from other elements

```
      MARGIN (outer space)
    ┌─────────────────────┐
    │   BORDER (outline)  │
    │  ┌───────────────┐  │
    │  │ PADDING (gap) │  │
    │  │  ┌─────────┐  │  │
    │  │  │ CONTENT │  │  │
    │  │  └─────────┘  │  │
    │  └───────────────┘  │
    └─────────────────────┘
```

---

### Width, Height & Border

```css
/* Width and height - using background-color lets us see the dimensions */
.box-modelDiv {
    width: 400px;
    height: 200px;
    background-color: rgb(255, 201, 201);

    /* border shorthand - border: width style color */
    border: 2px dotted rgb(136, 17, 17);
}

/* border full syntax (three separate properties) */
h1 {
    border-width: 2px;
    border-color: rgb(54, 70, 7);
    border-style: solid;
}
```

---

### border-radius

Used to create rounded corners. The value can be in pixels or percentage. If the value is **50%** it will create a **circle** if the width and height are equal.

```css
#div-a { border-radius: 10px; }  /* slightly rounded */
#div-b { border-radius: 25px; }  /* more rounded     */
#div-c { border-radius: 50%;  }  /* circle (w == h)  */
```

---

### Padding

Padding is the space between the content and the border. Can be set for each side individually or with shorthand.

```css
/* individual sides */
padding-top: 40px;
padding-right: 40px;
padding-bottom: 40px;
padding-left: 40px;

/* shorthand - single value sets all four sides */
padding: 40px;

/* shorthand - four values: top right bottom left */
padding: 40px 40px 40px 40px;
```

---

### Margin

Margin is the space outside the border that separates the element from other elements. Same shorthand rules as padding.

```css
/* individual sides */
margin-top: 20px;
margin-right: 20px;
margin-bottom: 20px;
margin-left: 20px;

/* shorthand - single value sets all four sides */
margin: 20px;

/* shorthand - four values: top right bottom left */
margin: 20px 20px 20px 20px;
```

---

## 08 - Display, Visibility & Alpha Channel

### Block vs Inline

- **Block elements** take up the full width available and start on a new line. Examples: `<div>`, `<h1>`, `<p>`.
- **Inline elements** only take up as much width as necessary and do not start on a new line. Examples: `<span>`, `<a>`, `<strong>`.

We can **change the display property** of an element to modify its behavior.

```css
/* block element changed to inline */
#blockChange { display: inline; }

/* inline element changed to block */
#inlineChange { display: block; }
```

---

### display: inline-block

Inline elements do not start on a new line, and their **vertical** margins and padding do not affect the layout. To solve this, use `display: inline-block` - similar to inline elements, but **with block-level properties like Margin and Padding**.

```css
.divEdit1 {
    display: inline;
    /* vertical margin/padding ignored */
}

.divEdit2 {
    display: inline-block;
    /* respects width, height, margin, padding */
}
```

---

### display: none vs visibility: hidden

- **`display: none`** - the element is completely removed from the document flow and is not visible.
- **`visibility: hidden`** - the element is hidden but **still takes up space** in the layout.

```css
#box2      { display: none;      } /* removed from flow, no space */
#box2again { visibility: hidden; } /* invisible but space reserved */
```

---

### Alpha Channel - rgba()

The alpha channel represents **transparency** in RGBA color values. The alpha value ranges from **0** (completely transparent) to **1** (completely opaque).

```css
#alpha1 { background-color: rgba(255, 0, 0, 0.25); } /* 25% opaque */
#alpha2 { background-color: rgba(255, 0, 0, 0.50); } /* 50% opaque */
#alpha3 { background-color: rgba(255, 0, 0, 0.75); } /* 75% opaque */
/* alpha = 1 is fully opaque */
```

---

## 10 - Relative Units

### `%` - Percentage of the parent element's dimension

```css
#box1 { width: 200px; }   /* parent */
#box2 {
    width: 50%;   /* 50% of parent's width  */
    height: 50%;  /* 50% of parent's height */
}
```

---

### `em` - Relative to the parent element's font-size

em units represent the font size of the element. If the parent font-size is 16px, then 1em = 16px. So 2em = 2 �- 16px = 32px.

```css
#box3 { font-size: 16px; }  /* parent */
#box4 {
    font-size: 2em;
    /* 2 �- 16px = 32px */
}
```

---

### `rem` - Root em (relative to the `html` tag)

Root em means the font size of the root element (the `html` tag). This is consistent regardless of nesting level.

```css
html  { font-size: 16px; }
#box5 {
    font-size: 1rem;
    /* 1rem = 16px (the html font-size) */
}
```

---

### `vw` / `vh` - Viewport Width & Height

`vh` means a percentage of the **viewport height** (the browser window height). `vw` means a percentage of the **viewport width**.

```css
#box6 {
    width: 50vw;   /* 50% of the viewport width  */
    height: 50vh;  /* 50% of the viewport height */
}
```

---

## 11 - Position & Z-Index

### position: static (default)

Static positioning means the element follows normal document flow. We **can't change its position** - `top`, `left`, `right`, `bottom`, and `z-index` all have **no effect**.

```css
#box1 {
    position: static;
    top: 20px;   /* no effect */
    left: 20px;  /* no effect */
}
```

---

### position: relative

The element is positioned **relative to its normal position**. We can offset it using `top`, `left`, `right`, `bottom`. But it **still takes up the same space** in the document flow as if it were static.

```css
#box2 {
    position: relative;
    top: 20px;   /* shifted down 20px from its normal position  */
    left: 20px;  /* shifted right 20px from its normal position */
}
```

---

### position: absolute

The element is positioned relative to its **nearest positioned ancestor** (one with position other than static). If none exists, it is positioned relative to the viewport. It is **removed from the normal document flow** - does not take up space.

```css
#box3 {
    position: absolute;
    top: 250px;
    left: 200px;
}
```

---

### position: fixed

The element is positioned relative to the **viewport (the browser window)**. It is removed from the document flow and stays fixed while the page scrolls. Commonly used for sticky headers or footer bars.

```css
/* sticky footer */
#box4 {
    position: fixed;
    height: 50px;
    width: 100%;
    bottom: 0px;
    left: 0px;
}

/* sticky header */
#fixedbox {
    position: fixed;
    height: 50px;
    width: 100%;
    top: 0px;
}
```

---

### position: sticky

The element is positioned relative to the viewport **once it reaches a certain scroll position**. Before that it behaves like a relative element.

```css
#box5 {
    position: sticky;
    top: 0;
    left: 50%;
}
```

---

### z-index - Stacking Order

If a div overlaps with another div, `z-index` determines which one appears on top. By default, elements are stacked in HTML order, with **later elements appearing on top**.

> `z-index` **only works on elements with a position value other than static** (relative, absolute, fixed, or sticky).  
> If two elements have the same z-index value, the one that appears later in the HTML will be on top.

```css
#box1 {
    position: absolute;
    z-index: 1;  /* behind box2 */
}
#box2 {
    position: absolute;
    z-index: 2;  /* in front of box1 */
}
#box3 {
    position: absolute;
    z-index: 3;  /* in front of both box1 and box2 */
}
```

---

## 12 - Background Image & Size

```css
/* cover - scales image to cover the entire container, may crop */
#box1 {
    background-image: url('image.jpg');
    background-size: cover;
}

/* contain - scales to fit fully inside, may leave empty space (tiles by default) */
#box2 {
    background-image: url('image.jpg');
    background-size: contain;
}

/* contain + no-repeat - fits inside and does not tile */
#box3 {
    background-image: url('image.jpg');
    background-size: contain;
    background-repeat: no-repeat;
}

/* auto - image displays at its natural dimensions, tiles if smaller */
#box4 {
    background-image: url('image.jpg');
    background-size: auto;
}
```

---

## 14 - Flexbox: Container Properties

### display: flex

To use flexbox on a container, set `display: flex`. Only then can we use flexbox properties.

```css
.container {
    display: flex;
}
```

---

### flex-direction

In flex direction the content div size will auto adjust according to the inner content size.

```css
/* row - items in a row from left to right (default) */
#container1 { flex-direction: row;            }

/* row-reverse - items in a row from right to left */
#container2 { flex-direction: row-reverse;    }

/* column - items in a column from top to bottom */
#container3 { flex-direction: column;         }

/* column-reverse - items in a column from bottom to top */
#container4 { flex-direction: column-reverse; }
```

---

### justify-content

1. **flex-start** - items placed at the start of the container (default).
2. **flex-end** - items placed at the end of the container.
3. **center** - items placed at the center of the container.
4. **space-around** - equal space around items. The first/last items have half the space that exists between items.
5. **space-between** - equal space between items. First item at start, last item at end.
6. **space-evenly** - equal space between all items including edges.

```css
#container11 { flex-direction: row; justify-content: flex-start;  }
#container21 { flex-direction: row; justify-content: flex-end;    }
#container31 { flex-direction: row; justify-content: center;      }
#container41 { flex-direction: row; justify-content: space-around; }
#container51 { flex-direction: row; justify-content: space-between;}
#container61 { flex-direction: row; justify-content: space-evenly; }
```

---

### flex-wrap

```css
/* nowrap - boxes will not wrap, auto-adjusts their size (default) */
#container12 { flex-wrap: nowrap;       }

/* wrap - boxes wrap to the next line if they don't fit */
#container22 { flex-wrap: wrap;         }

/* wrap-reverse - boxes wrap to the next line in reverse order */
#container32 { flex-wrap: wrap-reverse; }

/* flex-flow - shorthand for flex-direction + flex-wrap */
#container13 { flex-flow: row wrap;     }
```

---

### align-items

Align Items is always by default **stretch** - items stretch to fill the container along the cross axis. Works per-line when wrapping.

```css
/* stretch - items fill cross axis (default). Gap visible between lines */
#container14 { flex-wrap: wrap; align-items: stretch;    }

/* flex-start - not stretch, starts from the top of each line */
#container24 { flex-wrap: wrap; align-items: flex-start; }

/* center - not stretch, centered vertically in each line */
#container34 { flex-wrap: wrap; align-items: center;     }

/* flex-end - not stretch, ends at the bottom of each line */
#container44 { flex-wrap: wrap; align-items: flex-end;   }
```

---

### align-content

Align Content means items are now not working as different items for each line - they are treated as **the same content for the whole container** (only has effect with `flex-wrap`).

```css
/* stretch - fills the container along the cross axis (default) */
#container15 { flex-wrap: wrap; align-content: stretch;       }

/* flex-start - packed to the top of the container */
#container25 { flex-wrap: wrap; align-content: flex-start;    }

/* center - centered vertically in the container */
#container35 { flex-wrap: wrap; align-content: center;        }

/* flex-end - packed to the bottom of the container */
#container45 { flex-wrap: wrap; align-content: flex-end;      }

/* space-around - equal space around each row/line */
#container55 { flex-wrap: wrap; align-content: space-around;  }

/* space-between - equal space between rows/lines */
#container65 { flex-wrap: wrap; align-content: space-between; }

/* space-evenly - equal space between rows/lines and edges */
#container75 { flex-wrap: wrap; align-content: space-evenly;  }
```

---

## 14 - Flexbox: Item Properties

### order

The box order follows HTML order by default. Use the `order` property for a custom order:

1. Boxes with no `order` or `order: 0` appear first, in HTML order. Negative values appear before them, sorted lowest to highest.
2. Boxes with positive `order` values appear after, sorted lowest to highest.
3. If two or more boxes have the same `order` value, they appear in HTML order.

```css
#box1 { order: 3;  }
#box2 { order: 1;  }
#box3 { order: 2;  }
#box4 { order: -5; } /* appears first - negative value */
#box5 { order: 0;  }
#box8 { order: 5;  }
#box9 { order: 4;  }
```

---

### flex-grow

Defines how much space a flex item will take up relative to other flex items. If `flex-grow: 1`, the item takes up all available space. If `flex-grow: 0`, it takes no additional space.

```css
.box  { flex-grow: 0; } /* default - no extra space */
.box1 { flex-grow: 1; } /* takes all available space in the container */
```

---

### flex-shrink

Defines how much a flex item will shrink relative to others when there isn't enough space. If `flex-shrink: 1`, the item shrinks proportionally (default). If `flex-shrink: 0`, the item **will not shrink at all** and will overflow if wrap is disabled.

```css
/* default - shrinks proportionally when there isn't enough space */
/* flex-shrink: 1; */

.box2 {
    flex-shrink: 0;
    /* won't shrink - will overflow when there isn't enough space and wrap is disabled */
}
```
