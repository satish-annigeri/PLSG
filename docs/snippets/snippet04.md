# Isolated Rectangular Footing

## Notations and Sign Conventions

The origin of the coordinate system is assumed to be at the geometric centre of the rectangular footing. Coordinate axes are positive as shown in the figure. #L_x$ and $L_y$ do not have sign associated with them. All other quantities are positive when they are as shown in the figure. Values opposite to those shown are taken to be negative.

![Isolated rectangular footing](../assets/rect_footing.jpeg)

| Quantity     | Description                       | Sign Convention |
|:-------------|:----------------------------------|:----------------|
|$L_x$, $L_y$  | Dimensions of footing along x- and y-axis, respectively | Not applicable |
|$c_x, c_y$    | Coordinates of column from the origin | Positive along positive direction of axes |
|$x, y$        | Coordinates of the point at which pressure is to be calculated | Positive along positive direction of axes |
|$P'$           | Axial load at the base of the column | Positive when acting downwards |
|$M'_x$         | Moment at the base of the column about the x-axis | Positive as per the Right Hand Rule |
|$M'_y$         | Moment at the base of the column about the y-axis | Positive as per the Right Hand Rule |

Equivalent axial load $P$ and moments $M_x, M_y$ about the x- and y-axes at he origin due to applied loads:

$$
\begin{align*}
    P &= P' \\
    M_x &= M'_x - P' \cdot c_y \\
    M_y &= M'_y + P' \cdot c_x
\end{align*}
$$

Pressure at $x, y$ due to $P, M_x$ and $M_y$:

$$
\begin{align*}
    p &= \frac{P}{L_x \cdot L_y} - \frac{M_x}{\frac{L_x \cdot L_y^3}{12}} \cdot y + \frac{M_y}{\frac{L_y \cdot L_x^3}{12}} \cdot x \\
    &= \frac{P}{L_x \cdot L_y} - \frac{12 \cdot M_x}{L_x \cdot L_y^3} \cdot y  + \frac{12 \cdot M_y}{L_y \cdot L_x^3 \cdot x }
\end{align*}
$$

Pressure at $x, y$ due to self weight of the footing depends on the thickness variation of the footing. For simplicity, let us assume the thickness to be uniform and equal to the equivalent thickness of the footing, that is, total self weight divide by the area of contact $L_x \cdot L_y$. Typically, the thickness is not known at the time of determining the plan dimensions of the footing and it is customary to assume the self weight to be a certain percentage of the column load. While this may work satisfactorily for concentrically loaded footings, it may not be true for eccentrically loaded footings.

In any case, it is a good idea to compute the actual self weight of the footing once the design is complete and check it against the initially assumed self weight. If the actual value turns out to be significantly different, either greater than or lesser than the assumed value, the footing may be redesigned with the assumed self weight equal to the actual self weight. After a few iterations, the design will converge to a satisfactory value of actual self weight compared the the self weight assumed at he start of the iteration.

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


## Application

