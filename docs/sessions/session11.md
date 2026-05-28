# Session 11: Design and Development of Applications

**Date: 23-05-2026 4:00 pm to 6:00 pm**

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Developing an application to proportion an isolated rectangular footing

## Theory and sign conventions

See [Task 8](../tasks/task08_20260518.md#problem-statement) for the problem definition and [Snippet 4](../snippets/snippet04.md) for the theory, notations and sign conventions.

## Steps in Application Development

There are two distinct steps in developing an application:

1. Requirement study
2. Design of the application
3. Implementation of the application

These steps are not unique to application development. Most tasks that need to be executed, follow the same steps in their respective domains. Take for example a civl engineering task such as building a residence or water supply to an urban area. Similarly, all mechanical engineering tasks are good examples. Even, managing development and change in an organization to meet the needs and expectations of the future can also be considered as an example.

**Requirements study** is a deep examination of what the application is expected to do, as well as what it is **not expected to do**. For simple applications, this can be done by an individual developer but for complex projects, it may need an experienced software architect or a team of software architects. This stage results in an understanding of the architecture and technologies that are feasible and well suited for the task in hand.

**Design of an application** flows from the requirements study and the decisions regarding architecture and technologies can now be compared and a final decision arrived at. The design can be carried out independent of the programming language to be used but it narrows down the options based on the architecture and technologies that are to be supported. For example, if it is decided to use object oriented programming (OOP), programming languages that do not support OOP are ruled out. Other requirements may include strong support for numerical computations or graphical display etc. The outcome of a design may consist of flow charts, function interfaces and function dependence heirarchy in case of the procedural approach. In case of Object Oriented Analysis and design (OOAD), output may consist of class diagrams, class heirarchies, state diagrams etc. If the application uses a relational database, you may require entity-relationship diagrams and/or Structured Query Language (SQL) queries. At this stage, a choice of the programming language can usually be made.

**Implementation of the application** proceeds based on the output of the design phase. In case of the procedural approach, it may involve implementing the functions starting with the the most independent functions and progressing to the most dependent one. In case of OOP, it may involve starting with the least dependent classes and progressing to the most dependent and then wrting the functions to instantiate the objects and orchestrating their interactions. In either case, the implementation is iterative and may involve refactoring and sometimes even redesigning. At every stage of implementation, code needs to be tested, usually through systematic methods of testing.

## Some Tips for Application development

1. The most important of the above three steps is the requirements study. The architecture can be ambitious and the design and implementation can be taken up in phases. <br><br>It is like designing a campus for an educational institution: the master plan must be ambitious but the implementation must be based on immediate requirements, available time and budget. However, if the roads, water supply, sewage disposal are not considered in the master plan, future extension will be difficult or require major changes to architecture.<br><br>It is quite easy to be overambitious in the first phase of an application, but being aware of what is practical and achievable in terms of time, effort and budget is critical. 
2. For each phase of implementation, there must be a thorough design. When designing the first phase, you must be alert to the future expectations expressed in the architecture. When designing subsequent phases, you must fit neatly into the existing implementation.<br><br>If you need to reimplement previous phases of implementation, it is a sign of a poor architecture.
3. Implementation must go hand in hand with testing, it must not be an afterthought or a task to be taken up when the coding is complete. In fact, there is a method of application deevlopment called [Test Driven Development (TDD)](https://en.wikipedia.org/wiki/Test-driven_development) where it is required to write the tests before you implement the code. While it has its advantages and limitations, it is something to think about.
4. Comments within the code are very important and are a note to the developer as well as others who study your code. Comments clarify the intent of the code for future reference.<br><br>There are ways by which comments written in a specific way can be extracted into documentation of the source code. For Python, there are several specifications for commenting source code and software tools that can prepare documentation from them. [Zensical](https://zensical.org/) based on [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and [Sphinx](https://www.sphinx-doc.org/en/master/index.html) are the main document generation tools. Here is a good article on the topic of [Python source code documentation](https://realpython.com/documenting-python-code/).


## Incremental Application Development

Incremental development of the application will follow these steps:

1. Define the class to repersent a rectangular footing and its attributes
2. Add a method to calculate the area of the footing
3. Add a method to determine the lengths of the sides
4. Add a method to compute the pressure at any point within the footing
5. Add a method to compute the pressures at the four corners of the footing
6. Add a method to check whether the footing is safe
7. Add a method to iteratively increase the size of the footing until it becomes safe

```py title="rect_footing.py" linenums="1"
from dataclasses import dataclass
import math


class RectFooting:
    P: float  # kN
    Mx: float  # kNm
    My: float  # kNm
    bx: float  # m
    by: float  # m
    cx: float = 0.0  # m
    cy: float = 0.0  # m
    self_wt_factor: float = 10  # percentage of P


if __name__ == "__main__":
    f = RectFooting(150, 0, 0, 0.45, 0.23)
    print(f)
```

This should display the following output:
```doscon
RectFooting(P=150, Mx=0.0, My=0.0, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
```
!!! note
    The `dataclass` automatically provides the `__str__()` method that is used by `print()`.

Let us now add the method to calculate the required area of the footing based only on the axial load $P$ from the column, ignoring the moments $M_x, M_y$:

$$
A = \frac{\left(1 + \frac{\text{self weight factor}}{100} \right) \cdot P}{\text{SBC of foundation strata}}
$$

!!! warning "Alert"
    As the application changes, the new or changed lines are highlighted in blue color.

```py title="rect_footing.py" linenums="12" hl_lines="4-5 11-12"
#   Lines 1 - 12 not shown
    self_wt_factor: float = 10  # percentage of P

    def area(self, sbc: float) -> float:
        return (1 + self.self_wt_factor / 100) * self.P / sbc


if __name__ == "__main__":
    f = RectFooting(150, 0, 0, 0.45, 0.23)
    print(f)
    sbc = 130  # kN/m^2
    print(f.area(sbc))
```

You should see the following output:
```doscon
RectFooting(P=150, Mx=0.0, My=0.0, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
1.2692307692307692
```

Let us calculate the lengths of the sides based on a given aspect ratio $r = \frac{L_x}{L_y}$:

$$
\begin{align*}
    L_x &= r \cdot L_x \\
    A &= L_x \cdot L_y = r \cdot L_y^2 \\
    L_y &= \sqrt{\frac{A}{r}}
\end{align*}
$$

```py title="rect_footing.py" linenums="14" hl_lines="5-9 12-17"
# Lines 1-14 not shown
    def area(self, sbc: float) -> float:
        return (1 + self.self_wt_factor / 100) * self.P / sbc

    def lx_ly(self, sbc: float, aspect_ratio: float) -> tuple[float, float]:
        area = self.area(sbc)
        self.Ly = math.sqrt(area / aspect_ratio)
        self.Lx = aspect_ratio * self.Ly
        return self.Lx, self.Ly


if __name__ == "__main__":
    f = RectFooting(150, 0, 0, 0.45, 0.23)
    print(f)
    sbc = 130  # kN/m^2
    print(f.area(sbc))
    print(f.lx_ly(sbc, 1.0))
```

```doscon
RectFooting(P=150, Mx=0.0, My=0.0, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
1.2692307692307692
(1.126601424298216, 1.126601424298216)
```

Let us change $M_x = 0.2 \text{ kNm}, M_y = 0.5 \text{ kNm}$ and calculate the pressure at a point with coordinates $x, y$ due to $P, M_x, M_y$ applied at the origin:

$$
\begin{align*}
    p &= \frac{(1 + \frac{\text{Self weight factor}}{100}) \cdot P}{L_x \cdot L_y} - \frac{M_x}{\frac{L_y \cdot L_x^3}{12}} \cdot y + \frac{M_y}{\frac{L_x \cdot L_y^3}{12}} \cdot x \\
    &= \frac{(1 + \frac{\text{Self weight factor}}{100}) \cdot P}{L_x \cdot L_y} - \frac{12 \cdot M_x}{L_x \cdot L_y^3} \cdot y + \frac{12 \cdot M_y}{L_y \cdot L_x^3} \cdot x
\end{align*}
$$

```py title="rect_footing.py" linenums="21" hl_lines="4-9 13 16-19"
    # Lines 1-21 not shown
        return self.Lx, self.Ly

    def pressure(self, x: float, y: float) -> float:
        # Must be called only after self.lx_ly() has been called
        pz = (1 + self.self_wt_factor / 100) * self.P / (self.Lx * self.Ly)
        px = -12 * self.Mx / (self.Lx * self.Ly ** 3) * y
        py = 12 * self.My / (self.Ly * self.Lx ** 3) * x
        return pz + px + py


if __name__ == "__main__":
    f = RectFooting(150, 0.2, 0.5, 0.45, 0.23)
    print(f)
    sbc = 130.0  # SBC in kN/m^2
    print("Area =", f.area(sbc))
    print("Sides =", f.lx_ly(sbc, 1.0))
    print("Pressure at 1, 1 =", f.pressure(1, 1))
    print("Pressure at -1, -1 =", f.pressure(-1, -1))
```
The output should be as follows:
```doscon
RectFooting(P=150, Mx=0.2, My=0.5, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
Area = 1.2692307692307692
Sides = (1.126601424298216, 1.126601424298216)
Pressure at 1, 1 = 132.23471074380163
Pressure at -1, -1 = 127.76528925619836
```
Let us now calculate the pressures at the four corners:

```py title="rect_footing.py" linenums="21" hl_lines="4-9 20"
        # Lines 1-28 not shown
        return pz + px + py

    def corner_pressures(self) -> tuple[float, float, float, float]:
        p1 = self.pressure(self.Lx / 2, self.Ly / 2)
        p2 = self.pressure(self.Lx / 2, -self.Ly / 2)
        p3 = self.pressure(-self.Lx / 2, -self.Ly / 2)
        p4 = self.pressure(-self.Lx / 2, self.Ly / 2)
        return p1, p2, p3, p4


if __name__ == "__main__":
    f = RectFooting(150, 0.2, 0.5, 0.45, 0.23)
    print(f)
    sbc = 130.0  # SBC in kN/m^2
    print("Area =", f.area(sbc))
    print("Sides =", f.lx_ly(sbc, 1.0))
    print("Pressure at 1, 1 =", f.pressure(1, 1))
    print("Pressure at -1, -1 =", f.pressure(-1, -1))
    print("Pressure at corners =", f.corner_pressures())
```

Out should be as follows:
```doscon
RectFooting(P=150, Mx=0.2, My=0.5, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
Area = 1.2692307692307692
Sides = (1.126601424298216, 1.126601424298216)
Pressure at 1, 1 = 132.23471074380163
Pressure at -1, -1 = 127.76528925619836
Pressure at corners = (131.25881415343073, 132.9372330246717, 128.74118584656927, 127.06276697532829)
```
To check that the footing is safe, we check for two conditions:

1. Maximum pressure must be less than or equal to the SBC of the foundation strata
2. Minimum pressure must be greater than or equal to zero

```py title="rect_footing.py" linenums="28" hl_lines="4-8 20"
        # Lines 1-28 are not shown
        return p1, p2, p3, p4

    def is_safe(self, sbc: float) -> bool:
        pressures = self.corner_pressures()
        pmax = max(pressures)
        pmin = min(pressures)
        return (pmax <= sbc) and (pmin >= 0.0)


if __name__ == "__main__":
    f = RectFooting(150, 0.2, 0.5, 0.45, 0.23)
    print(f)
    sbc = 130.0  # SBC in kN/m^2
    print("Area =", f.area(sbc))
    print("Sides =", f.lx_ly(sbc, 1.0))
    print("Pressure at 1, 1 =", f.pressure(1, 1))
    print("Pressure at -1, -1 =", f.pressure(-1, -1))
    print("Pressure at corners =", f.corner_pressures())
    print("Footing is safe =", f.is_safe(sbc))
```

The output should be as follows:
```doscon
RectFooting(P=150, Mx=0.2, My=0.5, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
Area = 1.2692307692307692
Sides = (1.126601424298216, 1.126601424298216)
Pressure at 1, 1 = 132.23471074380163
Pressure at -1, -1 = 127.76528925619836
Pressure at corners = (131.25881415343073, 132.9372330246717, 128.74118584656927, 127.06276697532829)
Footing is safe = False
```

The footing is unsafe because we used only the value of $P$ when calculating the required area and neglected the effect of $M_x$ and $M_y$. One strategy to arrive at a safe design is to iteratively increase the length of the sides by a specified amount each time until the design is safe. This is a simple and practical approach instead of arriving at the required size through a derivation based on $P, M_x, M_y$ values. Moreover, the actual size of a footing in real life is never the exact value as calculated but a practical value based on fabrication practices.

Further, it is common practice to fix the sizes as a multiple of a suitably chosen value based on fabrication practices. Thus the initial sizes can be rounded up to the next higher multiple of a suitably chosen value.

Here is a function taht rounds up the given number $x$ to the next higher multiple of $m$.
```py
import math


def ceiling(x: float, m: float) -> float:
    return m * math.ceil(x / m)


if __name__ == "__main__":
    print(ceiling(1.12, 0.15))
```
This program prints the following result:
```doscon
1.2
```

For small values of $M_x, M_y$, this rounding is sufficient to result in a safe design. For large values of $M_x, M_y$, the strategy of iteratively increasing the length of the sidex will result in a safe design fairly quickly. Nevertheless, it is a good idea to specify the maximum number of iterations and raise an exception if the specified number of iterations do not result in a safe design. Smaller the increment in the length of the side, larger the number of iterations required.

## Full Implementation
```py title="rect_footing.py" linenums="1" hl_lines="5-6 32-39 62-77 93"
from dataclasses import dataclass
import math


def ceiling(x: float, m: float = 1) -> float:
    return m * math.ceil(x / m)


@dataclass
class RectFooting:
    P: float   # kN
    Mx: float  # kNm
    My: float  # kNm
    bx: float  # m
    by: float  # m
    cx: float = 0.0  # m
    cy: float = 0.0  # m
    self_wt_factor: float = 10  # percentage of P

    def area(self, sbc: float) -> float:
        return (1 + self.self_wt_factor / 100) * self.P / sbc

    def lx_ly(
        self, sbc: float, aspect_ratio: float) -> tuple[float, float]:
        area = self.area(sbc)
        Ly = math.sqrt(area / aspect_ratio)
        Lx = aspect_ratio * Ly
        self.Lx = Lx
        self.Ly = Ly
        return Lx, Ly

    def lx_ly_eqproj(self):
        reqd_area = self.area(sbc)
        bx_by = (self.bx - self.by)
        Lx = (bx_by / 2) + math.sqrt((bx_by / 2) ** 2 + reqd_area)
        Ly = Lx - bx_by
        self.Lx = Lx
        self.Ly = Ly
        return Lx, Ly

    def pressure(self, x: float, y: float) -> float:
        pz = (
            (1 + self.self_wt_factor / 100) * self.P / (self.Lx * self.Ly)
        )  # Must be called only after self.lx_ly() has been called
        px = -12 * self.Mx / (self.Lx * self.Ly**3) * y
        py = 12 * self.My / (self.Ly * self.Lx**3) * x
        return pz + px + py

    def corner_pressures(self) -> tuple[float, float, float, float]:
        p1 = self.pressure(self.Lx / 2, self.Ly / 2)
        p2 = self.pressure(self.Lx / 2, -self.Ly / 2)
        p3 = self.pressure(-self.Lx / 2, -self.Ly / 2)
        p4 = self.pressure(-self.Lx / 2, self.Ly / 2)
        return p1, p2, p3, p4

    def is_safe(self, sbc: float) -> bool:
        pressures = self.corner_pressures()
        pmax = max(pressures)
        pmin = min(pressures)
        return (pmax <= sbc) and (pmin >= 0.0)

    def calc_size(self, sbc: float, aspect_ratio: float):
        self.lx_ly(sbc, aspect_ratio)
        mx = my = 0.15
        maxiter = 10
        i = 0
        safe = self.is_safe(sbc)
        while not safe:
            i += 1
            self.Lx += mx
            self.Ly += my
            safe = self.is_safe(sbc)
            if safe:
                break
            elif i == maxiter:
                raise ValueError(f"Maximum iterations {i} reached")
        return i


if __name__ == "__main__":
    f = RectFooting(150, 5.0, 20.0, 0.45, 0.23)
    print(f)
    sbc = 130.0  # SBC in kN/m^2
    print("Area =", f.area(sbc))
    print("Sides =", f.lx_ly(sbc, 1.0))
    print("Pressure at 1, 1 =", f.pressure(1, 1))
    print("Pressure at -1, -1 =", f.pressure(-1, -1))
    print("Pressure at corners =", f.corner_pressures())
    print("Footing is safe =", f.is_safe(sbc))
    print(f.calc_size(sbc, 1.0))
    print(f.Lx, f.Ly)
    print(f.corner_pressures())
    print(f.lx_ly_eqproj(), (f.Lx - f.bx) == (f.Ly - f.by))
```
Output of the application is shown below:
```doscon
RectFooting(P=150, Mx=5.0, My=20.0, bx=0.45, by=0.23, cx=0.0, cy=0.0, self_wt_factor=10)
Area = 1.2692307692307692
Sides = (1.126601424298216, 1.126601424298216)
Pressure at 1, 1 = 241.73553719008268
Pressure at -1, -1 = 18.26446280991732
Pressure at corners = (192.94070767153673, 234.9011794525612, 67.05929232846327, 25.098820547438805)
Footing is safe = False
3
1.5766014242982158 1.5766014242982158
(89.34598371460784, 104.65634738389366, 43.41489270675038, 28.10452903746457)
(1.241958819582572, 1.021958819582572) True
```


