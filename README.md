# Custom Vue Tooltip

This is a customizable, reusable Vue.js Tooltip component.
To attach a tooltip to desired element, wrap it like this:

```
<Tooltip>
...
</Tooltip>
```
## Customizaton options

This tooltip offers a few customization options:

### Contents
Set up contents of your tooltip.
```
<Tooltip contents="Desired tooltip contents">
...
</Tooltip>
```
### Position
Set up desired position of your tooltip. If not specified, it will be automatically calculated based on the elements X and Y coordinates.

Possible options:
down, top, left, right, 
rightDown, rightTop, leftDown, leftTop,
topRight, topLeft, downRight, downLeft, 
custom.

If specified as custom, provide another props customPosition, with an array containing two string elements specifying top and left absolute parameters in pixels (example: ['10', '20']).
```
<Tooltip position="down">
...
</Tooltip>


<Tooltip position="custom" customPosition="['10', '20']">
...
</Tooltip>
```

### Color
Specifies the color of the span element.
```
<Tooltip color="#fff">
...
</Tooltip>
```
### Background
```
<Tooltip background="#2f2f2f">
...
</Tooltip>
```
### Border
Specifies border of the tooltip.
```
<Tooltip border="2px solid black">
...
</Tooltip>
```
### Border radius
Specifies border radius of the tooltip.
```
<Tooltip borderRadius="10px">
...
</Tooltip>
```
