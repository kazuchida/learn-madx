---
marp: true
---

# Cosylab Japan Internal Lectures #1

Accelerator Lattice Design and Simulation by MAD-X

2023.02.10 (FRI) Kazuhide Uchida

### Objective of this lecture.

- Learn how to use MADX

---

# MAD-X: Methodological Accelerator Design

- Free simulation code for beam optics and lattice design.
- Written in C/C++/F77/F90 and source code can be accessed on GitHub.
- MAD-X is a kind of single particle simulation, and not PIC simulation.
- MAD-X provides interpreter. So user can write input file and run it on MAD-X.

We will see how to write and run input files!

---

# Workflow of MAD-X

1. Define the machine hardware in input files (.madx)
    - Create own elements from classes.
    - Align the elements as a sequence.
2. Define the beam properties in input files
3. Activate the sequence
4. Execute the operation
    - Twiss parameters calculation
    - MATCHING
    - TRACKING, etc.

---

# References

- [MAD-X Github Repo](https://github.com/MethodicalAcceleratorDesign/MAD-X)
- [MAD-X Homepage](http://madx.web.cern.ch/madx/)
- [X.Feng, et. al., "REVIEW OF PROTON LINAC BEAM DYNAMIC SIMULATION CODE"](https://inspirehep.net/files/302d188a02f0e249db8f3c622a182920)
- [R.Cee, et. al., "A MAD-X MODEL OF THE HIT ACCELERATOR"](https://inspirehep.net/files/e368865b392d90f861385d199441be15)

