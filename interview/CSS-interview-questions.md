#### 1. What is CSS and why is it used?
CSS (Cascading Style Sheets) is used to style HTML elements — controlling layout, colors, fonts, spacing, and responsiveness. It separates content (HTML) from presentation, improving maintainability.

#### 2. Types of CSS?
Inline CSS – inside the HTML element (style attribute).

Internal CSS – inside <style> tag in the HTML <head>.

External CSS – in a .css file linked via <link>.

#### 3.Difference between relative, absolute, fixed, and sticky positioning?

Relative – positioned relative to its original position.

Absolute – positioned relative to the nearest positioned ancestor (non-static).

Fixed – positioned relative to the viewport; doesn’t move on scroll.

Sticky – toggles between relative and fixed based on scroll position.

#### 4. Difference between em, rem, px, %?
px – fixed pixels, not scalable.

em – relative to the font-size of the parent.

rem – relative to the root (html) font-size.

% – relative to the parent’s dimension.

#### 5.Difference between inline and block-level elements?

Inline – takes only as much width as content, doesn’t start a new line (span, a).

Block – takes full width and starts on a new line (div, p).

#### 6. What are pseudo-classes? Give examples.
 Pseudo-classes define a special state of an element.

Example:
a:hover { color: red; } /* when mouse hovers */
p:first-child { font-weight: bold; }

#### 7.What are pseudo-elements? Give examples.
Pseudo-elements style specific parts of an element.

Example:
p::first-line { font-size: 18px; }
p::before { content: "Note: "; color: red; }

#### 8. Explain the CSS box model.
Every element is a box with:
Content → Padding → Border → Margin.
box-sizing: content-box (default) calculates width without border/padding; border-box includes them.

#### 9.Difference between float and flexbox?

1. Float
Purpose:
Originally designed to wrap text around images (like in newspapers), not for complex layouts.
People started using it for layouts before Flexbox existed, but it can be tricky to manage.

2. Flexbox
Purpose:
Designed for modern responsive layouts, making alignment and distribution of space easy in both rows and columns.

How it works:
Works on a parent-child relationship: the parent becomes a flex container, and its children become flex items.

You can easily align items horizontally and vertically.

No need for clearfix hacks.

#### 10. Difference between grid and flexbox?

Flexbox : 1-dimensional layout (either row or column at a time).

*Works on a single axis at a time (main axis or cross axis).
*Great for aligning items in a row or in a column.
*Good for smaller components or distributing space dynamically.

Grid → 2-dimensional layout (rows and columns at the same time).

*Works on both rows and columns simultaneously.
*Lets you define explicit rows and columns with precise control.
*Best for entire page layouts or complex grids.

#### 11.How does z-index work? give with example?

What is z-index?
z-index controls the stacking order of elements along the Z-axis (imagine layers stacked toward/away from you).

Higher z-index → element appears on top of lower ones.
Only works on elements with a position other than static (relative, absolute, fixed, sticky).

How it Works

Elements are placed in layers based on HTML order by default (later elements appear on top if overlapping).

z-index lets you manually control which layer is on top.

If two elements have the same z-index, the one later in HTML appears on top.

Stacking contexts matter — an element's z-index is only compared to others in the same stacking context.

#### 12.What are media queries?
Media queries are a CSS feature that let you apply styles based on the device’s characteristics, such as screen size, resolution, or orientation.

They are the foundation of responsive web design — helping your layout adapt to mobile, tablet, and desktop screens.

Basic Syntax

@media (condition) {
  /* CSS rules here apply only if the condition is true */
}

Why Use Media Queries?

Make websites mobile-friendly.

Optimize user experience for different devices.

Avoid maintaining separate mobile/desktop sites.


#### 13. Difference between min-width and max-width?
min-width – applies styles when width is greater than or equal to value.

max-width – applies styles when width is less than or equal to value.

Here’s the clear difference between min-width and max-width in media queries — these two often confuse people because they flip depending on whether you’re doing mobile-first or desktop-first design.

1. min-width
The CSS inside runs when the screen is at least this wide.

Often used in mobile-first design:
→ You write default styles for mobile (small screens),
→ Then use min-width to apply new styles for larger devices.

2. max-width
The CSS inside runs when the screen is at most this wide.

Often used in desktop-first design:
→ You write default styles for desktop (large screens),
→ Then use max-width to apply styles for smaller devices.

#### 14. Difference between opacity and visibility: hidden?

*opacity: 0 – element invisible but still takes space.

*visibility: hidden – invisible but still takes space.

*display: none – removes from layout.


1. opacity
Controls the transparency of an element.

opacity: 0 → the element is fully transparent but still takes up space and is clickable (unless pointer-events: none is also used).

Values range from 0 (fully transparent) to 1 (fully visible).

2. visibility: hidden
Hides the element visually and makes it non-interactive.

The element still takes up space in the layout.

The opposite is visibility: visible.

#### 15. Difference between @import and <link>?

import – loads CSS after HTML is loaded (slower).

<link> – loads CSS during HTML parsing (faster).





