---
layout: page
comments: true
title: "DjVu - Arch Linux"
---

#### Workflow:

1) Scan Tailor Universal - process images

`yay -S scantailor-universal-git`
<br><br>

2) sep.sh - encode DjVu

```
#!/bin/bash

# configuration
DPI=600
OUT_NAME="final.djvu"
TEMP_DIR="tmp"

mkdir -p "$TEMP_DIR"

# loop through layer files
for text_layer in *.tif; do
    # skip .sep.tif files
    [[ "$text_layer" == *.sep.tif ]] && continue
   
    base=$(basename "$text_layer" .tif)
    illus_layer="${base}.sep.tif"
   
    echo "Processing Page: $base"

    # foreground
    # create bitonal mask chunk (Sjbz)
    cjb2 -dpi $DPI "$text_layer" "$TEMP_DIR/$base.fg.djvu"

    # backgroud
    if [ -f "$illus_layer" ]; then
        # convert to PPM
        magick "$illus_layer" "$TEMP_DIR/$base.bg.ppm"
       
        # create temporary photo DjVu
        c44 -dpi $DPI "$TEMP_DIR/$base.bg.ppm" "$TEMP_DIR/$base.bg.djvu"
       
        # extract IW44 chunk
        djvuextract "$TEMP_DIR/$base.bg.djvu" BG44="$TEMP_DIR/$base.bg.chunk"

        # assemble masked page
        djvumake "$TEMP_DIR/$base.combined.djvu" \
            "INFO=,,$DPI" \
            Sjbz="$TEMP_DIR/$base.fg.djvu" \
            BG44="$TEMP_DIR/$base.bg.chunk"
    else
        # no illustrations - just use the text layer
        cp "$TEMP_DIR/$base.fg.djvu" "$TEMP_DIR/$base.combined.djvu"
    fi
done

# bind all pages
echo "Bundling into $OUT_NAME..."
djvm -c "$OUT_NAME" "$TEMP_DIR"/*.combined.djvu

# clean up
rm -rf "$TEMP_DIR"
echo "Done."
```
<br>

3) FineReader 15 - OCR

Wine
<br><br>

4) FR crutch - insert OCR layer

Wine
<br><br>

5) bookmark-djvu - insert contents

`yay -S bookmark-djvu`
<br><br>

6) Document Express Editor 6 - insert cover

Wine
