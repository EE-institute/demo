# The graphical formalism of GOSL

[//]: <> (Appendix A assumes that the reader knows the graphical formalism of GOSL. This need not be)
[//]: <> (the case for everyone. Therefore, we copy the relevant part of [1] Chap. 6 below. The textual)
[//]: <> (formalism of GOSL is included already in Chap. 2, The basics of DEMO-SL)

The graphical formalism of GOSL is based on the Venn diagram, as illustrated by Fig. 1. There
are two sets: RENTAL (with example elements r<sub>1</sub>, r<sub>2</sub> and r<sub>3</sub>) and PERSON (with example elements
p<sub>1</sub>, p<sub>2</sub>, p<sub>3</sub> and p<sub>4</sub>). The function renter is shown as a mapping from RENTAL to PERSON,
which are respectively the domain and the range of renter. The expression renter(r<sub>i</sub>) = p<sub>j</sub> means
that person p<sub>j</sub> is the renter of rental r<sub>i</sub>.

<a name="mathfuncmapping"><img src="images/mathfuncmapping.jpg" alt="mathfuncmapping" width="600"/>

![Fig. 1 Mathematical functions as mappings between sets]()

<a name="propmapping"><img src="images/propmapping.jpg" alt="propmapping" width="500"/>

![Fig. 2 Properties as mappings between entity classes]()

Fig. 2 exhibits the more stylised way in which functional mappings are represented in
GOSL. The roundangles9 represent entity classes, thus the extensions of entity types (cf. [1]
Chap. 5). The functions are now called properties. One best considers the lines with an arrow in
the middle as the bundles of separate mappings from elements in RENTAL to elements in PERSON
([cf. Fig. 1](#mathfuncmapping)).

Cardinality ranges are denoted as: <min>..<max>. Examples: 0..1, 1..1,
0..*, 1..* (“*” means undetermined). The default ranges are:
“1..1” at the side of the range, meaning that every element in the domain
is connected to exactly one element in the range;
“0..*” at the side of the domain, meaning that an element in the range
need not be connected to an element in the domain, and if it does, it may
be connected to many elements.
