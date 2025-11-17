# admin-dashboard

Practice of CSS's Grid Layout.

<!-- Personal notes -->
## Terminology:
### "Grid Track" - 
just refers to a row or a column

### "Explicit vs Implicit" tracks - 
grid-auto-rows: 100px; 

Handles the case when more grid items are added inside the grid container despite grid-template-rows only calling for say, 2 rows. 

Any additional grid items will be 100px.

### Gaps
Also known as gutter/alley
column-gap and row-gap are both available.

## Chrome DevTools for grid layouts
https://developer.chrome.com/docs/devtools/css/grid/

## Positioning
If there are 5 columns, there are 6 vertical lines. 
To have 1 cell take up 1 whole row by itself, we can do grid-column-start: 1; grid-column-end: 6;
Or combining them, do grid-column: 1/6
Same concept for rows.
We can also do grid-row-start / grid-column-start / grid-row-end / grid-column-end into one line using grid-area: 1/1/3/6

We can also even write out each cell in every row using grid-area. (very manual)
End up writing lines like 
    "living-room living-room living-room living-room living-room"
    "living-room living-room living-room living-room living-room"
    "bedroom bedroom bathroom kitchen kitchen"
inside the grid container. 

## Advanced - dynamic sizing, functions etc
### repeat()
Make grid container fast with grid-template-rows: repeat(2, 150px); grid-template-columns: repeat(5, 150px);

### Fractional units 
Key to making things dynamic(responsive in some way). px is always static(opposite of dynamic). grid-template-rows: repeat(2, 1fr);
grid-template-columns: repeat(5, 1fr);
grid-template-columns: repeat(2, 2fr) repeat(3, 1fr); Multiple repeat() functions help customise the individual rows/columns.
grid-template-columns: repeat(2, 125px) repeat(3, 1fr); We can also mix units. This means that the first 2 columns will always be 125px while the last 3 columns will take up equal width whatever the size of the screen.

### Viewport concerns
min-content() can ensure that browser will stop shrinking beyond the min-content value. 
Use min() and max() for better control. 
grid-template-rows: repeat(2, min(200px, 50%)); Each row takes up 50% of parent container's height unless viewport gets really big then it stops growing at 200px. min() sets the maximum height 
grid-template-columns: repeat(5, max(120px, 15%)); The smallest the width of a column can get is 120px, when viewport gets really big, it keeps growing and will always take up 15%. max() sets the minimum width here.

minmax() can take static units like minmax(150px, 200px)
clamp(150px, 20%, 200px) can also be used

Use minmax() / clamp() to make sure that images and elements don't overflow their containers(their cells)

If our grid is only 200px wide (say, on a handphone), it makes sense to just have 1 column. On bigger screens, 2 columns ok. Use auto-fit and auto-fill for automatic adjustments.   
.grid-container {
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}
means that at 299px we will still see only 1 column since the minimum is 150px. at 300px, we will see 2 columns that share the same width

(auto-fill, minmax(150px, 1fr)); auto-fill will keep grid items at 150px at large viewports to reserve space for imaginary columns whereas auto-fit will let existing items grow to fill the space

More Grid properties for the grid container and grid items 
https://css-tricks.com/snippets/css/complete-guide-grid/#grid-properties

Flexbox vs Grid:
https://www.theodinproject.com/lessons/node-path-intermediate-html-and-css-using-flexbox-and-grid

"items" are used on the grid container to control all the grid items all at one go 
"self" is used on individual grid items