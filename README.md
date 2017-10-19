# html2pdf

html2pdf converts any webpage or element into a printable PDF entirely client-side using [html2canvas](https://github.com/niklasvh/html2canvas) and [jsPDF](https://github.com/MrRio/jsPDF).

## Install

1. Copy `html2pdf.js` to your project directory.
2. Fetch the dependencies `html2canvas` and `jsPDF`, which can be found in the above repositories.
3. Include the files in your HTML document , one way is to use require.js

```js
require.config({
        deps: ['main'],
        paths:
        {
            jquery: '../../vendor/jquery/jquery',
            'es6promise':'../../vendor/es6-promise/es6-promise',
            jspdf: '../../vendor/jspdf/jspdf.debug',
            html2canvas_fork:'../../vendor/html2canvas_fork/html2canvas'

         }
      })

```

**Note:** For best results, use require.js to manage your front-end dependencies when using this library.

## Usage

### Basic usage

Including html2pdf exposes the `html2pdf` function. Calling it will create a PDF and prompt the user to save the file:

```js
var element = document.getElementById('element-to-print');
html2pdf(element);
```

The PDF can be configured using an optional `opt` parameter:

```js
Promise = require('es6promise').Promise;

            var element = document.getElementById('case-main');

            html2pdfnew(element, {
               margin: 0.25,
               filename: 'newpdf.pdf',
               image: { type: 'jpeg', quality: 0.98},
               html2canvas: {dpi: 192, letterRendering: true },
               useCanvasElems: true,
               jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait'}
            });


```

The `opt` parameter has the following optional fields:

|Name        |Type            |Default                       |Description                                                                                  |
|------------|----------------|------------------------------|---------------------------------------------------------------------------------------------|
|margin      |number or array |0                             |PDF margin. Array can be either [vMargin, hMargin] or [top, left, bottom, right].            |
|filename    |string          |'file.pdf'                    |The default filename of the exported PDF.                                                    |
|image       |object          |{type: 'jpeg', quality: 0.95} |The image type and quality used to generate the PDF. See the Extra Features section below.   |
|enableLinks |boolean         |true                          |If enabled, PDF hyperlinks are automatically added ontop of all anchor tags.                 |
|useCanvasElems |boolean         |true                          |If enabled, will use multiple Canvas elements in order to be able to convert large html pages to PDF. This is a custom enhancement by driscolldcfpb.                 |
|html2canvas |object          |{ }                           |Configuration options sent directly to `html2canvas` ([see here](https://html2canvas.hertzen.com/documentation.html#available-options) for usage).|
|jsPDF       |object          |{ }                           |Configuration options sent directly to `jsPDF` ([see here](http://rawgit.com/MrRio/jsPDF/master/docs/jsPDF.html) for usage).|

### Extra features

#### Page-breaks

You may add `html2pdf`-specific page-breaks to your document by adding the CSS class `html2pdf__page-break` to any element (normally an empty `div`). During PDF creation, these elements will be given a height calculated to fill the remainder of the PDF page that they are on. Example usage:

```html
<div id="element-to-print">
  <span>I'm on page 1!</span>
  <div class="html2pdf__page-break"></div>
  <span>I'm on page 2!</span>
</div>
```

#### Image type and quality

You may customize the image type and quality exported from the canvas by setting the `image` option. This must be an object with the following fields:

|Name        |Type            |Default                       |Description                                                                                  |
|------------|----------------|------------------------------|---------------------------------------------------------------------------------------------|
|type        |string          |'jpeg'                        |The image type. HTMLCanvasElement only supports 'png', 'jpeg', and 'webp' (on Chrome).       |
|quality     |number          |0.95                          |The image quality, from 0 to 1. This setting is only used for jpeg/webp (not png).           |

These options are limited to the available settings for [HTMLCanvasElement.toDataURL()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL), which ignores quality settings for 'png' images. To enable png image compression, try using the [canvas-png-compression shim](https://github.com/ShyykoSerhiy/canvas-png-compression), which should be an in-place solution to enable png compression via the `quality` option.

## Dependencies

html2pdf depends on the 2 external packages [`html2canvas`](https://github.com/driscolldcfpb/html2canvas) and [`jsPDF`](https://github.com/driscolldcfpb/jsPDF).

## Contributing

### Pull requests

Right now, html2pdf is a single source file located in `/src/`. If you want to create a new feature or bugfix, feel free to fork and submit a pull request!

## Credits
[David Driscoll] (https://github.com/driscolldcfpb

Forked from in order to add enhancement for large html pages to allow them to export to PDF.
[Erik Koopmans](https://github.com/eKoopmans)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2017 >
