# brush
emmit evenly spaced brush stroke event

```javascript
/**
You can sketch on screen by dragging.
If you drawing on wacom tablet then line size is controlled by tablet pressure.
*/

// initialization
var croquis = new Croquis();
croquis.setCanvasSize(400, 300);
croquis.addLayer();
croquis.fillLayer('#abc');

var brush=new Croquis.Brush(function(x, y){ // the callback function we need
	console.log(x, y)
});
brush.setSpacing(1);
brush.setColor('rgba(0,0,0,.3)')
croquis.setTool(brush);

// croquis dom element
// document.body.appendChild(croquis.getDOMElement()); // we don't need the canvas any more

// mouse event
document.addEventListener('mousedown', function (e) {
    croquis.down(e.clientX, e.clientY);
    document.addEventListener('mousemove', onMouseMove);
    document.addEventListener('mouseup', onMouseUp);
});
function onMouseMove(e) {
    croquis.move(e.clientX, e.clientY);
}
function onMouseUp(e) {
    croquis.up(e.clientX, e.clientY);
    document.removeEventListener('mousemove', onMouseMove);
    document.removeEventListener('mouseup', onMouseUp);
}
```

based on https://github.com/disjukr/croquis.js , croquis.js closely bind with canvas2d, but I want to use brush in webgl, so I extracted and modified it.
