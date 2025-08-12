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





