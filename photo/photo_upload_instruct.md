# Photo Upload Instructions

## Export Settings

- **Max dimension:** 800px on longest edge
- **Quality:** 80% JPEG
- **Aspect ratio:** preserved automatically (no cropping or stretching)
- **Original files:** keep backed up on external drive or iCloud — do not rely on the repo copy

## Directory Structure

Photos go in the `./photo/` directory in the repo root. Reference them in `index.html` as `./photo/filename.jpg`.

```
cedrichan.com/
├── index.html
├── photo/
│   ├── beach.jpg
│   ├── halfdome.jpg
│   └── ...
├── cooking/
│   └── dish.jpg
└── writing/
    └── essay.html
```

## Resizing with ImageMagick

### Installation (Windows)
Download installer from imagemagick.org/script/download.php — grab the Q16-HDRI x64 version. During install, check **"Add application directory to your system path"**. Verify with:
```bash
magick --version
```

### Batch resize all JPGs in current directory
Navigate to the photo directory first, then run:
```bash
cd ~/cedrichan.com/photo

for f in *.jpg; do
  magick "$f" -resize "800x800>" -quality 80 "$f"
done
```

Note: quotes around `"800x800>"` are required in Git Bash on Windows — without them the `>` is interpreted as a shell redirect and the command fails.

### What the flags do
- `-resize "800x800>"` — scales image to fit within an 800x800 box, maintaining aspect ratio; the `>` means only shrink, never upscale
- `-quality 80` — 80% JPEG compression, good balance of quality and file size

### Single file
```bash
magick input.jpg -resize "800x800>" -quality 80 output.jpg
```

## Expected Output Sizes
A properly resized photo should be roughly 100–300KB. If a file is still several MB after resizing, check that the command ran correctly.