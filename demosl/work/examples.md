# The DEMO Specification Language v4.10

## Abstract

Conceptual models must be expressed in a suitable language in order to communicate them. To avoid misunderstandings, this language should allow for formulating clear, unambiguous expressions. First order logic is a language that has all the properties one needs and wants, but it has the drawback that its common Peano-Russell notation puts off people who lack a background in logic and mathematics. The DEMO Specification Language (DEMO-SL) offers a user-friendly look, although it is firmly based on first order logic. The syntax of DEMO-SL is defined in Extended Backus-Naur Form (EBNF) or in syntax diagrams. In addition to formal textual expressions, it allows for graphical representations. Three aspect models, the Cooperation Model, the Process Model, and the Fact Model, are represented in diagrams. Diagrams are kept simple, which means that what cannot be expressed in a diagram, must be expressed in formal text. The Action Model is expressed in formal text only. In addition to the explanation and illustration of DEMO-SL, the meta model or schema of each of the four aspect models is presented and discussed, as well as the schema of each of the diagrams kinds and table kinds.

## Ownership and Authorship

The ownership of the DEMO Specification Language, abbreviated to DEMO-SL, lies with the Enterprise Engineering Institute. Ownership implies the responsibility regarding the correctness of the content of this document, and its availability on the website.

The version of this document is 4.10.1. Major changes to the content will result into version 4.11, 4.12, etc. Minor changes, notably error corrections, will result into version 4.10.1, 4.10.2, etc.

The most recent version, as well as a selected number of earlier versions, can always be downloaded from www.ee-institute.org.

The authorship of version 4.10 lies with Jan Dietz (rgg@sapio.nl)

### Differences with version 4.10.0

Version 4.10.1 contains minor changes to version 4.10.0, mainly textual corrections.

## 1. Introduction

In this document, the formal language is presented in which the essential models of DEMO-4 (Design and Engineering Methodology for Organisations), as defined in [1], Chap. 12, are expressed. The language is called DEMO Specification Language, or DEMO-SL for short.

The distinction between models on the one side and the diagrams, tables and formalised texts in which they are expressed on the other side, is crucial: they constitute respectively the semantics and the syntax of DEMO-SL (cf. [1] Chap. 6).

Expressions in DEMO-SL are basically formal textual expressions in first order logic [2]. Many textual expressions have also a graphical or tabular equivalent, because the appreciation of formal text in current practice is generally low, particularly by people who lack a logical/mathematical background. Therefore, one should understand DEMO diagrams as graphical representations of logical formulas. The same holds for tabular expressions.

Despite the current preference for diagrams to formal text, there are limits to the expressive power of diagrams: they can easily become impractical if one has to remember (too) many shapes, symbols and constructs. Therefore, the diagrams in DEMO-SL are kept simple; they have a limited set of shapes, symbols and constructs. What cannot be expressed in a diagram, must be expressed in a formal text. To illustrate the point: the graphical process modelling language BPMN 2.0 comprises over 100 symbols, and the graphical data modelling language ORM 2 several dozens. This makes it hard to keep up, both in producing diagrams and in reading them.

In Chap. 2, the basics of DEMO-SL are presented: the definition of terms, references, variables, assertions and assignments, the declaration and the derivation of types, and the ways in which time values are represented. The four aspect models in DEMO, thus the Cooperation Model (CM), the Action Model (AM), the Process Model (PM) and the Fact Model (FM) as discussed in [1], Chap. 12, are summarised in Sect. 2.6. Figs. 2.1 and 2.2 have (slightly) been adapted to be compliant with the EE Implementation Theory in [3]. In Chaps. 3 through 7, the various ways in which the aspect models can be expressed, are discussed. Appendix A contains the meta model or schema of the four aspect models, as well as the schema's of the diagrams and tables in which they are expressed. In appendix B, the graphical formalism of GOSL (cf. [1] Chap. 6) is included, which makes it easier to read this document. In appendix C, the syntax diagram is presented. It is an alternative way to formally express the syntax of DEMO-SL. Syntax diagrams are applied in Chap. 5.

## 2. The Basics of DEMO-SL

In this chapter, the vocabulary and the syntax of DEMO-SL are defined in the Extended Backus-Naur Form (EBNF), the international standard syntactic meta language, defined in ISO/IEC 14977. To improve readability, English words, like articles and prepositions are added, which make the logical formulas look like structured English sentences, quite unlike the common Peano-Russell notation. The added words are printed in **bold** in order to distinguish them clearly from the formal text. In Sect. 2.6, the four aspect models of DEMO are discussed.

In EBNF, names are put between double quotation marks. The symbol "|" stands for "exclusive or". The symbol "," means "followed by". The brackets "{" and "}" enclose an expression that may be repeated a number of times (including zero); the closing bracket "}-" means that there is at least one occurrence. The brackets "[" and "]" enclose an expression that is optional. The end of a definition is marked by ";". Comments are put between "%" and "%".

### 2.1 References, Variables, Assertions and Assignments

```ebnf
reserved term = coordination act name | coordination fact name | special term;

coordination act name = "request" | "promise" | "declare" | "accept" | "decline" | "reject" |
"revoke" | "allow" | "refuse";

coordination fact name = "requested" | "promised" | "declared" | "accepted" | "declined" |
"rejected" | "revoked" | "allowed" | "refused";

shorthand C-act/fact name = "rq" | "pm" | "da" | "ac" | "dc" | "rj" | "rv" | "al" | "rf"

special term =
"performer" |
"addressee" |
"et" % event time % |
"ot" % operative time; it may be preceded by a coordination fact name, like "requested" % |
"now" % at any time, the value of the variable now is the current time % |
"is" % 'a is b' means that the entity referred to by a is identical to the entity referred to by b; in
addition, "is" is used to indicate the assignment of an entity b to an entity variable a; "is" is also
used in expressing the perfect past tense of a verb, like in 'is completed'; % |
"is equal to" % 'u is equal to v' means that the value referred to by u is equal to the value referred to by v; in mathematical terms: u = v; it is also used to indicate the assignment of the value
v to the attribute variable u % |
"is less than" % 'u is less than v' means u < v % |
"is less than or equal to" % 'value u is less than or equal to v' means u ≤ v % |
"is greater than" % 'u is greater than v' means u > v % |
"is greater than or equal to" % 'u is greater than or equal to v' means u ≥ v % |
"is set of" % 'A is set of b' defines A as a set of (individuals or sets) b % |
"is in" % 'a is in A' means that the entity referred to by a is an element of the set A % |
"is within" % 'v is within V' means that the value v is within the value range V % |
"is before" % 's is before t' means that the time value s is earlier than the time value t % |
"is after" % 's is after t' means that the time value s is later than the time value t % |
"case" % 'case value reference is equal to value name: value name'; the use of the case construct will be explained in Sect. 2.3 %
```

#### Identifiers and Names

```ebnf
transaction kind id = "TK", {digit}-; 
% Examples: TK7, TK07 %

multiple transaction kind id = "MTK", {digit}-; 
% Examples: MTK2, MTK02 %

product kind id = "PK", {digit}-; 
% Examples: PK3, PK03 %

actor role id = "AR", {digit}-; 
% Examples: AR8, AR08 %

transactor role id = "TAR", {digit}-; 
% Examples: TAR17, TAR06 %

composite transactor role id = "CTAR", {digit}-; 
% Examples: CTAR01, CTAR1 %

entity name = {letter | digit}-; 
% Examples: John, 1089, Mary47 %

value name = {letter | digit}-; 
% Examples: sedan, 1021, 2272BP %

shorthand C-act kind id = "[" transaction kind id, "/", shorthand C-act/fact name, "]";
% Examples: [TK01/rq], [TK17/da] %

shorthand C-fact kind id = "(" transaction kind id, "/", shorthand C-act/fact name, ")";
% Examples: (TK01/rq), (TK17/da) %

transaction kind name = entity type name, present continuous tense of a verb (in lower case);
% Examples: rental completing, deposit paying %

multiple transaction kind name = noun or nominal phrase;
% Examples: persons facts, Library facts %

product kind name = "[", entity type name, "]", "is", event type name (in lower case);
% Examples: [rental] is completed, [rental] is deposit paid %

actor role name = entity type name, nominal form of a verb (in lower case);
% Examples: rental completer, deposit payer %

entity type name = noun or nominal phrase (in lower case);
% Examples: rental, deposit paid rental %

entity class name = noun or nominal phrase (in upper case);
% Examples: RENTAL, DEPOSIT PAID RENTAL %

value type name = noun or nominal phrase (in lower case);
% Examples: pizza kind, car group %

value class name = noun or nominal phrase (in upper case) between "{" and "}";
% Examples: {PIZZA KIND}, {CAR GROUP} %

property type name = noun or nominal phrase (in lower case);
% Examples: renter, pick-up branch %

attribute type name = noun or nominal phrase (in lower case);
% Examples: age, daily rental rate %

event type name = perfect tense of a verb (in lower case);
% Examples: completed, paid %
```

As discussed in the FI theory ([1] Chap. 5), the signifier of a conceptual thing can be a name, a noun or a sentence, depending on the kind of thing. Moreover, a name can be a proper name, like 'John' or 'John Smith' for a person, or an identifier like 'TK01' for a transaction kind, '2272BP' for a postal area, and '069684996' for a Dutch Citizen (the so-called BSN, similar to the SSN in the USA).

To avoid confusion, we put signifiers between single quotation marks, as we did above already. For example, we write "value type 'car group'" instead of "value type car group", and "car group 'sedan'" instead of "car group sedan".

#### Entity References

```ebnf
entity reference = definite entity reference | indefinite entity reference | indirect entity reference;

definite entity reference = entity type name, entity name;
% Examples: rental '1089', car '387462', citizen '069684996' %

indefinite entity reference = "a" | "an", entity type name;
% Examples: a person, an elephant %

indirect entity reference = ["the"], property type name, {"of" ["the"] entity reference }- ;
% Examples: renter of rental '1089',
the mother of the member of membership '387' %

entity variable = "[", entity type name , "]";
% Examples: [person], [car], [rental] %
```

#### Value References

```ebnf
value reference = definite value reference | indefinite value reference | indirect value reference;

definite value reference = value type name, value name;
% Examples: number '1089', day '2458270', car group 'sedan', year '2021' %

indefinite value reference = "a" | "an", value type name;
% Examples: a number, a day, an article group %

indirect value reference = ["the"], attribute type name, {"of" ["the"] entity reference | value
reference}- , ["within" ["the"], time reference];
% Examples: the weight of the car of rental '1089',
the daily rental rate of car group 'sedan' within the year '2021' %

value variable = "[", value type name , "]";
% Examples: [day], [car group] %

value range = "(", value reference, ",", value reference, ")"
% Examples: (1,10), (min amount, max amount) %
```

> **NOTE:** Value ranges only apply to values of the scale sorts Ordinal, Interval, Rational and Absolute (cf. Chap. 2.4).

#### Time References

Time values are a subclass of values. Because of their special role in (entity or value) references, they deserve special attention.

```ebnf
time type name = noun or nominal phrase (in lower case);
% Examples: day, year %

time class name = noun or nominal phrase (in upper case) between "{" and "}";
% Examples: {DAY}, {YEAR} %

time reference = definite time reference | indefinite time reference | indirect time reference;

definite time reference = time type name, time instance name;
% Examples: day '2458270', year '2000', week '34' %

indefinite time reference = "a" | "an", time type name;
% Examples: a day, a month, a week %

indirect time reference = "the" time type name, {"of" entity reference | value reference} |
"each" time type name, "within", time range;
% Examples: the year of the starting day of rental '1089',
the week of the ending day of rental '1089',
each day within (starting day of [rental], ending day of [rental]) %

time range = "(", time reference, ",", time reference, ")"
% Examples: (day '2458270', day '2458280'), (week '34', week '38') %
```

#### Property Variables and Assertions

```ebnf
property variable = "the", property type name, {"of", entity reference | property reference | value
reference | attribute reference }- , ["in" | "on", time reference];
% Examples: the renter of [rental],
the father of the renter of [rental],
the renter of a rental on day '2458270',
the month in which the car of rental '1089' is taken %

property assertion = property variable, "is" | "is not", property variable | entity reference;
% Examples: the renter of [rental] is the driver of [rental],
the driver of [rental] is not person '92637',
the father of the driver of [rental] is not person '92637' %
```

#### Attribute Variables and Assertions

```ebnf
attribute variable = "the", attribute type name, {"of", entity variable | property variable | value
variable | attribute variable}- , ["in" | "on", time reference];
% Examples: the age of [person],
the daily rental rate of [car group] in [year]
the deposit amount of a rental on day '2458270',
the penalty of a loan on the ending day of rental '1089' %

attribute assertion = attribute variable, "is equal to" | "is not equal to" | "is greater than" | "is
less than" | "is equal to or greater than" | "is equal to or less than" , attribute variable | definite
value reference;
% Examples: the ending day of [rental] is equal to or greater than
the starting day of [rental],
the number of free cars of the car group of [rental]
on each day within (the starting day of [rental],
the ending day of [rental]) is greater than the number '0' %
```

> **NOTE:** Attribute assertions can only apply to instances of value types (or scale types) of the sorts Ordinal, Interval, Rational and Absolute (cf. Chap. 2.4).

#### Boolean Expressions

```ebnf
boolean assertion = "(" property assertion | attribute assertion, ")";

boolean expression = boolean assertion, {"and" | "or", boolean assertion}-;
```

**Example:**
```
((the article kind of [sale] is 'alcoholic') and (the age of the customer of the [sale] on the day of
[sale] is equal to or greater than the minimal age of alcoholic drinks in the year of the [sale]))
or (the article kind of [sale] is not 'alcoholic')
```

> **NOTE:** By means of this expression, one checks whether the age of someone who wants to buy alcoholic drinks conforms to the legal minimal age.

The logical operators not, and and or have their common meanings. In order to avoid confusion about the order in which the parts of a boolean expression are evaluated, we use brackets in the example expression to separate the parts clearly.

#### Set Membership and Assignments

```ebnf
set membership assertion = (entity reference, "is [not] in", entity set reference) |
(value reference, "is [not] in", value set reference);

entity set reference = entity reference, where the referred entity is a set of entity reference;

value set reference = value reference, where the referred value is a set of value reference;
% Examples: person is in members
person is not in members
number is in even numbers %

property assignment = property variable, "is", property variable | entity reference;
% Examples: the renter of [rental] is the driver of [rental],
the renter of [rental] is a person,
the renter of [rental] is person '92637' %

attribute assignment = attribute variable, "is equal to" attribute variable | value reference;
% Examples: the amount of [sale] is equal to the total price of [sale],
the amount of [sale] is equal to an amount of money,
the amount of [sale] is equal to '24 euro' %

set members selection = "for each" entity reference | value reference "in" entity set reference |
value set reference ":"
% Example: for each [sale item] in [sale] : %
```

> **NOTE:** Assignments occur in with-clauses in the response part of an action rule (cf. Chap. 5).

### 2.2 Declaration of Types

Fact types (or types for short) can be specified graphically and textually, both on the schema level and on the meta schema level cf. [1] Chap. 6). The graphical specification is discussed in Chaps. 3 thru 6. Below, the textual specification is presented.

```ebnf
type declaration = entity type declaration | value type declaration | property type declaration |
attribute type declaration | event type declaration;

entity type declaration = "entity type", entity type name, "exists";
% Example: entity type 'rental' exists %

value type declaration = "value type", value type name, "exists";
% Example: value type 'car group' exists %

property type declaration = "property type", property type name, "exists";
% Example: property type 'renter' exists %

attribute type declaration = "attribute type", attribute type name, "exists";
% Example: attribute type 'starting day' exists %

event type declaration = "event type", event type name, "exists";
% Example: event type 'completed' exists %
```

### 2.3 Derivation of Types

Derived types can be specified graphically or textually. Examples of graphically specified derived types are provided in Chap. 6. Examples of textually specified derived fact types are provided below (the symbol "≡" must be read as "is defined as"). If the value of a derived fact is a choice out of a number of values, dependent on the current value of some variable, the case construct (known from programming languages) is used.

If the base type of the specified type is integer or real (cf. Sect. 2.4), the common arithmetic operations are applicable (like addition (plus), subtraction (minus) and multiplication (times)). If the base type is boolean, thus {true, false}, boolean expressions may be constructed by using the logical operators and, or and not.

#### Examples of specifications with arithmetic operations:

```
the rental charge of [rental] ≡ the duration of [rental] times the daily rental rate of the car group
of [rental] in the year of the starting day of [rental],

the duration of [rental] ≡ the ending day of [rental] minus the starting day of [rental] plus 1,

the actual duration of [rental] ≡ the day of the et of (car returning for [rental] is accepted) minus
the starting day of [rental] plus 1,

the late return penalty of [rental] ≡ (the actual duration of [rental] minus the duration of [rental])
times (the late return penalty in the year of the starting day of [rental])
```

#### Examples of a specification with choice:

```
the discount percentage of [sale] ≡
case customer kind of [sale] is equal to 'golden customer': 20
customer kind of [sale] is equal to 'silver customer': 10
customer kind of [sale] is equal to 'incidental customer': 0
```

### 2.4 Value Types - Dimensions, Units and Sorts

Values of variables, like the day of birth of a person, her/his length or weight, or the sort of a transaction kind (original, informational, documental or physical), are measurements on a scale. In measuring theory, these six scale sorts are commonly distinguished: Ordinal (O), Interval (I), Rational (R), Categorial (C), Absolute (A) and Boolean (B).

**Ordinal scales** have no zero point and no measuring unit, they are only orderings from less to more. A well-known example is the hardness of rocks: it is only possible to determine that the one rock is harder than an other rock.

**Interval scales** do have a measuring unit but no zero point. The measuring unit can be chosen freely. A well-known value type in this scale sort is temperature (Note, the temperature in degrees Kelvin does have a physical zero point but it is still considered an interval scale). Another example is time. Because of the very natural unit of a day, all calendars are based it.

**Rational scales** have also a freely choosable measuring unit but a fixed zero point. Well-known value types in this scale sort are length, surface, volume and velocity.

**Categorial scales** (also called nominal scales) are actually not measurement scales, because there is no measurement unit and no zero point. They are (basically arbitrary) distinctions. Examples are product categories in shops (like fruit, vegetables, dairy, etc.) and car groups in a car rental company (like sedan, mini, sports car, etc.).

The **Absolute scale** is actually not a measurement scale. It is just counting, like the number of apples in the basket and the number of persons in a car. Considered as a scale, it has a fixed zero point and a fixed measuring unit.

The **Boolean scale** consists of the two (logical) boolean values true and false.

In Table 2.1, the standard value types are presented. One can assume that they are always present. So, there is no need to define them explicitly in a DEMO model.

#### Table 2.1 Dimensions, units and sorts of value types

| value type | dimension | measuring unit | base type | scale sort |
|------------|-----------|----------------|-----------|------------|
| time | TIME | Julian day, hour, minute… | integer | I |
| duration | TIME | number of days, .. | integer | A |
| amount | MONEY | dollar ($), euro (€), … | real | R |
| mass | MASS | … kg, g, mg, … | real | R |
| length | LENGTH | … m, cm, mm, … | real | R |
| area | LENGTH² | … m², cm², mm², … | real | R |
| volume | LENGTH³ | … m³, cm³, mm³, … | real | R |
| velocity | LENGTH/TIME | … m/s, … | real | R |
| temperature | TEMPERATURE | °C, °F, K | real | I |
| number | NUMBER | < not applicable > | integer | A |
| truth value | BOOLEAN | < not applicable > | {true, false} | B |
| sort | SORTAL | < not applicable > | {O, I, D} | C |

Value classes are formulated as follows in BNF: `"{", dimension name, " : ", unit name, "}"`.

Examples are `{MONEY : euro}`, `{MONEY : €}`, `{TEMPERATURE : °C}`, `{TEMPERATURE : K}`. It is allowed to omit the unit, and thus to only indicate the dimension. For example: `amount {MONEY}`. It is also allowed to abbreviate `<dimension><unit>` to `<unit>` if no confusion can arise. Then, the unit is written in capitals. For example: `{JULIAN: day}` may be abbreviated to `{DAY}`. The value type 'sort' regards the sort of organisation according to the ALPHA theory (cf. [1] Chap. 11), so the distinction between the O-, I-, D- and M-organisation.

### 2.5 Representing Time Values

Time values, like the day of birth of a person and the starting day of a car rental, are measured on the Julian time scale. Next to this scale, time units from the Gregorian Calendar, like year and month, may be used. The conversion between the Julian scale and the Gregorian Calendar is based on the converter of the US Navy. So, in expressions like "the first day of the next month (from now)" and "the year of the starting day of [rental]", the values of month and year on the Gregorian Calendar are calculated by means of this converter. Note that the value of the universal variable 'now' is a value on the Julian time scale.

The preciseness with which time values are measured and represented depends on the situation at hand. Normally, the smallest unit is probably the second. For example, the Julian value of '30 April 2019 12:00 hours, 0 minutes and 0 seconds' is '2458604.000000'.

### 2.6 The Ontological Aspect Models

The essential model of an enterprise consists of the integrated whole of four ontological aspect models, each taking a specific view on the enterprise's O-organisation: the Cooperation Model, the Action Model, the Process Model and the Fact Model. The relationships between the four models is illustrated in Fig. 2.1. Instead of enterprise, we will use the notion of Scope of Interest (SoI). An SoI may be a part of an enterprise, but it may also comprise (parts of) several enterprises. Within an SoI, one may choose a focus; it is the part of the SoI of which one wants to produce the complete essential model.

The **Cooperation Model (CM)** of an SoI is a model of the cooperation between its actors (cf. [1] Chap. 10), or, following Chap. 9 in [1]), the construction of the SoI, i.e. of the transactor roles and the coordination structures among them.

The **Action Model (AM)** of an SoI is a model of its operation, i.e. the manifestation of the construction in the course of time (cf. [1] Chaps. 8 and 9). It comprises action rules and work instructions.

The **Process Model (PM)** of an SoI is a model of the (business) processes (consisting of transaction steps and process links between them) that take place as the effect of the activity of actors (cf. [1] Chap. 8). In systemic terms, it is a specification of the state space and the transition space of the coordination world (cf. [1] Chap. 9).
The **Fact Model (FM)** of an SoI is a model of the products (clusters of independent fact types and their dependent fact types) of the SoI that actors bring about (cf. [1] Chap. 8). It is a specification of the state space and the transition space of the production world (cf. [1] Chap. 9).

![Fig. 2.1 The integrated four DEMO aspect models]

As illustrated by the triangular shape in Fig. 2.1, and the division of this shape in the four aspect models, the CM and the AM cover both coordination and production, the PM regards only coordination and the FM only production. The PM connects the CM and the AM, as far as the coordination between actors is concerned. The FM does so as far as production is concerned. The AM constitutes the solid basis on which the other three models are firmly standing. As a matter of fact, the CM, PM and FM are already 'contained' in the AM, they only need to be 'extracted' from it. Lastly, there is nothing 'above' the CM. Figs. A.1, A.2 and A.3 contain the combined conceptual schemata of the CM, the AM and the PM, expressed in GOSL (cf. Appendix B). Fig. A.4 contains the meta schema of the FM. Every instance of the meta schema, so every FM, is itself a schema, namely of the production world of the modelled SoI (cf. [1] Chap. 6).

Fig. 2.2 presents the ways in which the aspect models are expressed, in diagrams, tables and formal textual expressions. The Bank Access Table (BAT) is an alternative way of expressing the interstriction structure (cf. Chap. 3). The other tables are so-called cross model tables: each of them represents a specific relationship between two aspect models. The set of cross-model tables is by no means exhaustive: one may freely define new ones if there is a need. The presented tables are just the ones that are commonly used in practice. In addition, alternative diagrams may be developed to express the four models. There are three tables that connect the ontological model of an SoI to its implementation model (cf. [3]): the ADT (Authorisation Delegation Table), the APT (Actor role Position Table), and the WIS (Work Instruction Specifications). They are added to the diagram in Fig. 2.2, for the sake of completeness.

![Fig. 2.2 Ways of expressing the four aspect models]

## 3. Expressing the Cooperation Model (CM)

### 3.1 The Coordination Structure Diagram

The Coordination Structure Diagram (CSD) is a graphical way of expressing the CM of an SoI. Its legend is exhibited in Figs. 3.1 and 3.2. The upper left part of Fig. 3.1 shows the elementary and the self-activating transactor roles. The shapes and constructs in the lower part of Fig. 3.1 are considered to be sufficiently explained in the figure. The constructs hold for each of the three sorts of organisations as distinguished in Chap. 11 of [1]: O-organisations, I-organisations, D-organisations, and M-organisations.

![Fig. 3.1 Legend of the Coordination Structure Diagram (1)]

![Fig. 3.2 Legend of the Coordination Structure Diagram (2)]

The focus within an SoI is indicated in a CSD by colouring the actor role shapes outside the focus light-grey. The transactor roles inside the focus are called internal, and the transactor roles outside are called environmental (if there is interaction with an internal actor role) or external otherwise (cf. [1] Chap. 9). There are three coordination structures among transactor roles: the interaction structure, the interstriction structure, and the interimpediment structure.

The **interaction structure** consists of initiator links, represented by solid lines from actor role shapes to transactions kind shapes. A cardinality range (k..n) may apply. Through this structure, trees of transactor roles emerge, as illustrated by Fig. 3.3. It is the CSD of the O-organisation of the GloLog enterprise (cf. [1] Chap. 18). By definition, the top of such an interaction tree is a self-activating transactor role (cf. [1] Chap. 10). The organisation of an SoI, often contains only subtrees of such trees. Then, the cut-off upper part is represented by a composite transactor role.

The **interimpediment structure** consists of wait links from transaction kinds to actor roles. A wait link expresses that actors in the connected actor role have to wait for a specific progress in transactions of the connected transaction kind before they can proceed their work (in their own transactions). In other words, the initiators or executors of these transactions impede actors in the connected actor role to carry on as long as the wait condition holds. A wait link is indicated by a dotted arrow from a transaction kind shape to the shape of the impeded actor role. The interimpediment structure constitutes the process dependencies among the corresponding transaction processes: the acts of the connected actors depend on the progress of the connected transaction processes.

If one abstracts from the realisation of the O-organisation of an SoI, and thus aims at producing its essential model (cf. [1] Chap. 11), a third coordination structure comes on the scene. This **interstriction structure** consists of access links from actor roles to transaction kinds, which are now conceived as transaction banks. Access links are the ontological abstraction of the sharing transaction kinds between the O-organisation and the I-organisation of the SoI (cf. [1] Chap. 11). An access link expresses that actors in the connected actor role have reading access to the contents of the transaction bank (both to the C-facts and to the P-facts). Access links are indicated by dashed lines between actor role shapes and transaction kind shapes. The interstriction structure constitutes the state dependencies among the corresponding transaction processes: the acts of the connected actors depend on the current state of the connected transaction processes, represented by the facts in the transaction bank. Actors have always access to the banks of transaction kinds in which they are initiator or executor.

The other transaction kinds between the O- and the I-organisation, so the remembering transaction kinds are abstracted from by considering the facts that are created by the initiator and the executor of a transaction to be stored in the transaction bank.

On the right side of Fig. 3.1, it is shown how external and environmental transactor roles are indicated, namely by colouring the shapes light-grey. The right side of Fig. 3.2 shows how external (multiple) transaction kinds are indicated. A multiple transaction kind is defined as a (non-empty) set of transaction kinds.

Fig. A.5 shows the fact types in the schema of the CM of which instances are expressed in a CSD. As an example, the CSD in Fig. 3.3 contains 18 transactor roles. Three of them are self-activating: TAR11, TAR12 and TAR13. There is one composite transactor role: CTAR01. The fourteen initiator links constitute the interaction structure. Next, there are four wait links: one from TK02 to AR10, one from TK03 to AR14, one from TK07 to AR15, and one from TK15 to AR17, together constituting the interimpediment structure. Lastly, there are three access links: one from AR11 to TK01, one from AR12 to TK03, and one from AR13 to TK14, together constituting the interstriction structure. Note that the access links to external information sources are omitted. Otherwise, there would have been many more access links.

![Fig. 3.3 The three coordination structures in the GloLog enterprise]

### 3.2 The Bank Access Table

A CSD may be supplemented by a Bank Access Table (BAT), as the alternative representation of the interstriction structure of an SoI. A BAT is particularly suitable if there are many access links, whose expressions in a CSD would lead to a mess of crossing dashed lines. Table 3.1 shows the BAT of the Library organisation (cf. [1] Chap. 16). A "U" (from Uses) indicates that there is an access link from the actor role (in the row) to the transaction bank (in the column). The access links from the executor and initiator roles to transaction kinds are indicated respectively by "Ex" and "In". As said, both the initiator and the executor of a transaction have access to the facts that are produced in transaction process of the transaction kinds in which they fill the initiator role or the executor role. Fig. A.11 shows the fact types of which instances are expressed in a BAT.

#### Table 3.1 BAT of the Library organisation

| Bank Actor | TK01 | TK02 | TK03 | TK04 | TK05 | TK06 | TK07 | TK08 | TK09 | MTK01 | MTK02 | MTK03 |
|------------|------|------|------|------|------|------|------|------|------|-------|-------|-------|
| AR01       | Ex   | In   | U    | U    | U    |      |      |      |      |       |       |       |
| AR02       |      |      | Ex   |      |      |      |      |      |      | U     |       |       |
| AR03       | U    |      |      | In   | In, Ex | U  | U    | U    |      |       |       |       |
| AR04       | U    |      |      |      | Ex   | U    | U    | U    | U    |       |       |       |
| AR05       | U    |      |      |      |      | In   | In, Ex | U  | U    |       |       |       |
| AR06       | U    | U    |      |      |      |      | Ex   | In   | In   | In    | U     | U     |
| AR07       |      |      |      |      |      |      |      | Ex   |      | U     |       |       |
| AR08       |      |      |      |      |      |      |      |      | Ex   | U     |       |       |
| AR09       |      |      |      |      |      |      |      |      | Ex   | U     |       |       |
| CTAR01     |      | In   |      |      |      |      |      |      | In   | U     |       |       |
| CTAR02     |      |      |      |      |      |      |      |      | In   | U     |       |       |

## 4. Expressing the Process Model (PM)

### 4.1 The Transaction Pattern Diagram

The Transaction Pattern Diagram (TPD) is the graphical way of expressing the structure of a transaction. The legend of the TPD is exhibited in Fig. 4.1. Fig. 4.2 contains the TPD of the Complete Transaction Pattern (CTP), as presented and discussed in [1], Chap. 8.

![Fig. 4.1 Legend of the Transaction Pattern Diagram (TPD)]

![Fig. 4.2 TPD of the complete transaction pattern (CTP)]

### 4.2 The Process Structure Diagram

The Process Structure Diagram (PSD) is the graphical way of expressing the structure of a business process kind. The legend of the PSD is exhibited in Fig. 4.3. It also shows the general shape of a transaction kind in a Process Structure Diagram (PSD). The sausage-like shape arises from stretching the disk shape horizontally. One must imagine that there is a (non-proportional) linear time axis from left to right. The sort of the shown transaction kind is original, indicated by the red diamond (cf. Fig. 4). As discussed in [1], Chap. 8, a transaction proceeds in three phases: the order phase (to the left of the diamond), the execution phase (the diamond), and the result phase (to the right of the diamond). The state "in" is the initial state of the transaction process; it is some state in some transaction process. The indicators of the other states, as well as the indicators of the presented C-acts, are arbitrarily chosen letters. In order to show that response links and wait links can apply both to the order phase and to the result phase, they are drawn on both sides of the diamond (u, v, w for the order phase, and x, y, z for the result phase). The P-act (TKi/ex, "ex" from "execute") is indicated by a grey-coloured small box.

In a PSD, only those C-act kinds and C-fact kinds are shown that are connected to other transaction processes by means of response links or wait links (cf. Fig. 4.3). The shapes of C-act kinds (the small boxes) that are performed by the initiator are drawn on top of the 'sausage', so within the responsibility area of the initiator, whereas the shapes of C-act kinds that are performed by the executor are drawn at the bottom, so within the responsibility area of the executor, as is the shape of the P-fact kind (the small grey box). In principle, the same rule holds for the shapes of C-fact kinds (the small disks). So, the shapes of C-fact kinds created by the initiator are drawn on the top of the 'sausage', and the shapes of C-fact kinds created by the executor are drawn at the bottom. However, to avoid that the drawing of response links and wait links become a mess, it is allowed to put the shapes of C-fact kinds on either side. For the same reason, one may duplicate the shapes of C-act and C-fact kinds. The states xx and yy represent states from which the revoke request or revoke promise, and the revoke declare or revoke accept are performed respectively.

![Fig. 4.3 Legend and general shape of the PSD]

The response links in Fig. 4.3 from C-fact kinds to (unspecified) C-act kinds are called initiation links. By definition, they start from the shape of a C-fact kind and end in the shape of the request act of some transaction kind. A C-fact kind may have several outgoing initiation links, meaning that transactions of several transaction kinds are initiated from it. Similarly, a C-fact kind may have several outgoing wait links. It means that the occurrence of an event of the C-fact kind is a wait condition for the performance of acts of several C-act kinds. Likewise, a P- or C-act kind may have several incoming wait links. It means that performing the act has to wait for the occurrence of all of these coordination events.

Cardinality ranges apply to response links and to wait links. A cardinality range k..n for a response link means that the C-act at the arrow side is performed a minimum number of times k and a maximum number of times n. The default value of k and n is 1; default values are commonly omitted in a PSD. Likewise, a cardinality range k..n for a wait link means that performing the C- or P-act at the arrow side is postponed until a minimum number of k and a maximum number of n C-events at the shaft side have occurred. The default value of k and n is again 1; default values are commonly omitted in a PSD. In order to illustrate the cardinality ranges in a PSD, Fig. 4.4 exhibits one of the PSDs from the case Rent-A-Car (cf. [1] Chap. 15).

![Fig. 4.4 PSD of the car transportation process in the case Rent-A-Car]
It shows in addition how self-activation is expressed in a PM, namely by a response link from the state requested (rq) to the act request [rq]. It means that the request for the next carrying out of a transaction TK07 is created immediately after the initiation of the current one. In this way, the self-activation of actor AR07 is not dependent on the carrying out of any of the enclosed transactions TK08. Fig. A.7 shows the fact types of which instances are expressed in a PSD.

In order to show precisely the connections to and from other transaction kinds, the PSD of an SoI may be supplemented by a number of Transaction Process Diagrams (TPD). An example of the use of a TPD in the case Volley is exhibited in Fig. 4.5. It shows precisely the connections between the transaction kinds TK01 and TK02. To save space, only the standard pattern of TK01 is shown. The connections between the patterns of transaction kinds TK01 and TK02 are indicated in orange. In response to the event (TK01/pm), the act [TK02/rq] is performed. The performing of the P-act [TK01/ex] has to wait for the occurrence of the C-event (TK02/ac).

![Fig. 4.5 The use of a TPD as a supplement to a PSD]
## 5. Expressing the Action Model (AM)

Action rules guide actors in responding to coordination events. In principle, there is an Action Rule Specification (ARS) for every combination of a coordination event kind (whose occurrences have to be responded to) and a specific wait condition (if applicable). As an example from the case Rent-A-Car (cf. [1] Chap. 15), the action rule specifications ARS-3, ARS-7 and ARS-9 all apply to the event kind TK01/pm, but with different additional while-conditions.

An ARS specifies the facts in the production world and/or the coordination world whose presence or absence in the current state of the world must be assessed, as well as the (production and/or coordination) acts that must be performed, depending on the outcome of the assessment. Action rules are imperative business rules that operationalise declarative business rules, which are the existence laws in the PM and the FM, thus the rules that determine the state space of the C- as well as the P-world of the SoI.

An action rule consists of three sequential parts: the event part, the assess part and the response part. As an example, Fig. 5.1 shows the specification of the action rule from the case Volley (cf. [1] Chap. 12), in which the request for membership starting is dealt with. The three parts are highlighted by background colours: cyan for the event part, magenta for the assess part, and yellow for the response part.

![Fig. 5.1 Example of an Action Rule Specification (ARS)]

Action rules are specified in Action Rule Specifications (ARSs). Figs. 5.2 through 5.5 contain the syntax diagrams that define the syntax of an ARS.

![Fig. 5.2 Syntax diagram of the event part of an action rule]

> **NOTE:** When a C-act is performed (in the response part of some action rule), a number of P-facts (possibly zero) are provided. In the given clause of an action rule, a selection of these P-facts are listed, namely those that are used in the assess part or the response part.

![Fig. 5.3 Syntax diagram of the assess part of an action rule (1)]

Assertions in the truth condition regard the state of the production world and/or the coordination world. The example in Fig. 5.1 regards the production world of the Volley organisation.

![Fig. 5.4 Syntax diagram of the assess part of an action rule (2)]

![Fig. 5.5 Syntax diagram of the response part of an action rule]

> **NOTE:** With "performer of C-event reference in when clause" in the last line in Fig. 5.5, we refer to the actor who has performed the C-act that resulted in the C-event in the when clause, as specified in Fig. 5.2. As said before, whether the response part of an action rule may contain the else clause, is determined by the CTP (cf. Fig. 4.2). It only occurs if the C-event in the when clause is a request, a declare, a revoke-request, a revoke-promise, a revoke-decline, a revoke-declare, a revoke-accept or a revoke-reject.

> **NOTE:** The expression * justification of [coordination act name] * is an (optional) informal account of the reason for performing the act. It is particularly interesting if the act is 'exceptional', like a decline and a reject.

## 6. Expressing the Fact Model (FM)

### 6.1 The Object Fact Diagram (OFD)

The Object Fact Diagram (OFD) is the graphical way to express the FM of an SoI. In order to understand the relationships between the schema level and the instance level of the conceptual model of a world, we start this chapter with presenting a few basic notions from mathematical set theory, notably the notion of (mathematical) function.

The common way of representing sets in set theory is the Venn Diagram. In such a diagram, the shape of a set is an oval; symbols within the oval represent elements of the set (cf. Fig. 11). The common way of representing functions (or binary relations in general) is to extend the Venn Diagram with connections between the elements of two (not necessarily different) sets. One set is called the domain of the function, the other one the range. A function maps the elements in the domain to the elements in the range. Fig. 6.1 exhibits an extended Venn Diagram, representing the function 'has as renter', with domain RENTAL and range PERSON.

![Fig. 6.1 Extended Venn diagram of a (mathematical) function]

The OFD is derived from this extended Venn Diagram: it consists of classes and of mappings between them. The classes are either entity classes or value classes. The shape of a class in an OFD is a roundangle (a contraction of "rounded rectangle"). The mappings between these classes represent property types or attribute types.

Property types are indicated by directed lines between entity classes. As an example in Fig. 6.2, the property type 'the renter of [rental] is [person]' is a function that maps the class RENTAL to the class PERSON. One should imagine that the line between the roundangles represents the set of connections between elements in RENTAL and elements in PERSON. The ">" indicates that RENTAL is the domain of the function and PERSON is the range.

Attribute types are indicated in a simpler way. The name of the attribute type is written in the roundangle of the (entity or value) class that is its domain. To the right of it, the name of the value class that is the range is written. To avoid confusion, the name of a value class is written between "{" and "}". The name of the class that is the domain of the attribute types and the list of attribute types, are separated by a dotted line in the roundangle of the domain.

![Fig. 6.2 OFD of the Rent-A-Car organisation]

Production event types are indicated by diamonds, the universal symbol of production (cf. [1] Chap. 8). They are expressed as a unary predicate concerning an entity class. For example, the event type '[rental] is completed' concerns the entity type rental (or the entity class RENTAL). An event type in the FM is identical to a product kind in the CM. Therefore, the numeral part of the product kind identifier (e.g. 01) is written in the diamond of the event type. The entity class that an event type concerns may be an aggregation of a number of entity types, like {CAR GROUP} * {YEAR} in Fig. 6.2.

Derived entity types can often be specified graphically. It is done in Fig. 6.2 for 'completed rental', in order to specify very precisely the property types and the attribute types: they are all functions with as domain the entity classes COMPLETED RENTAL. Standard value classes like DAY and MONEY are assumed to be implicitly present in every OFD (cf. Chap. 2.3). The value class YEAR is explicitly included in the OFD in Fig. 6.2 for specifying the attribute types that have YEAR as their domain.

![Fig. 6.3 part of the OFD of the GloLog organisation]

In Fig. 6.3, a part of the OFD of the GloLog organisation ([1] Chap. 18) is exhibited in order to show how sets can be specified graphically. The entity class SET OF SALE is graphically specified by drawing a roundangle around the roundangle of SALE. Conversely, every individual sale belongs to a purchase. Another example can be found in Fig. A.4.

An OFD also exhibits the existence laws that can conveniently be specified graphically (cf. [1] Chap. 6). For example, the OFD in Fig. 6.2 shows that the domain of the property type 'the renter of [rental] is [person]' is RENTAL and that the range is PERSON. In addition it shows that every rental has exactly one person as its renter, whereas a person can be renter in 0, 1 or more rentals. This follows from the (default) cardinality range.

External entity classes, like PERSON, are coloured light-grey. It means that persons are 'created' outside the focus of the SoI. But it must be possible to inspect their existence and to use their properties and attributes. All standard value classes are external, as discussed before, and thus also coloured light-grey. For the complete legend of the OFD, the reader is referred to [1] Sect. 6.3.3. Fig. A.4 presents the meta schema of the FM. As one may expect, it is identical to the general meta schema in conceptual modelling (cf. [1] Chap. 6). Fig. A.9 exhibits the fact types in the schema of the FM of which instances are expressed in an OFD.

### 6.2 Derived Fact Specification and Existence Law Specification

As said, derived fact types (of all kinds) that cannot be specified graphically, must be specified textually. In the case Volley ([1] Chap. 12), there are three attribute types that have to be specified textually. It is done in Fig. 6.4. Days are values in the Julian time dimension (cf. Table 1). So, the age of a person is expressed in the number of days that the person exists. If needed, it can be transformed to years in the Gregorian calendar or in any other calendar (cf. Chap. 2.4).

![Fig. 6.4 Derived Fact and Existence Law Specifications of the Volley organisation]

Fig. 6.4 also contains the existence laws that apply to Volley. Existence laws are the declarative counterparts of the (imperative) business rules or action rules that are discussed in Chap. 4. Action rules, or imperative business rules in general, are the operationalisation of declarative business rules, which are first order logical formulas concerning the production world of an SoI. Existence laws that cannot be specified graphically, must be specified as formal texts.

An example of such an existence law in the Volley organisation is that members must at least have the age of 12 years. This is formally expressed in Fig. 6.4 in the second existence law.

As discussed in [1], Chap. 12, the state space and the transition space of the coordination world of an SoI are fully determined by its PM. Moreover, the transition space of the production world of an SoI is fully determined by the transition space of the corresponding coordination world: a P-fact starts to exist at the time that the accept act in the corresponding transaction is performed.

## 7. Cross-Model Tables

Cross-Model Tables are tables that represent a specific relationship between two aspect models. In this chapter, we present and discuss the cross-model tables that are shown in Fig. 2.2. This set is by no means exhaustive: one may freely define new cross-model tables if need be.

### 7.1 The Transactor Product Table (TPT)

According to the OER method ([1] Chap. 12), the CSD of an SoI is mandatorily supplemented by a Transactor Product Table (TPT), for the sake of formulating product kinds formally and properly. A TPT is a table of transaction kinds with their corresponding product kinds and executing actor roles. It connects the CM and the FM of an SoI. The syntax of a TPT entry is specified as follows in EBNF:

```ebnf
TPT entry = (transaction kind id, transaction kind name), (product kind id, product kind formulation), (actor role id, actor role name);

product kind formulation= entity variable | property variable | attribute variable, "is", perfect tense verb;
```

Examples of product kind formulations are:
- `[rental] is contracted`
- `the car of [rental] is returned`
- `the fee of [membership] in [year] is paid`

Fig. A.10 shows the fact types in the schema of the CM of which instances are expressed in a TPT: the entity types 'transaction kind', 'product kind' and 'executing actor role', and the property types that determine the product kind of each transaction kind. Because the product kinds are identical to the P-event types in the FM, the TPT is called a cross-model table; it bridges the CM and the FM. Table 7.1 exhibits the TPT of the case Rent-A-Car (cf. [1] Chap. 15).

#### Table 7.1 TPT of the Rent-A-Car organisation

| transaction kind | product kind | executor role |
|------------------|--------------|---------------|
| TK01 rental completing | PK01 [rental] is completed | AR01 rental completer |
| TK02 car taking | PK02 the car of [rental] is taken | AR02 car taker |
| TK03 car returning | PK03 the car of [rental] is returned | AR03 car returner |
| TK04 deposit paying | PK04 the deposit of [rental] is paid | AR04 deposit payer |
| TK05 invoice paying | PK05 the invoice of [rental] is paid | AR05 invoice payer |

### 7.2 The Bank Contents Table (BCT)

A Bank Contents Table (BCT) connects the CM and the FM of an SoI. It shows the fact types of which instances are contained in the corresponding transaction banks. The order in which the fact types are listed is: entity class (if not already existing), the P-event type that concerns the class, corresponding property types and attribute types.

The syntax of a BCT entry is specified as follows in EBNF:

```ebnf
BCT entry = (transaction kind id, transaction kind name) | (multiple transaction bank id, multiple transaction bank name), (entity class name | product kind formulation | property variable | attribute variable);
```

#### Table 7.2 BCT of the Volley organisation

| Bank | Contents |
|------|----------|
| TK01 membership starting | MEMBERSHIP<br>[membership] is started<br>the member of [membership] is [person]<br>the payer of [membership] is [person]<br>the starting day of [membership] is [day] |
| TK02 fee paying | [fee] is paid<br>the membership of [fee] is [membership]<br>the year of [fee] is [year]<br>the amount of [fee] is [amount] |
| MTK01 persons facts | PERSON<br>the name of [person] is [name]<br>the day of birth of [person] is [day]<br>the gender of [person] is [gender] |

Table 7.2 exhibits the BCT of the case Volley (cf. [1] Chap. 12). The fact types are grouped according to the transaction banks in which their instances are stored. P-fact types whose instances are used within the SoI but created outside it, are also listed in the BCT. Because one commonly doesn't know the specific transaction kind in whose instances they are created, a multiple transaction bank is conceived. Fig. A.11 shows the fact types in the schema of the CM of which instances are expressed in a BCT: the entity types 'transaction kind', 'multiple transaction kind' and 'P-fact type,' and the property type that determines which facts are contained in which transaction bank.

### 7.3 The Create Use Table (CUT)

A Create Use Table (CUT) is a cross-model table that connects the PM and the FM. It shows in which transaction steps instances of the fact types in the FM are created and in which steps they are used. The contents of a CUT is fully determined by the AM of the considered SoI.

The syntax of a CUT entry is specified as follows in EBNF:

```ebnf
CUT entry = entity class | value class | P-fact type, C-act kind | "" | "" | "" , [C-fact kind];
```

As an example, Table 7.3 shows the CUT of the case Volley. All fact types, so entity types, value types, event types, property types and attribute types, that are specified in the FM, are listed in the first column of the table. In the second column one indicates the acts by which facts of the type in the left column are created. For fact types whose instances are contained in external transaction banks, the indication is "<given externally>". For fact types whose instances are provided as input values in the with-clause of the when-clause of an action rule concerning the C-event type in the third column, the indication in the second column is "<provided as input>". Derived fact types are indicated by "<derived>". They must be included in the Derived Fact Specifications, as part of the FM. In the third column one indicates the C-event type during the settlement of whose instances, facts of the type in the left column are used.

#### Table 7.3 CUT of the Volley organisation

| Fact Type | Created by | Used in |
|-----------|------------|---------|
| MEMBERSHIP | [TK01/rq] | |
| [membership] is started | [TK01/ac] | [TK02/rq] |
| the member of [membership] is [person] | <provided as input> | [TK01/pm] |
| the payer of [membership] is [person] | <provided as input> | [TK01/pm] |
| the starting day of [membership] is [day] | <provided as input> | [TK01/pm] |
| FEE | [TK02/rq] | |
| [fee] is paid | [TK02/ac] | |
| the membership of [fee] is [membership] | <provided as input> | [TK02/pm] |
| the year of [fee] is [year] | <provided as input> | [TK02/pm] |
| the amount of [fee] is [amount] | <derived> | [TK02/pm] |
| PERSON | <given externally> | |
| the name of [person] is [name] | <given externally> | [TK01/pm] |
| the day of birth of [person] is [day] | <given externally> | [TK01/pm] |
| the gender of [person] is [gender] | <given externally> | [TK01/pm] |
| the age of [person] is [number] | <derived> | [TK01/pm] |

Concerning the creation of entities, like memberships in the Volley organisation, some additional explanation is needed. A new instance of membership is created as soon as an act [TK01/rq] is performed (cf. [1] Chap. 8). It happens at the moment that the addressee of the act has understood the message up to the performa level (cf. [1] Fig. 8.5). It is the addressee who then creates a new membership, together with the properties and attributes that are provided as input: the member, the payer and the starting day. Note that no new membership is created when the request is performed as a consequence of settling a revoke; the membership then exists already, only some properties or attributes may change.

Fig. A.13 exhibits the fact types in the schema of the FM and the schema of the AM of which instances are expressed in a CUT.

## 8. Expressing the Implementation Design

DEMO-SL currently contains three ways of expressing the implementation design of the ontological model of an organisation. They are indicated in Fig. 2.2 (right side).

### 8.1 The Authorisation Delegation Table (ADT)

The Authorisation Delegation Table (ADT) connects the ontological model of an SoI with its implementation. It presents the assignment of tasks to (organisational) positions, in order to show precisely the delegations of authority (cf. [1] Chap. 8). The ADT is defined in Fig. A.14.

The columns of an ADT represent tasks (T); the task is to respond to the coordination event. The rows represent the positions (P) in the organisation. An "A" at the crossing of a column and a row indicates that somebody in the position is authorised to perform the task, a "D" that (the filler of the) position has delegated authority.

#### Table 8.1 ADT of the Pizzeria

| T/P | TK01/pm | TK02/da | TK03/pm | TK04/da |
|-----|---------|---------|---------|---------|
| customer | D | | | |
| order taker | A | A | A | A |
| baker | | | | |
| deliverer | | | D | D |

Table 8.1 exhibits the ADT of the Pizzeria organisation (cf. [1] Chap. 14). For logistic reasons, the order taker has to delegate the tasks in the ADT to people in the mentioned positions.

### 8.2 The Actor Role Position Table (APT)

The Actor Role Position Table (APT) connects the ontological model of an SoI with its implementation. It presents the assignment of actor roles to (organisational) positions. The definition of the APT is presented in Fig. A.14.

The columns of an APT represent actor roles. The rows represent the (organisational) positions that are distinguished in the organisation. An X in a cell means that the position (in the row) is assigned to the actor role (in the column). There may be multiple X's in a row or in a column.

#### Table 8.2 APT of the Pizzeria

| actor role / position | AR01 | AR02 | AR03 |
|-----------------------|------|------|------|
| desk officer | X | | |
| baker | | X | |
| deliverer | | | X |

Table 8.2 exhibits the APT of the Pizzeria organisation (cf. [1] Chap. 14). It expresses that persons in the position desk officer fill actor role AR01, persons in position baker fill actor role AR02 and persons in position deliverer fill actor role AR03.

### 8.3 The Work Instruction Specifications (WIS)

The Work Instruction Specifications (WIS) connect the ontological model of an SoI with its implementation. It presents the implementation of (ontological) production acts as well as (ontological) coordination acts as sequences of respectively production steps and coordination steps. The definition of the WIS is presented in Fig. A.16.

An example of the implementation of a (ontological) production act kind or P-act kind in a sequence of (technological) production step kinds or P-step kinds, is the 'translation' of the P-act kind [TK02/ex] from the exercise Pizzeria (cf. [1] Chap. 14 or [3] Chap. 12) into this sequence of P-step kinds:

```
< inspect the pizza kind of [sale] on the pink copy of [sale] >
< take a piece of dough that fits the pizza kind of [sale] >
< put the ingredients on the dough that belong to the pizza kind of [sale] >
< put the dough with the ingredients in the oven >
< wait the time needed, as indicated by the pizza kind of [sale] >
< retrieve the pizza from the oven >
< put the pizza in a fitting box >
< shift the box together with the pink copy of [sale] through the hatch to the order taker >
```

An example of the implementation of a (ontological) coordination act kind or C-act kind in a sequence of (technological) coordination step kinds or C-step kinds, is the 'translation' of the C-act kind [TK01/rq] from the exercise Pizzeria (cf. [1] Chap. 14 or [3] Chap. 12) into this sequence of C-step kinds (Note: we assume that the customer orders by telephone):

```
< take your smart phone >
< look up the telephone number of the Pizzeria >
< connect to the Pizzeria >
< tell your order to the order taker >
< end the connection >
< put away your smart phone >
```

## Appendix A

### Fig. A.11 Definition of the Bank Contents Table (BCT) 

![Fig. A.11 Definition of the Bank Contents Table (BCT)]

The purple coloured and bold-lined parts above collectively define the (semantic) contents of a Bank Contents Table (BCT). Thus, every BCT represents the existence, in the chosen SoI, of a number of transaction kinds, multiple transaction kinds, and P-fact types. In addition, it represents for every P-fact type in which transaction kind (now interpreted as a transaction bank) instances of it are contained.

The instances of the property type 'is part of' (between transaction kind and multiple transaction kind) may be implicitly given. It is important yet to understand that a multiple transaction kind is a collection of transaction kinds. Table 7.2 contains an example of a BCT.

### Fig. A.12 Definition of the Bank Access Table (BAT)

![Fig. A.12 Definition of the Bank Access Table (BAT)]

The purple coloured and bold-lined parts above collectively define the (semantic) contents of a Bank Access Table (BAT). Thus, a BAT represents the existence, in the chosen SoI, of transaction kinds, multiple transaction kinds, and actor roles, as well as of access links from actor roles to transaction banks, including the executor role and the initiator roles. To clarify this, the entity type 'composite actor role' is added to the schema (which can be fully deduced from the composite transactor role).

A BAT represents the interstriction structure of an SoI, as an alternative to drawing access links in the CSD. Access links may also exist between actor roles and multiple transaction kinds, and between composite actor roles and (multiple) transaction kinds. An example of a BAT is presented in Table 3.1.

### Fig. A.13 Definition of the Create Use Table (CUT)

![Fig. A.13 Definition of the Create Use Table (CUT)]

The purple coloured and bold-lined parts above collectively define the (semantic) contents of a Create Use Table (CUT). Thus, every CUT represents the existence, in the chosen SoI, of a number of transaction kind step kinds and P-fact types. In addition, it expresses for every P-fact type, in which transaction kind step kind its instances are created and in which transaction kind step kind its instances are used. Table 7.3 contains an example of a CUT.

### Fig. A.14 Definition of the Authorisation Delegation Table (ADT) 

![Fig. A.14 Definition of the Authorisation Delegation Table (ADT)]

The dark blue coloured and bold-lined parts above collectively define the (semantic) contents of the Authorisation Delegation Table (ADT). Note that the entity class POSITION is added to the schema, to make the definition possible.

The columns of an ADT represent tasks (T), where a task is to respond to the mentioned coordination event (TKSK). The rows represent the task performers (P), which are positions in the organisation. An "A" at the crossing of a column and a row indicates that somebody in the position is authorised to perform the task, a "D" that he/she has delegated authority.

### Fig. A.15 Definition of the Actor role Position Table (APT) - 

![Fig. A.15 Definition of the Actor role Position Table (APT)]

The dark blue coloured and bold-lined parts above collectively define the (semantic) contents of the Actor role Position Table (APT). Note that the entity class POSITION is added to the schema, to make the definition possible.

The columns of an APT represent actor roles (A). The rows represent the positions in the organisation (P). An "X" at the crossing of a column and a row indicates that somebody in the position is authorised to fill the actor role. Note that there may be multiple X's, both in a row and in a column.

### Fig. A.16 Definition of the Work Instruction Specifications (WIS) 

![Fig. A.16 Definition of the Work Instruction Specifications (WIS)]

The dark blue coloured and bold-lined parts above collectively define the (semantic) contents of the Work Instruction Specifications (WIS). Note that the entity class WORK INSTRUCTION is added to the schema, to make the definition possible.

A WIS specifies sequences of production steps and sequences of coordination steps that must be taken in order to perform respectively the ontological production act and the ontological coordination act that is implemented by the sequence.

## Appendix B - The graphical formalism of GOSL 

Appendix A assumes that the reader knows the graphical formalism of GOSL. This need not be the case for everyone. Therefore, we copy the relevant part of [1] Chap. 6 below. The textual formalism of GOSL is included already in Chap. 2 (The basics of DEMO-SL).

The graphical formalism of GOSL is based on the Venn diagram, as illustrated by Fig. B.1. There are two sets: RENTAL (with example elements r₁, r₂ and r₃) and PERSON (with example elements p₁, p₂, p₃ and p₄). The function renter is shown as a mapping from RENTAL to PERSON, which are respectively the domain and the range of renter. The expression renter(rᵢ) = pⱼ means that person pⱼ is the renter of rental rᵢ.

### Fig. B.1 Mathematical functions as mappings between sets

![Fig. B.1 Mathematical functions as mappings between sets](mathfuncmapping.jpg)

### Fig. B.2 Properties as mappings between entity classes

![Fig. B.2 Properties as mappings between entity classes](propmapping.jpg)

Fig. B.2 exhibits the more stylised way in which functional mappings are represented in GOSL. The roundangles represent entity classes, thus the extensions of entity types (cf. [1] Chap. 5). The functions are now called properties. One best considers the lines with an arrow in the middle as the bundles of separate mappings from elements in RENTAL to elements in PERSON (cf. Fig. B.1).

**Cardinality ranges are denoted as:**
- `<min>..<max>` 
- Examples: `0..1`, `1..1`, `0..*`, `1..*` ("*" means undetermined)

**The default ranges are:**
- `1..1` at the side of the range, meaning that every element in the domain is connected to exactly one element in the range
- `0..*` at the side of the domain, meaning that an element in the range need not be connected to an element in the domain, and if it does, it may be connected to many elements

Default cardinality ranges need not be indicated (they may be omitted).

The strings "0..*" and "1..1" denote the cardinality ranges that apply. The first number is the minimum cardinality and the second one the maximum cardinality. The symbol "*" (which can only occur as the maximum cardinality) means that the number is undetermined, i.e. any number larger than or equal to the minimum cardinality is allowed. The cardinality ranges in Fig. B.2 state that every rental has exactly one person as its renter (minimum 1 and maximum 1), and that every person is the renter of an arbitrary number of rentals (minimum 0 and maximum *). The ranges shown in Fig. B.2 are the default ones. They may be omitted, as is done e.g. in Fig. B.4.

### Fig. B.3 The notation and declaration of the distinct types 

![Fig. B.3 The notation and declaration of the distinct types](notationdeclaration.jpg)

Hereafter, the remainder of the graphical formalism of GOSL is presented in a number of figures. Fig. B.3 shows the graphical notation of the distinct types (entity, event, value, property and attribute) as well as the way in which they are entered into a conceptual schema, either by declaration or by derivation.

In terms of logic, entity types and event types are unary predicates, whereas property types and attribute types are binary predicates. To emphasise that a roundangle denotes a class, the class name is written in capitals. Next to every figure, the logical formulation is shown, in the well-known Peano-Russell Notation (PRN).

As mentioned in [1] Sect. 6.2.3, a conceptual schema of a world is a specification of its state space and its transition space. The state space of a world is determined first of all by the distinct sorts of facts (entities, events, properties and attributes) that may exist in a state of the world. In addition, it is determined by the applicable existence laws. Existence laws regulate the coexistence of facts. We distinguish three kinds of existence laws: reference laws, cardinality laws and exclusion laws.

Reference laws state which facts must exist together. They are shown in Fig. B.4. As an example, if the property type 'renter' exists, then its domain and its range must also exist. This is expressed in the figure by connecting the representation of the property renter with the representations of the classes RENTAL and PERSON. Like roundangles represent classes of entities (of a specific type), diamonds represent classes of events (of a specific type). An event is a unary predicate concerning an entity. As exemplified in Fig. B.4, the unary predicate 'concluded' holds for elements of the class RENTAL. If GOSL is used to model the production world of an organisation (cf. [1] Chap. 8), an event is the becoming existent of the independent fact of a product, as the result of a transaction. Events are thus elementary state changes (cf. [1] Chap. 9). As extensively discussed in [1] Chap. 8, a number of so-called dependent facts may start to exist together with an independent fact.

### Fig. B.4 The specification of reference laws 

![Fig. B.4 The specification of reference laws](referencelaw.jpg)

Attributes are a special kind of properties. The distinction is first, that the range of an attribute type is a value class, whereas the range of a (normal) property type is an entity class, and second, that both cardinality ranges are the default ones (cf. Fig. B.2). This allows for a more compact notation of attribute types, as shown in Fig. B.4 (bottom). The domain of the attribute group is the class RENTAL and the range is the extension of the value type car group.

**GRAPHICAL SPECIFICATION of REFERENCE LAWS**

| Element | PRN Notation |
|---------|--------------|
| concluded concerns rental | ∀x: concluded(x) ⇒ rental(x) |
| the domain of renter is rental | ∀x,y: renter(x,y) ⇒ rental(x) ∧ person(y) |
| the range of renter is person | |
| the domain of group is rental | ∀x,y: group(x,y) ⇒ rental(x) ∧ car_group(y) |
| the range of group is car group | |

### Fig. B.5 The specification of cardinality laws 

![Fig. B.5 The specification of cardinality laws](cardinalitylaw.jpg)

Cardinality laws provide a further specification of reference laws, by stating what their cardinality ranges are, as shown in Fig. B.5. As said, the default values (so "0..*" on the side of the domain and "1..1" on the side of the range) may be omitted, and therefore usually are omitted.

**GRAPHICAL SPECIFICATION of CARDINALITY LAWS**

| Relationship | Description | PRN Notation |
|-------------|-------------|--------------|
| renter (RENTAL to PERSON) | Every rental has exactly one person as its renter. Every person is renter of zero, one or more rentals. | ∀x,y: renter(x,y) ⇒ rental(x) ∧ person(y)<br>∀x,y,z: renter(x,y,) ∧ renter(x,z) ⇒ y=z<br>∀x ∈ RENTAL: ∃y ∈ PERSON: renter(x,y) |
| holder (DRIVING LICENSE to PERSON) | Every license is the driving license of exactly one person. Every person has zero or one driving licenses | ∀x,y: holder(x,y) ⇒ driving_license(x) ∧ person(y)<br>∀x,y,z: holder(x,y) ∧ holder(x,z) ⇒ y=z<br>∀x ∈ DRIVING_LICENSE: ∃y ∈ PERSON: holder(x,y)<br>∀x,y,z: holder(x,y) ∧ holder(z,y) ⇒ x=z |

### Fig. B.6 The specification of exclusion laws

![Fig. B.6 The specification of exclusion laws](exclusionlaw.jpg)

Exclusion laws serve to specify which facts cannot exist together, in addition to the restrictions that are already expressed in reference laws and cardinality laws. In other words, they state that the existence of a fact excludes the existence of one or more other facts. Fig. B.6 exhibits their graphical notation. We assume that the figure is self-explaining.

**GRAPHICAL SPECIFICATION of EXCLUSION LAWS**

| Relationship | Description | PRN Notation |
|-------------|-------------|--------------|
| STUDENT ⟂ EMPLOYEE | a thing cannot at the same time be a student and an employee | STUDENT ∩ EMPLOYEE = ∅ |
| owner ⟂ renter | a person cannot at the same time be the owner of a house and the renter of the (same) house | ∀x,y: owner(x,y,) ⇒ ¬ renter(x,y)<br>∀x,y: renter(x,y,) ⇒ ¬ owner(x,y) |

Like existence laws determine the set of lawful states of a world, occurrence laws determine which state transitions are lawful. Two kinds of occurrence laws are distinguished: precedence laws and preclusion laws. They are presented in Fig. B.7, which we assume is self-explaining. A precedence law states that an event of some type, concerning a particular entity, must always precede an event of some other type, concerning the same entity. A preclusion law states that an event of some type, concerning a particular entity, forbids the (future) occurrence of an event of some other type, concerning the same entity.

### Fig. B.7 The specification of occurrence laws

![Fig. B.7 The specification of occurrence laws](occurrencelaw.jpg)

**GRAPHICAL SPECIFICATION of OCCURRENCE LAWS**

| Law Type | Description |
|----------|-------------|
| PRECEDENCE LAW | for all memberships it holds that the occurrence of the event `<membership> is paid` precedes the occurrence of the event `<membership> is started` |
| EXCLUSION LAW | for all application it holds that the occurrence of the event `< application> is approved` excludes the occurrence of the event `< application> is disapproved` (and vice versa) |

Existence laws that cannot or not easily be specified graphically, must be specified textually in GOSL. Here are some, presumably self-explaining, examples of textual specifications (words between the brackets "[" and "]" denote variables):

- `[membership] is started on [day] implies that [day] is the first day of some [month] and that [month] is equal to or greater than the Current Month;`
- `[membership] is started on [day] implies that the age of the member of [membership] on [day] is equal to or greater than the minimum age in the year of [day];`

Next to introducing concept types in a conceptual schema by declaration, as explained above, one can introduce types by derivation, meaning that one defines a new type on the basis of existing types. In Fig. B.8 and Fig. B.9, the graphical specification of three kinds of derived types are shown: specialisation, generalisation and aggregation, in accordance with their definitions in the FI theory (cf. [1] Chap. 5).

### Fig. B.8 The specification of derived types (1)

![Fig. B.8 The specification of derived types (1)](derivedtypes.jpg)

Fig. B.8 (left side) exhibits an example of generalisation. It defines in a precise and complete way the derived type vehicle: a vehicle is either a car or a boat or an aircraft. As discussed in [1] Chap. 5, specialisation and generalisation are not each other's inverses. They are fundamentally different ways of constructing a type on the basis of one or more other types. The only invertible relationships between types is the subtype-supertype relationship. For example, student is a subtype of person, and thus is person = a supertype of student (cf. Fig. B.9). Likewise, boat is a subtype of vehicle and thus vehicle is a supertype of boat, etc.

On the right side of Fig. B.8, the notion of aggregation is explained. The derived concept offer could be useful for comparing the prices of a product (on a day) in different shops. The price would then be an attribute type of the entity type offer.

**GRAPHICAL SPECIFICATION of GENERALISATION and AGGREGATION**

| Type | Description | PRN Notation |
|------|-------------|--------------|
| VEHICLE (generalisation) | VEHICLE is a generalisation of CAR, BOAT and AIRCRAFT. This is indicated by the "+" sign in the triangle. | VEHICLE = CAR ∪ BOAT ∪ AIRCRAFT<br>∀x: vehicle(x) ⇒ car(x) ∨ boat(x) ∨ aircraft(x) |
| OFFER (aggregation) | OFFER is an aggregation of PRODUCT, SHOP and DAY. This is indicated by the "*" sign in the triangle | OFFER = PRODUCT * SHOP * DAY<br>OFFER = {(x, y, z)}: product(x) ∧ shop(y) ∧ day(z) |

### Fig. B.9 The specification of derived types (2) 

![Fig. B.9 The specification of derived types (2)](derivedtypes2.jpg)

The definition of the specialisation completed_rental in Fig. B.9 (right side) is comprehensive. The definition of the specialisation student (left side), however, needs to be complemented by a precise rule, e.g. that a student is a person for whom there is an admission in which this person is the applicant.

**GRAPHICAL SPECIFICATION of SPECIALISATION**

| Type | Description | PRN Notation |
|------|-------------|--------------|
| STUDENT | the entity type named "student" is a specialisation of the entity type named "person" | STUDENT ⊆ PERSON<br>NOTE. The derivation rule that determines whether a person is (also) a student, has to be provided yet |
| CONCLUDED RENTAL | the entity type named "concluded rental" is a specialisation of the entity type named "rental" | CONCLUDED_RENTAL ⊆ RENTAL<br>concluded_rental(x) ⇒ rental(x) ∧ concluded(x) |

Derived types which are not, or not completely, specified graphically, must be specified textually in GOSL. Here are some, presumably self-explaining, examples of textual specifications of derived types:

- `the age of [person] on Day = Day minus the day of birth of [person]`
 - *% Note that the age is expressed in Julian %*
- `the first fee of [membership] = (((12 minus the month of the starting day of [membership]) plus 1) divided by 12) times the annual fee in the year of the starting day of [membership]`

## Appendix C - The syntax diagram 

The syntax diagram is a graphical language for defining the syntax of a language in a formal way. Syntax diagrams are, for example, used to define the syntax of Pascal and CANDE¹⁰ ¹¹. We will use syntax diagrams particularly for defining the syntax of action rule specifications. They are presented in Fig. 26.

The easiest way to introduce syntax diagrams is by means of the example below. An arrow indicates the direction of reading. The bar at the far right side indicates the end of the definition.

According to the defined syntax, the following (not exhaustive) set of sentences can be produced:

- ROW THE BOAT GENTLY DOWN-STREAM
- ROW, ROW THE BOAT GENTLY DOWN-STREAM
- ROW, ROW, ROW THE BOAT GENTLY DOWN-STREAM
- ROW YOUR BOAT GENTLY DOWN-STREAM
- ROW THE BOAT DOWN-STREAM
- ROW THE BOAT GENTLY DOWN THE STREAM
- ROW THE BOAT GENTLY DOWN THE OLD STREAM
- ROW THE BOAT GENTLY DOWN - STREAM

## Abbreviations 

Hereafter, the most common abbreviations of terms in Enterprise Ontology are explained, in alphabetical order.

| Abbreviation | Full Term | Description |
|--------------|-----------|-------------|
| **ADT** | Authorisation Delegation Table | implementation form of the Action Model |
| **AM** | Action Model | aspect model of the ontological model of an organisational layer |
| **APT** | Actor role Position Table | implementation form of the Cooperation Model |
| **ARS** | Action Rule Specifications | representation form of the Action Model |
| **BAT** | Bank Access Table | representation form of the Cooperation Model |
| **BCT** | Bank Contents Table | cross-model representation form of the Cooperation Model and the Fact Model |
| **CM** | Cooperation Model | aspect model of the ontological model of an organisational layer |
| **CSD** | Coordination Structure Diagram | representation form of the Cooperation Model |
| **CUT** | Create Use Table | cross-model representation form of the Process Model and the Fact Model |
| **DFS** | Derived Fact Specifications | representation form of Fact Model |
| **FM** | Fact Model | aspect model of the ontological model of an organisational layer |
| **ICT** | Information and Communication Technology | It combines Information Technology (IT) for information processing and storage, and Communication Technology (CT) for transmitting information |
| **OFD** | Object Fact Diagram | representation form of Fact Model |
| **PM** | Process Model | aspect model of the ontological model of an organisational layer |
| **PSD** | Process Structure Diagram | representation form of the Process Model |
| **TPD** | Transaction Process Diagram | representation form of the Process Model |
| **TPT** | Transactor Product Table | cross-model representation form of the Cooperation Model and the Fact Model |
| **WIS** | Work Instruction Specifications | implementation form of the Action Model |

## References

1. Dietz, J.L.G., Mulder, J.B.F., Enterprise Ontology - a Human-Centric Approach to Understanding the Essence of Organisation. 2 ed. Enterprise Engineering. 2024: Springer Nature.
2. Sowa, J.F., Knowledge representation : logical, philosophical, and computational foundations. 2000, Pacific Grove: Brooks/Cole. xiv, 594 p.
3. Dietz, J.L.G., Mulder, J.B.F., Enterprise Design Fundamentals - settling the Enterprise Business and devising the Enterprise Organisation. Enterprise Engineering. 2025: Springer Nature.

## Endnotes

1. https://www.omg.org/spec/BPMN/2.0.2/PDF
2. http://www.orm.net/pdf/ORM2_TechReport1.pdf
3. https://en.wikipedia.org/wiki/Extended_Backus–Naur_form
4. https://www.cl.cam.ac.uk/~mgk25/iso-14977.pdf
5. https://en.wikipedia.org/wiki/Peano–Russell_notation
6. https://aa.usno.navy.mil/data/docs/JulianDate.php
7. "restriction" originates from the Latin verb "stringere", meaning trimming, curtailing. The word "interstriction" expresses that actors restrict each others decision freedom or 'play area'.
8. In [1], an OFD is included (Fig. 15.3) that differs from Fig. 6.2. It should be replaced by Fig. 6.2.
9. A roundangle is a rectangle with rounded corners
10. https://www.cs.rice.edu/~javaplt/311/Readings/CPSyntax.pdf
11. http://bitsavers.org/pdf/burroughs/B6500_6700/5000318_B6700_CANDE_Oct72.pdf
