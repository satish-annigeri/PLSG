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
=== "Using `pip` on Windows"  
    ```doscon
    > .venv\Scripts\activate
    (.venv) > pip install Pillow
    (.venv) > python -c "import PIL; print(PIL.__version__)"
    12.2.0
    ```
=== "Using `pip` on GNU/Linux or macOS"  
    ```doscon
    > source .venv/bin/activate
    (.venv) > pip install Pillow
    (.venv) > python -c "import PIL; print(PIL.__version__)"
    12.2.0
    ```

## Application Development

### Pillow Documentation

[Pillow documentation](https://pillow.readthedocs.io/en/stable/) is searcheable and searching for the selected keywords yielded the following results:

1. Keyword: scale. Result: `PIL.ImageOps.scale(image: Image, factor: float, resample: int = Resampling.BICUBIC) → Image`
2. Keyword: resize. Result: `Image.resize(size: tuple[int, int] | list[int] | NumpyArray, resample: int | None = None, box: tuple[float, float, float, float] | None = None, reducing_gap: float | None = None) → Image`
3. Keyword: convert. Result: `Image.convert(mode: str | None = None, matrix: tuple[float, ...] | None = None, dither: Dither | None = None, palette: Palette = Palette.WEB, colors: int = 256) → Image`

Let us use `PIL.ImageOps.scale` to scale the image and `PIL.Image.convert()` to convert the image to grayscale with the 

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
3. `bw: bool=False` Convert image to grayscale if True.

**Output parameter:** `PIL.Image` object subjected to one or both of the operations, namely scaling and conversion to grayscale.

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
    try:
        img = Image.open(img_fname)
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
    main("sample_image01.png", scale=0.5, save=True)
    main("sample_image01.png", bw=True)
    main("sample_image01.png", scale=0.5, bw=True)
```

**Note**

1. The function `img_scale_bw(img: Image, *, scale: float=1, bw: bool=False)` carries out scaling and conversion to black and/or white depending on the values of `scale` and `bw` and returns the modified image object.
2. The function `get_output_fname(fname: str, scale: float, bw: bool) -> str` returns the name of the output file by appending `_scaled` and/or `_bw` depending on the values of `scale` and `bw`.
3. The function `main(img_fname: str, scale: float=1, bw: bool=False, save: bool=False)` is the main driver function that calls `img_scale_bw()` given the name of the input image file, scaling factor `scale`, whether or not to convert the image to grayscale based on the value of `bw` and whether to save the modified image to file based on `save` or display the image on screen. This can be easily converted into a CLI application with the help of `typer`.
4. The `PIL.Image.show()` function requires a default image viewer application defined by the operating system.

The code below the `#!py if __name__ == "__main__":` block tests three conditions:

1. Apply a scale factor `0.5` and save the image to file `sample_image01_scaled.png`.
2. Convert the image to grayscale and display the image on screen.
3. Scale the image to `0.5` times its original size and convert the image to grayscale and display the image on screen.

### CLI Application

To convert this application to a CLI application, delete the three lines below the  `#!py if __name__ == "__main__":` block and replace them with a single line `#!py typer.run(main)`.

```python title="image_app.py" linenums="38" hl_lines="1 8"
# Lines above not shown
    except Exception as e:
        print(f"Error: {e}")
        raise e


if __name__ == "__main__":
    typer.run(main)
```

Now test to verify that the CLI application displays help with the following command:

=== "Using `uv`"
    ```doscon
        > uv run -- python image_app.py --help
    ```
=== "Using `venv` on Windows"
    ```doscon
    > .venv\Scripts\activate
    (.venv) > python image_app.py
    ```
=== "Using `venv` on GNU/Linux or macOS"
    ```doscon
    > source .venv/bin/activate
    (.venv) > python image_app.py
    ```

This should display the following output:
```doscon
                                                                                    
    Usage: image_app.py [OPTIONS] IMG_FNAME                                        
                                                                                    
    ╭─ Arguments ──────────────────────────────────────────────────────────────────╮
    │ *    img_fname      TEXT  [required]                                         │
    ╰──────────────────────────────────────────────────────────────────────────────╯
    ╭─ Options ────────────────────────────────────────────────────────────────────╮
    │ --scale                 FLOAT  [default: 1]                                  │
    │ --bw       --no-bw             [default: no-bw]                              │
    │ --save     --no-save           [default: no-save]                            │
    │ --help                         Show this message and exit.                   │
    ╰──────────────────────────────────────────────────────────────────────────────╯
```

Try the CLI application with the following commands:

=== "Using `uv`"
    ```doscon
    > uv run -- python image_app.py sample_image01.png --scale 0.5 --save
    > uv run -- python image_app.py sample_image01.png --bw
    > uv run -- python image_app.py sample_image01.png --scale 0.5 --bw
    ```
=== "Using `venv` on Windows, GNU/Linux or macOS"
    ```doscon
    > python image_app.py sample_image01.png --scale 0.5 --save
    > python image_app.py sample_image01.png --bw
    > python image_app.py sample_image01.png --scale 0.5 --bw
    ```

**Note**

1. The first command scales the image to half its original size and saves the modified image to `sample_image01_scaled.png`.
2. The second command converts the image to grayscale and displays the converted image on screen.
3. The second command scales the image to half its original size, converts the image to grayscale and displays the converted image on screen.

## Lessons to remember

The above code is the outcome of a systematic and step-wise refinement of a series of thoughts:

1. Understand what is the expected outcome.
2. Identify the package that can accomplish the given task and study its documentation to identify the functions that are required.
3. Interactively try out the functions to test your own understanding of the ackage, the selected functions to carry out the task and close the gap in your understanding of the package and its usage.
4. Design the application using the appropriate approach, procedural paradigm in this case. Thaus, identify the functions required, their signature - name, input parameters and output parameters. Ensure that each function accomplishes a single well defined task. Any time a function grows too large, it is time to design a function, and replace several lines by a single function call.
5. Orchestrate the call to lower level functions to build higher level functions. In this example, `main()` calls `img_scale_bw()` and `img_scale_bw()` depends on `get_output_fname()` to accomplish the task of generating the name of the output file. This organisation is far simpler compared to writing the whole program without using functions at all. These are the advantages that accrue:  
    1. Each function accomplishes a simple well defined task and can be developed and tested independently and once tested, it can be used as a black-box, unless you wish to add more functionality/features.
    2. Complex tasks can be accomplished by relying on lower level functions to handle the simpler tasks.
6. Test the application to ensure that all features are working as expected. In this case:  
    1. Scale the image.
    2. Convert the image to grayscale.
    3. Display the modified image on screen.
    4. Save the modified image to file with an appropriate name.
    5. Or any combination of the above.
7. Convert the application to a CLI application to make it usable from the command line.