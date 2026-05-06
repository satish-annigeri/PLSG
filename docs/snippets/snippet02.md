# Image Manipulation

[Task 6](../tasks/task20260415.md#task-for-non-structural-engineers) defined two problems, the second of which required the following two tasks to be accomplished:

1. Scale a given image file to a specified positive value.
2. Convert a given image to black & white.

It was suggested to use the [Pillow](https://pillow.readthedocs.io/en/stable/) package for image manipulation. Let us do the following:

1. Install Pillow package from PyPI.
2. Study the documentation to read an image from file, change resolution of an image, convert an image to black & white.
3. Try out the commands from Python REPL.
4. Develop a function to perform the specified tasks.
5. Develop a CLI application to use the function.

## Install Pillow

=== "Using `uv`"
    ```doscon
    > uv add Pillow
    > uv run -- python -c "import PIL; print(PIL.__version__)"
    12.2.0
    ```
=== "Using `pip`"
    ```doscon
    > pip install Pillow
    > uv run -- python -c "import PIL; print(PIL.__version__)"
    12.2.0
    ```

## Application Development

### Pillow Documentation

[Pillow documentation](https://pillow.readthedocs.io/en/stable/) is searcheable and searching for the selected keywords yielded the following results:

1. Keyword: scale. Result: `PIL.ImageOps.scale(image: Image, factor: float, resample: int = Resampling.BICUBIC) → Image`
2. Keyword: resize. Result: `Image.resize(size: tuple[int, int] | list[int] | NumpyArray, resample: int | None = None, box: tuple[float, float, float, float] | None = None, reducing_gap: float | None = None) → Image`
3. Keyword: convert. Result: `Image.convert(mode: str | None = None, matrix: tuple[float, ...] | None = None, dither: Dither | None = None, palette: Palette = Palette.WEB, colors: int = 256) → Image`

Let us use `PIL.ImageOps.scale` to scale the image and `PIL.Image.convert()` to convert the image to black and white with the 

### Try Pillow in Python REPL

Open Python REPL or (IPython REPL inside Spyder IDE) and try the following:

```pycon
>>> from PIL import Image
>>> import PIL.ImageOps as imgops
>>> img_fname = "sample_img01.png"
>>> img = Image.open(img_fname)
>>> img.show()
>>> scale = 0.5
>>> img1 = imgops.scale(img, scale)
>>> img1.show()
>>> img2 = img.convert("L")
>>> img2.show()
>>> img3 = imgops.scale(img, scale).convert("L")
```
!!! warning "Alert"
    Pillow is imported as `PIL` not `pillow`!

![Scaled image](../assets/images.PNG)

### Function and Application

The function will replicate the code tried out in the Python REPL. Its interface is as follows:

**Name of function:** `process_image()`

**Input parameters:**

1. `image: PIL.Image` Object read from file in a format readable by Pillow.
2. `scale: float=1` Scaling factor assumed as `1` if not provided.
3. `bw: bool=False` Convert image to black and white if True.

**Output parameter:** `PIL.Image` object subjected to one or both of the operations, namely scaling and conversion to black and white.

```python title="image_app.py" linenums="1"
from pathlib import Path

from PIL import Image
import PIL.ImageOps as imageops
import typer

def img_scale_bw(img: Image, *, scale: float=1, bw: bool=False):
    if bw:
        img = img.convert("L")

    if (scale > 0):
        if scale != 1:
            img = imageops.scale(img, scale)
        return img
    else:
        raise ValueError(f"Scale factor {scale} is invalid. It must be greater than zero")

def get_output_fname(fname: str, scale: float, bw: bool) -> str:
    p = Path(fname)
    output_fname = p.stem

    if (scale > 0) and (scale != 1):
        output_fname += "_scaled"
    if bw:
        output_fname += "_bw"
    return f"{output_fname}{p.suffix}"

def main(img_fname: str, scale: float=1, bw: bool=False, save: bool=False):
    img = Image.open(img_fname)

    try:
        img_mod = img_scale_bw(img, scale=scale, bw=bw)

        if img_mod:
            if save:
                p = Path(img_fname)
                img_mod.save(get_output_fname(img_fname, scale, bw))
            else:
                img_mod.show()
    except Exception as e:
        print(f"Error: {e}")
        raise e


if __name__ == "__main__":
    # typer.run(main)
    main("sample_image01.png", scale=0.5, save=True)
    main("sample_image01.png", bw=True)
    main("sample_image01.png", scale=0.5, bw=True)
```

**Note**

1. The function `img_scale_bw(img: Image, *, scale: float=1, bw: bool=False)` carries out scaling and conversion to black and/or white depending on the values of `scale` and `bw` and returns the modified image object.
2. The function `get_output_fname(fname: str, scale: float, bw: bool) -> str` returns the name of the output file by appending `_scaled` and/or `_bw` depending on the values of `scale` and `bw`.
3. The function `main(img_fname: str, scale: float=1, bw: bool=False, save: bool=False)` is the main driver function that calls `img_scale_bw()` given the name of the input image file, scaling factor `scale`, whether or not to convert the image to black and white based on the value of `bw` and whether to save the modified image to file based on `save` or display the image on screen. This can be easily converted into a CLI application with the help of `typer`.
4. The `PIL.Image.show()` function requires a default image viewer application defined by the operating system.

