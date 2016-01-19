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

## Scales

“Scales are functions that map from an input domain to an output range.”

- Mike Bostock https://github.com/mbostock/d3/wiki/Quantitative-Scales

Will not correspodn exactly to pixel measurements for use in your visualization. Provides convenient ways to map data values to new values for useful visualization purposes

D3 scales are functions whose parameters are free to define. Once created, you call scale function, pass it a data value, and it returns a nicely scaled output value. Define and use as much as you like kekeke

No direct visual represtation. Only linear scales are covered here

Normalization is the process of mapping a numeric value to a new value between 0 and 1, based on the possible minimum and maximum values. For example, with 365 days in the year, day number 310 maps to about 0.85, or 85% of the way through the year.

Typically, you will call scale functions from within an attr() method or similar, not on their own. Let’s modify our scatterplot visualization to use dynamic scales.

d3 also supports math helpers to loop through arrays, such as min() and max(). top level functions

scales can also be applied independently per axis

### Cool Scale Methods

nice() — This tells the scale to take whatever input domain that you gave to range() and expand both ends to the nearest round value. From the D3 wiki: “For example, for a domain of [0.20147987687960267, 0.996679553296417], the nice domain is [0.2, 1].” This is useful for normal people, who find it hard to read numbers like 0.20147987687960267.

rangeRound() — Use rangeRound() in place of range() and all values output by the scale will be rounded to the nearest whole number. This is useful if you want shapes to have exact pixel values, to avoid the fuzzy edges that may arise with antialiasing.

clamp() — By default, a linear scale can return values outside of the specified range. For example, if given a value outside of its expected input domain, a scale will return a number also outside of the output range. Calling .clamp(true) on a scale, however, forces all output values to be within the specified range. Meaning, excessive values will be rounded to the range’s low or high value (whichever is nearest).

### Other Scales

identity — A 1:1 scale, useful primarily for pixel values
sqrt — A square root scale
pow — A power scale (good for the gym)
log — A logarithmic scale
quantize — A linear scale with discrete values for its output range, for when you want to sort data into “buckets”
quantile — Similar to above, but with discrete values for its input domain (when you already have “buckets”)
ordinal — Ordinal scales use non-quantitative values (like category names) for output; perfect for comparing apples and oranges

# AXES

Axes are functions whose parameters are defined by the grammer. Does not return a value, but generates the visual elements of the axis, including lines, labels, and ticks.

Axis functions are SVG specific, as they generate SVG elements. Aslo, axes are intended for use with quantiative scales (as opposed to ordinal scales).

At minimum, each axis also needs to be told on what scale to operate. the axis takes its scale as the parameter of its scale method. It also has an oreitnation method, where the labels should appear relative to the axis.

Last, axis must be generated and inserted into SVG xAxis function must be called.

call() method takes a selection as input and hands that selection off to any function. Classes can be applied to any group on svg.append

In example, g becomes selection for next link in chain, while call() hands selection off to xAxis, so axis is generated within g.

### TICKS

Ticks were not specified in example, nor intervals. D3 examines xScale and makes "informed judgments." But transforming ticks with ticks() method on axis() can provide overrride.

Tick Labels are provided by entering tickFormat(). Controls number and category formating, e.g. floating point, percentages, both.

One approach - define a new number formatting function, then provide it to axis.tickFormat(formatter). Useful to test in browser.

# TRANSITIONS

