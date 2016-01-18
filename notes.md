# D3 Notes

SOURCE: http://alignedleft.com/tutorials/d3/an-svg-primer

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

There are no layers or depth. SVG elements will stack, and code deternmines the depth order. First in code, first in render. All subsequent code/render is on top of previous render.

As a consequence, axes and labels should be added last so they appear in front.

## Managing Transparency

Two methods - use RGB color with alpha, or add opacity
  -RGBA accepts 0-255 for RGB, and 0.0 - 1.0 for alpha

With RGBA, transparency is applied to fill and stroke separately. Stroke width is some kind of perimeter calling

With opacity, the setting applies to the entire element. This can be used on elements which have RGBA, and the transparencies are multiplied, i.e. opacity x alpha

Can be specified with any D3 style that accepts color

## Drawing SVGS

All properties of SVG elements are specified as attributes

An ATTRIBUTE is one which has a property/value pairs in an element (oh).

<!-- <element property="value"/> -->
Hmm, that looks strangely like HTML!

<!-- <p class="eureka"> -->

Therefore, it is possible to use append() and attr() in the capacity to generate images

  - best practice to use variables

You can append the SVGs to the body, then define a svg which will be the base, then create those svgs with binded data, to appended to the body

## Data Types

GUESS WHAT - JAVASCRIPT TYPING

GEO JSON

A formalization of existing Javascript object sytax. Can be used in geographical space, or for shapes and spatial features.

var geodata = {
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [ 150.1282427, -24.471803 ]
            },
            "properties": {
                "type": "town"
            }
        }
    ]
};

Listed lon / lat.

## BAR CHARTS YO

D3 has text areas desingated for its data. You can style the text, use padding, etc.

## Scatterplot

What about going into R^2? 2 Tuples in arrays.

