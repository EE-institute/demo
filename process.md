# DEMO-SL change board

DEMO-SL is the Specification Language for the Design and Engineering Methodology for Organizations, as described in [Enterprise Ontology
A Human-Centric Approach to Understanding the Essence of Organisation by Jan Dietz and Hans Mulder (2024)](https://link.springer.com/book/10.1007/978-3-031-53361-7)

## Constitution
- The DEMO-SL change board is constituted by the EEI management
- Changes in members of the board are decided by the EEI management
- The board consists of at least three (3) members and preferably has an uneven number of members
- The board preferably reflects a diverse (global) geographic background
- Board members have a deep practical experience (at least 3 years) with DEMO, and preferably have experience with
  + enterprise modeling, meta modeling and language specification, and/or
  + translating requirements into (IT) solutions
 
## Decision making
- Decision making is done by a simple majority vote. In case of a tie, the board can ask advice from external experts or can ask the EEI management to take a decision.
- There should be at least three (3) votes for a decision to be valid.
- A member has no vote in the decision about adopting a change request submitted by that board member. In case of too few votes, external experts can be temporarily added to the board. All experts should still comply to the rules as stated above.
- [ ] TODO: beslissingsbevoegdheid en aanstellingsregels van het EEi-bestuur

## Scope
- Ontological parts of DEMO that require (meta)specification
- The scope of this board can only be changed with approval of the EEI management
- Current standards: DEMO-SL, GO(-)SL
- [ ] Any part outside of this scope will be processed separately - t.b.d.

## Change request process
1. **Submission**
  The submitter defines the desired change through an issue ticket on [this Github](https://github.com/EE-institute/demo/issues), stating at least:
  - The parts that are impacted by the change (GOSL, syntax, aspects, visuals, examples, other)
  - Why the change is needed or what the added value is of the change
  - [ ] Intended domain; TODO: beoogd domein (b.v. inrichtingsonafhankelijk modelleren van essentie, of implementatie van organisaties modelleren of …) onderbouwt dat met minstens 1 uitgewerkt voorbeeld (oud versus nieuw)
  - [ ] Optional: any relevant documentation regarding practical and/or scientific validation of the change request; TODO gedocumenteerde praktijkervaring van een ander dan de indiener + aanbevelingen / wensen voor het change-proces
2. **Intake**
  The change board checks whether the change request complies with the formal criteria (stated above) and will communicatie an indicative timeline for processing the change request, aimed at a maximum of 8 weeks.
3. **Investigation**
  The change board will investigate the change request and check, a.o.,
  - Connection with older versions
  - Connection with other standards
  - Impact for different users of the standard
  The change board can also decide for a public consultation, or to opt for a partial acceptance
4. **Public consultation** (optional)
  Every stakeholder (DEMO modeler, architects, tool developers, etc.) can respond, stating their interest and their argumented perspective on the change request.
  There will be at most 4 weeks to respond.
5. **Feedback**
  The change board will communicate the results of the investigation and possibly of the public consultation, to enable the `right of reply'. Such a 'discussion' may lead to a change in the original change request, and in extreme cases may lead to reverting the process to the investigation step (3).
6. **Decision and publication**
  The board finalizes the decision and publishes the decision. In case of a (partial) adoption, a new version of the standard will be published, to which stakeholders can subscribe.

## Versioning
- [ ] t.b.d.

## Resten, to be removed
3. onderzoek: ⁠uitvoering beoordeling door changeboard,
   leidend tot gezamenlijk voorstel
   - wel/niet akkoord, al dan niet met amendementen
   - resultaat is mogelijk een voorstel voor wel/niet openbare consultatie geadviseerd & waarom
   - het gezamenlijke voorstel kan overigens een meerderheids- of minderheidsstandpunt omvattten

Inspiratiebron: https://www.forumstandaardisatie.nl/sites/default/files/BFS/3-lijsten/standaarden-aanmelden/toetsen/Toetsingsprocedure-en-criteria-22_0.pdf , vooral de inhoudelijke criteria.
