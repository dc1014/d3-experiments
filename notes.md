# D3 Notes

## Selection

Select an element by Class, ID, or HTML tags
  - or use selectAll for all elements

## Data Binding

D3 maps data to visuals.

As a result, binding data inpurt values to elements in the DOM. Binding is attaching or associating data to specific elements, so that later you can reference those values to apply mapping roles.

selection.data() method is available. Requires
  1. The data
  2. A selection of DOM elements

The data variable of the node can actually be accessed from the browser's console using d3.select(x)

text can instead be given a function whose signature is (d) where d is the data value from the data array. You can do whatever you want with this in func.

## STYLE

.classed("class_name", Boolean) - this allows applying or removing from elements

## SVG

Assumes px dimensions as default. Accepts em, pt, in, cm, and mm.

visual elements in SVG include
  - rect
  - circle
  - ellipse
  - line
  - text
  - path

coordinate system is (0,0) in top left corner. x is horizontal axis, y is vertical axis

Text SVG inherits CSS-specified font styles of its parent element unless specified oetherwise

Any visual element that runs up against SVG will be clipped.

## Styling SVG

Can be applied inline or via css rule

* fill
  - takes color value in name, hex, RGB, RGBA
* stroke
  - takes a color value
* stroke width
  - numeric measurement (usually in px)
  - opacity (0.0 is completely transparent, 1.0 is opaque)
* text
  - font-family
  - font-size

But using CSS to apply SVG can be odd, since SVG props are not CSS props. Consider including SVG in the CSS selectors

### Layer and Drawing

There are no layers or depth
