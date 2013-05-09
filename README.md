Quick-start
===========

For simple scenarios, you can use the ```pxxl()``` function. It takes care of downloading the font file via ajax, it parses the font and then it 'renders' the text to a 'pixel info' array. 

    pxxl(<font-url>, <text>, <callback>)

* ```<font-url>```
  - A url used to retrieve a font file via XHR. The font should be in the BDF format, which is an old text-based format for bitmap fonts.
  

* ```<text>```
  - The text you would like you render.
    

* ```<callback>``` (signature: ```(function(pixels) {} )```)
  - The callback is where the rendering should happen. It is called after the font has loaded and has been parsed. The ```pixels``` argument that gets passed is an array of pixels, like this:
  
		[{ x: 0, y : 0 },
		 { x: 1, y : 0 },
		 { x: 2, y : 1 },
		 { x: 3, y : 1 }
		 ..etc..        ]

You can use the pixel info any way you like. You can:

  - plot them to a canvas
  - create a absolutely positioned divs for every pixel or
  - use WebGL
  - use 3D CSS
  - etc

## Example

    pxxl("fonts/c64d.bdf", "Pxxl.js", function (pixels) {
      var ctx = $('canvas')[0].getContext('2d');

      for (var p=0,hue=0 ; p<pixels.length ; p++,hue++) {
        var pixel = pixels[p],
          x = pixel.x*6,
          y = pixel.y*6;

        ctx.fillStyle = "hsl("+ hue +",100%,50%)";
        ctx.fillRect(x,y,5,5);
      }
    });

API
===

# Pxxl.LoadFont()
```Pxxl.LoadFont(<url>, <callback>)```

Load and parse a font file and executed the callback afterwards.

		Pxxl.LoadFont(fontUrl, function(font) {
			...
		});
The ```font``` param that is received by the callback is an instance of ```Pxxl.Font```.

# Pxxl.Font.getPixels()
```Pxxl.Font.getPixels()```

Gets the pixel info based on given font and text. The pixel info reflects how the text would be rendered. You can use the pixel info to do your own rendering.

		var pixels = font.getPixels(text);

The array looks like this:
  
		[{ x: 0, y : 0 },
		 { x: 1, y : 0 },
		 { x: 2, y : 1 },
		 { x: 3, y : 1 }
		 ..etc..        ]
		 

