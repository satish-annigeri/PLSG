# Section Properties

[Task 6](../tasks/task20260415.md#task-for-non-structural-engineers) defined two problems, the first of which required the geometric properties of sections as per SP-6(1).

It was suggested to use the [sectionproperties](https://sectionproperties.readthedocs.io/en/stable/index.html) package for the calculations. Let us do the following:

1. Install `sectionproperties` package from PyPI.
2. Study the documentation to create an I-section and calculate its geometric properties.
3. Try out the commands from Python REPL.
4. Develop a class to perform the specified tasks.
5. Develop a function to read data froma CSVV/Excel file and use the class to calculate geometric properties of sections listed therein.
6. Develop a CLI application to use the function.

## Install Pillow

=== "Using `uv`"
    ```doscon
    > uv add sectionproperties
    > uv run -- python -c "import sectionproperties"
    ```
    If no error is generated, the package is installed correctly.
=== "Using `pip` on Windows"  
    ```doscon
    > .venv\Scripts\activate
    (.venv) > pip install sectionproperties
    (.venv) > python -c "import sectionproperties"
    ```
    If no error is generated, the package is installed correctly.
=== "Using `pip` on GNU/Linux or macOS"  
    ```doscon
    > source .venv/bin/activate
    (.venv) > pip install sectionproperties
    (.venv) > python -c "import sectionproperties"
    ```
    If no error is generated, the package is installed correctly.

## Application Development

### `sectionproperties` Documentation

Exploring the [`sectionproperties` documentation](https://sectionproperties.readthedocs.io/en/stable/index.html) showed that the steps to calculating geometric properties of a section require the following steps:

1. Create a geometry.
2. Create a mesh for the geometry.
3. Create a section (`sectionproperties.analysis.Section`) from the geometry.
4. Calculate geometric propertiesof the section.
5. There is a pre-defined library of functions to create standard geometris and the one that is appropriate for steel cross sections as per SP-6(1) are `tapered_flange_i_section()` for I sections and `tapered_flange-channel` for channel sections.

### Try sectionproperties in Python REPL

Open Python REPL or (IPython REPL inside Spyder IDE), note down the size of ISMB 300 from SP-6(1)  and try the following:

```pycon
>>> from sectionproperties.pre.library import tapered_flange_i_section
>>> from sectionproperties.analysis import Section
>>> geom = tapered_flange_i_section(d=300, b=140, t_f=12.4, t_w=7.5, r_r=14.0, r_f=7.0, alpha=8, n_r=16)
>>> geom.create_mesh(mesh_sizes=0)
<sectionproperties.pre.geometry.Geometry object at 0x000001E97ECEAF90>
>>> geom.plot_geometry()
>>> sec = Section(geometry=geom)
>>> sec.calculate_geometric_properties()
>>> sec.display_results()
     Section Properties
┏━━━━━━━━━━━┳━━━━━━━━━━━━━━┓
┃ Property  ┃        Value ┃
┡━━━━━━━━━━━╇━━━━━━━━━━━━━━┩
│ area      │ 5.626648e+03 │
│ perimeter │ 1.084520e+03 │
│ qx        │ 8.439972e+05 │
│ qy        │ 3.938654e+05 │
│ ixx_g     │ 2.126448e+08 │
│ iyy_g     │ 3.210956e+07 │
│ ixy_g     │ 5.907981e+07 │
│ cx        │ 7.000000e+01 │
│ cy        │ 1.500000e+02 │
│ ixx_c     │ 8.604526e+07 │
│ iyy_c     │ 4.538987e+06 │
│ ixy_c     │ 2.235174e-08 │
│ zxx+      │ 5.736351e+05 │
│ zxx-      │ 5.736351e+05 │
│ zyy+      │ 6.484268e+04 │
│ zyy-      │ 6.484268e+04 │
│ rx        │ 1.236627e+02 │
│ ry        │ 2.840237e+01 │
│ i11_c     │ 8.604526e+07 │
│ i22_c     │ 4.538987e+06 │
│ phi       │ 0.000000e+00 │
│ z11+      │ 5.736351e+05 │
│ z11-      │ 5.736351e+05 │
│ z22+      │ 6.484268e+04 │
│ z22-      │ 6.484268e+04 │
│ r11       │ 1.236627e+02 │
│ r22       │ 2.840237e+01 │
└───────────┴──────────────┘

>>> sec.get_area()
np.float64(5626.648100857684)
>>> sec.get_ic()
(np.float64(86045259.31526682), np.float64(4538987.412026007), np.float64(2.2351741790771484e-08))
>>> sec.get_z()
(np.float64(573635.0621017787), np.float64(573635.0621017789), np.float64(64842.67731465717), np.float64(64842.6773146573))
>>> sec.get_rc()
(np.float64(123.66266358883864), np.float64(28.40237203783421))
```
!!! warning
    Slope of Flange D for ISMB 300 in SP-6(1) is 98 degrees (measured with reference to the vertical direction). `alpha` of `tapered_flage_i_section()` is 8 degrees (measured with respect to horizontal direction)

![Scaled image](../assets/ismb300.png)

The area of cross section as per SP-6(1) is $56.26 \text{cm}^2$ whereas the area as calculated by `sectionproperties` is $5626.648100857684 \text{mm}^2 = 56.27 \text{cm}^2$, an error 0f $0.01 \text{cm}^2$ with respect to the value in SP-6(1).

### Class and Application

Let us create a class to store the properties of an I section and provide methods to perform the required tasks. Let us use `dataclasses.dataclass` to simplify the creation of the class.

**Name of class:** `class ISection`

**Object initialisation parameters:**

1. Depth of the tapered flange I section `d` - $h$ in SP-6(1)
2. Width of the tapered flange I section `b` - $b$ in SP-6(1)
3. Mid-flange thickness of the tapered flange I section (measured at the point equidistant from the face of the web to the edge of the flange) `t_f` - $t_f$ in SP-6(1)
4. Web thickness of the tapered flange I section `t_w` - $t_w$ in SP-6(1)
5. Root radius of the tapered flange I section `r_r` - $r_1$ in SP-6(1)
6. Flange radius of the tapered flange I section `r_f` - $r_2$ in SP-6(1)
7. Flange angle of the tapered flange I section in degrees `alpha` - Slope of flange $D - 90$ degrees in SP-6(1)
8. Number of points discretising the radii `n_r` to be chosen by the user


**Methods:**  

1. Plot geometry `plot_geometry()`
2. Display geometric properties `display_geometric_properties()`

**Properties**

1. Area `area`
2. Second moment of area about centroidal axes `Ixx`, `Iyy`
3. Section modulus about centroidal axes `Zxx`, `Zyy`
4. Radius of gyration about centroidal axes `rxx`, `ryy`

```python title="secprop.py" linenums="1"
from dataclasses import dataclass

from sectionproperties.pre.library import tapered_flange_i_section
from sectionproperties.analysis import Section


@dataclass
class ISection:
    d: float
    b: float
    t_f: float
    t_w: float
    r_r: float
    r_f: float
    alpha: float
    n_r: int = 16

    def __post_init__(self):
        self.geom = tapered_flange_i_section(d=self.d, b=self.b, t_f=self.t_f, t_w=self.t_w, r_r=self.r_r, r_f=self.r_f, alpha=self.alpha, n_r=self.n_r)
        self.geom.create_mesh(mesh_sizes=0)
        self.sec = Section(geometry=self.geom)
        self.sec.calculate_geometric_properties()

    def display_geometric_properties(self):
        self.sec.display_results()

    def plot_geometry(self):
        self.geom.plot_geometry()

    @property
    def area(self):
        return self.sec.get_area()

    @property
    def Ixx(self):
        return self.sec.get_ic()[0]

    @property
    def Iyy(self):
        return self.sec.get_ic()[1]

    @property
    def Zxx(self):
        return self.sec.get_z()[0]

    @property
    def Zyy(self):
        return self.sec.get_z()[2]

    @property
    def rxx(self):
        return self.sec.get_rc()[0]

    @property
    def ryy(self):
        return self.sec.get_rc()[1]


if __name__ == "__main__":
    ISMB300 = ISection(d=300, b=140, t_f=12.4, t_w=7.5, r_r=14.0, r_f=7.0, alpha=8, n_r=32)
    print(f"A = {ISMB300.area / 1e2:.2f} cm^2")
    print(f"Ixx = {ISMB300.Ixx / 1e4:.1f} cm^4")
    print(f"Iyy = {ISMB300.Iyy / 1e4:.1f} cm^4")
    print(f"Zxx = {ISMB300.Zxx / 1e3:.1f} cm^3")
    print(f"Zyy = {ISMB300.Zyy / 1e3:.1f} cm^3")
    print(f"rxx = {ISMB300.rxx / 10:.2f} cm")
    print(f"ryy = {ISMB300.ryy / 10:.2f} cm")
```

The output is very close or identical to the values in SP-6(1) and is shown below:
```doscon
A = 56.27 cm^2
Ixx = 8604.3 cm^4
Iyy = 453.9 cm^4
Zxx = 573.6 cm^3
Zyy = 64.8 cm^3
rxx = 12.37 cm
ryy = 2.84 cm
```

**Note**

1. The magic method `__post_init__(self)` runs automatically immediately after the object is initialized and gives an opportunity to the prorgammer to do post initialization steps if any. This method is necessary because the `__init__(self)` magic method is automatically generate by `dataclass`.
2. The `__post_init__()` magic method automatically creates the geometry and the section using the fields in the initialized object.
3. The `@property` decoratotr available through the `dataclass` allows us to write a **getter**, that is, a way to **get** a value from inside the object. Not having to write a getter function with the trailing parentheses `()` makes the method appear like a property.


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