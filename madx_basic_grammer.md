---
marp: true
---


# Basic Grammar

```madx
LABEL: CLASS, attributes,... ;
```

For example, CLASS are like SBEND, QUADRUPOLE, SEXTUPOLE, etc.
Attribute types depend on the class. QUADRUPOLE has k value, length, etc.

See the references:
- [MAD-X Primer](https://indico.cern.ch/event/509762/contributions/2450804/attachments/1487283/2338842/MAD-X-Primer.pdf)
- [MAD-X Manual](http://madx.web.cern.ch/madx/doc/usrguide/usrguide.html)

---
# Comment

```madx
! line comment
// line comment  
/* area comment */
```
Line and area comments are supported.

---

# Expression

```madx
// normal expression
my_var = 1234;

// deferred expression
my_var := GAUSS() * 0.001;
```

! Deferred expressions become important for error assignment and matching.

---

# Machine Description by statements

---

# Element definition

```madx
// subclass, element class, attribute
MQL: QUADRUPOLE, L=1.0;

// use element
QFL01: MQL;
```

---

# Sub class

```madx
// Dipole
MB001: RBEND, L=14.3, ANGLE=2*PI/1132;

// Quadrupoles
QF001: QUADRUPOLE, L=0.5, K1=+0.00147235;

// Sextupoles
SF001: SEXTUPOLE, L=1.4, K2=+0.00147235;

// Orbit correction kicker
MCV01: VKICKER, L=0.1, KICK:=KCV01;
```

---

# Multipoles

```madx
// General multipole element
MPLE01: MULTIPOLE, LRAD=0.0, TILT=angle, KNL={k0L, k1L}, KSL={k0L, k1L};

// Quadrupole as multipole
QFT: MULTIPOLE, LRAD=0, KNL={0, k1L, 0, 0};
```

---

# Markers (Inactive element)

```madx
START_IP: MARKER;
END_IP: MARKER;
```


---

# Sequence

Align elements between "SEQUENCE" and "ENDSEQUENCE" keywords.
- AT: A relevant position from start of sequence.
- FROM: A relevant position from an existing element.

```madx
seq_name: SEQUENCE, REFER=CENTER, L=6912.00;
MQF05:     MQL,     AT=256.0000;
BPMH05:    MONITOR, AT=-1.75,    FROM=MQF05;
MCH05:     HKICKER, AT=2.10,     FROM=MQF05;
MBL05.001: MBL,     AT=265.9000;
ENDSEQUENCE;
```

Sequences can be nested.

---

# Periodic machine

Can be defined with while loop with a lattice cell:

```madx
n = 1;
while(n < ncell+1) {
    // elements
    n = n + 1;
}
```

---

# Commands 

---

# MAD-X Commands

Commands are used to define and execute actions on the machines:

- Calculations of Twiss functions
- I/O of the lattices  
- Particle tracking
- Lattice matching

---

# Beam

Create a beam and assign to a sequence:

```madx
BEAM, PARTICLE=PROTON, ENERGY=7000, SEQUENCE=seq_name;
```

---

# I/O

```madx
// Read sequence from file
CALL, FILE="filename.madx";

// Use the sequence
USE, SEQUENCE=seq_name;
```

---

# Calculate Linear Optics

Basic Twiss calculation:

```madx
TWISS;
```

Output can be customized:

```madx
SELECT, FLAG=TWISS, COLUMN=NAME,S,MUX,BETX,MUY,BETY;
TWISS, FILE="twiss.out";
```

---

# Plot

```madx
SELECT, FLAG=TWISS;
TWISS, FILE="twiss.beta";
PLOT, HAXIS=S, VAXIS=BETX,BETY;
```

.ps file and .out file are generated.

---

# Matching

- Global Matching
- Local Matching

---

# Global Matching

Some global machine parameters such as tune or chromaticity can be adjusted by global matching:

```madx
MATCH, SEQUENCE=seq_name;
    VARY, NAME=KQF, STEP=0.00001;
    VARY, NAME=KQD, STEP=0.00001;
    GLOBAL, SEQUENCE=seq_name, Q1=26.58;
    GLOBAL, SEQUENCE=seq_name, Q2=26.62;
    LMDIF, CALLS=10, TOLERANCE=1.0E-21;
ENDMATCH;
```

! Use the deferred variable definition for KQF.

---

# Local Matching

```madx
MATCH, SEQUENCE=SEQUENCE_NAME, RANGE=LEFT/RIGHT;
    VARY, NAME=KQ1.L, STEP=0.0001;
    CONSTRAINT, RANGE=RIGHT, SEQUENCE=SEQUENCE_NAME, BETX=10.0, BETY=10.0;
    CONSTRAINT, RANGE=IP, SEQUENCE=SEQUENCE_NAME, BETX=1.0, BETY=1.0;
    LMDIF, CALLS=100, TOLERANCE=1.0E-21;
ENDMATCH;
```
---

# Error Definition

Alignment and field errors can be assigned:

### Alignment Error

```madx
SELECT, FLAG=ERROR, CLASS=QUADRUPOLE;
EALIGN, DX:=GAUSS()*0.0005, DY:=GAUSS()*0.0002;
```

### Field Error

```madx
SELECT, FLAG=ERROR, CLASS=RBEND;
EFCOMP, RADIUS:=0.017, ORDER:=0, DKNR:={}, DKSR:={};
```

---

# TRACKING

Particle tracking simulations:

```madx
! Single particle tracking
TRACK, DELTAP=0.001, ONEPASS;
    START, X=0.001, Y=0.001;
    RUN, TURNS=1000;
ENDTRACK;

! Multiple particles
TRACK, DELTAP=0.001;
    START, X=0.001, Y=0.001, PX=0.0001, PY=0.0001;
    START, X=-0.001, Y=-0.001, PX=-0.0001, PY=-0.0001;
    RUN, TURNS=100, FFILE=1;
ENDTRACK;
```

Output files are generated for analysis of particle trajectories.