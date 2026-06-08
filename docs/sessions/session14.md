# Session 14: A Python Package for Reinforced Concrete Design as per IS456:2000

**Planned Date: 13-06-2026 4:00 pm to 6:00 pm**

## Agenda

1. What should the package do?
2. Which design and implementation approach is better?
3. What is the starting point for the design?
4. Should I design everything fist before I begin implementation?

# What should the package do?

This is an important question to answer. It defines the scope of the work we are about to undertake. It also helps us think about the components of the software that must be implemented to meet the expected outcomes.

One way to answer this question is to make a list of all the things the package should be able to do. For example:

1. Will the package to only design or also do detailing?
2. Does *design* mean - design of an entire structure, design of components of a structure, design of cross sections of an individual member?
3. Does designing a beam include design for bending, shear and torsion at selected locations along its length or exclude design for torsion?