# barcode.php

### Generate barcodes from a single PHP file. MIT license.

  * Output to PNG, GIF, JPEG, or SVG.
  * Generates UPC-A, UPC-E, EAN-13, EAN-8, Code 39, Code 93, Code 128, Codabar, ITF, QR Code, and Data Matrix.

Use from a PHP script:

```
include 'barcode.php';

$generator = new barcode_generator();

/* Output directly to standard output. */
$generator->output_image($format, $symbology, $data, $options);

/* Create bitmap image. */
$image = $generator->render_image($symbology, $data, $options);
imagepng($image);
imagedestroy($image);

/* Generate SVG markup. */
$svg = $generator->render_svg($symbology, $data, $options);
echo $svg;
```

Use with GET or POST:

```
barcode.php?f={format}&s={symbology}&d={data}&{options}
```

e.g.

```
barcode.php?f=png&s=upc-e&d=06543217
barcode.php?f=svg&s=qr&d=HELLO%20WORLD&sf=8&ms=r&md=0.8
```

#### Options:

`f` - Format. One of:
```
    png
    gif
    jpeg
    svg
```

`s` - Symbology (type of barcode). One of:
```
    upc-a          code-39         qr     dmtx
    upc-e          code-39-ascii   qr-l   dmtx-s
    ean-8          code-93         qr-m   dmtx-r
    ean-13         code-93-ascii   qr-q   gs1-dmtx
    ean-13-pad     code-128        qr-h   gs1-dmtx-s
    ean-13-nopad   codabar                gs1-dmtx-r
    ean-128        itf
```

`d` - Data. For UPC or EAN, use `*` for missing digit. For Codabar, use `ABCD` or `ENT*` for start and stop characters. For QR, encode in Shift-JIS for kanji mode.

`w` - Width of image. Overrides `sf` or `sx`.

`h` - Height of image. Overrides `sf` or `sy`.

`sf` - Scale factor. Default is 1 for linear barcodes or 4 for matrix barcodes.

`sx` - Horizontal scale factor. Overrides `sf`.

`sy` - Vertical scale factor. Overrides `sf`.

`p` - Padding. Default is 10 for linear barcodes or 0 for matrix barcodes.

`pv` - Top and bottom padding. Default is value of `p`.

`ph` - Left and right padding. Default is value of `p`.

`pt` - Top padding. Default is value of `pv`.

`pl` - Left padding. Default is value of `ph`.

`pr` - Right padding. Default is value of `ph`.

`pb` - Bottom padding. Default is value of `pv`.

`bc` - Background color in `#RRGGBB` format.

`cs` - Color of spaces in `#RRGGBB` format.

`cm` - Color of modules in `#RRGGBB` format.

`tc` - Text color in `#RRGGBB` format. Applies to linear barcodes only.

`tf` - Text font for SVG output. Default is monospace. Applies to linear barcodes only.

`ts` - Text size. For SVG output, this is in points and the default is 10. For PNG, GIF, or JPEG output, this is the GD library built-in font number from 1 to 5 and the default is 1. Applies to linear barcodes only.

`th` - Distance from text baseline to bottom of modules. Default is 10. Applies to linear barcodes only.

`ms` - Module shape. One of: `s` for square, `r` for round, or `x` for X-shaped. Default is `s`. Applies to matrix barcodes only.

`md` - Module density. A number between 0 and 1. Default is 1. Applies to matrix barcodes only.

`wq` - Width of quiet area units. Default is 1. Use 0 to suppress quiet area.

`wm` - Width of narrow modules and spaces. Default is 1.

`ww` - Width of wide modules and spaces. Applies to Code 39, Codabar, and ITF only. Default is 3.

`wn` - Width of narrow space between characters. Applies to Code 39 and Codabar only. Default is 1.
