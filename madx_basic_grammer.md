---
marp: true
---


# Basic Grammer

```sh
LABEL: CLASS, attributes,... ;
```
<br>
For example, CLASS are like SBEND, QUADRUPOLE, SEXTUPOLE, etc.
Attribute types are depend on the class. QUADRUPOLE has k value, length, etc.

See the references:
- [MADX Primer](https://indico.cern.ch/event/509762/contributions/2450804/attachments/1487283/2338842/MAD-X-Primer.pdf)
- [MADX Manual]()

---
# Comment

```sh
! line commnet
// line comment
/* area comment */ 
```
line and area comment are supported.

---

# Expression

```sh
// normal expression
my_var = 1234;

// defered expression
my_var := GAUSS() * 001;
```

! deffered expressions becomes important for error assignment and matching.

---

# Machine Description by statements

---

# Element definition

```sh
// subclass, element class, attribute
MQL: QUADRUPOLE, L=1.0;

// use element
QFL01: MQL;
```

---

# Sub class

```sh
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

```sh
// 
MPLE01: MULTIPOLE, LRAD=0.0, TILT=angle, KNL={k0L, k1L}, KSL={k0L, k1L};

//
QFT: MULTIPOLE, LRAD=0, KNL={0, k1L,0,0};

```

---

# Markers (Inactive element)

```sh
START_IP: MARKER, AT=183.872;
```


---

# Sequence

Align elements betweekn "SEQUENCE" and "ENDSEQUENCE" keywords.
AT:   A relevant position from start of sequence.
FROM: A relevant position from an existing element.

```sh
seq_name: SEQUENCE, REFFER=CENTER, LENGTH=6912.00;
...
...
MQF05:     MQL,     AT=256.0000;
BPMH05:    MONITOR, AT-1.75    , FROM=MQF05;
MCH05:     HKICKER, AT=2.10    , FROM=MQF05;
MBL05.001: MBL,     AT=265.9000;
...
...
ENDSEQUENCE;
```

sequence can be nested

---

# Periodic machine

can be defined with while loop with a lattice cell;

```sh
n=1;
while(n < ncell+1){
    ...
    elements
    ...
    n = n+1;
}

```

---

# Commands 

---

# MAD-X Commands

Commands are used to define, eecute actions on the machines.

- Calculations of Twiss functions
- I/O of the lattices
- Particle tracking
- Lattice matching

---

# beam

Create a beam and assign on a sequence.


```sh
BEAM, PARTICLE=name, ENERGY=xxx, SEQUENCE=seq_name;
```

---

# IO

```sh
// read sequence from file
CALL, FILE="filename"

// use the sequence
USE, PERIOD="seq_name"

```

---

# Calculate Linear 

```TWISS;```

Calc output can be modified.

```sh
SELECT, FLAG=TWISS, COLUMN=NAME, S, MUX, EBTX, MUY, BETY;
TWISS, FILE="twiss.out"
```

---

# Plot

```sh
SELECT, FLAG=TWISS;
TWISS, FILE="twiss.beta";
PLOT, HAXIS=S, VAXIS=BETX, BETY;
```
.ps file and .out file are generated.

---

# Matching

- Global Matching
- Local Matching

---

# Global Matching

Some global machine parameters such as tune or chromaticity can be adjusted by global matching.

```sh
MATCH, SEQUENCE="seq_name";
VARY, NAME=KQF, STEP=0.00001;
VARY, NAME=KQF, STEP=0.00001;
GLOBAL, SEQUENCE="seq_name", Q1=26.58;
GLOBAL, SEQUENCE="seq_name", Q2=26.62;
LMDIF, CALLS=10, TOLERANCE=1.0E-21;
ENDMATCH;
```

! use the defered variable definition for KQF.

---

# Local Matching

```sh
MATCHING, SEQUENCE="SEQUENCE_NAME", RANGE=LEFT/RIGHT, BETX=,BETY-;

VARY, NAME=KQ1.L, STEP=0.0001;
...

VONSTRAINT, RANGE=RIGHT, SEQUENCE="SEQUENCE_NAME", BETX=, BETY=;
CONSTRAINT, RANGE=IP, SEQUENCE="SEQUENCE_NAME", BETX=, BETY=;
LMDIF, CALLS=100, TOLERANCE=1.0E-21;
ENDMATCH;

```
---

# Error definition

Alignment and field errors can be assigned.

### Alignment error

```
SELECT, FLAG=ERROR, CLASS=MQ
EALIGN, 
    DX:=GAUSS()*0.0005;
    DY:=GAUSS()*0.0002;
```

### Field error

```
SELECT, FLAG=ERROR, CLASS=MB;
EFCOMP, RADIUS:=0.017, ORDER:=0,
DKNR:={},
DKSR:={},
```

---

# TRACKING

```
TBA
```

---