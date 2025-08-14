# DEMO-SL change board

## Constitution
- The DEMO-SL change board is constituted by the EEI management
- Changes in members of the board are decided by the EEI management
- The board consists of at least three (3) members and preferably has an uneven number of members
- The board preferably reflects a diverse (global) geographic background
- Board members have a deep pratical experience (at least 3 years) with DEMO, and preferably have experience with
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
3. **Intake**
4. **Investigation**
5. **Public consultation** (optional)
6. **Feedback**
7. **Decision and publication**

2. intake: change board checkt op ingediende change aan de formele criteria voldoet;
   op basis daarvan terugkoppeling aan indiener met indicatie voor tijdlijn change-afhandeling
   streven is 8 weken maximaal
3. onderzoek: ⁠uitvoering beoordeling door changeboard,
   leidend tot gezamenlijk voorstel
   - wel/niet akkoord, al dan niet met amendementen
   - resultaat is mogelijk een voorstel voor wel/niet openbare consultatie geadviseerd & waarom
   - het gezamenlijke voorstel kan overigens een meerderheids- of minderheidsstandpunt omvattten
   overwegingscriteria o.a.:
   - aansluiting op eerdere versies (legacy-consequenties)
   - aansluiting op andere standaarden (o.a. past dit bij scope van het domein, of zijn daar ook al andere standaarden voor)
   - voor- en nadelen voor diverse doelgroepen
4. ⁠indien er sprake is van een openbare consultatie (optioneel):
   alle belanghebbenden (b.v. modelleurs, architecten, tool-ontwikkelaars, repositorybeheerders, …) kunnen reageren,
   onder opgave van hun belang, hun standpunt en de onderbouwing daarvan.
   - feedback tijd is beperkt tot max 4 weken.
5. ⁠terugkoppeling : EEi-changeboard koppelt de resultaten van expertteam + openbare consultatie terug naar indiener als hoor- en wederhoor;
   - dit kan leiden tot aanpassingen van het change-voorstel (en in het uiterste geval tot herhaling van enkele voorgaande stappen vanaf stap 3)
6. ⁠resultaat: EEi-changeboard beslist en voert aanpassingen door en publiceert dit op github (waarop belanghebbenden zich kunnen abonneren).

Te bepalen:
- versienummering keuze


Inspiratiebron: https://www.forumstandaardisatie.nl/sites/default/files/BFS/3-lijsten/standaarden-aanmelden/toetsen/Toetsingsprocedure-en-criteria-22_0.pdf , vooral de inhoudelijke criteria.
