# Deep Groove Ball Bearing - FreeCAD macro

Creates fully parametric, **3D-printable** deep groove ball bearings in PartDesign: the
inner and outer races, a snap-in cage and (optionally) the balls. Pick a circular edge -
the end of a shaft, a housing bore, or the bore of a part you want the bearing built
into - fill in the task panel while a live preview shows the bearing in place, done.
Every size can be changed later from a single place.

<img src="images/turntable.gif" width="420" alt="Bearing cutaway turning: races (blue), cage (orange), balls (red)">

Tested with FreeCAD 1.1.

## Demo

<img src="images/workflow.gif" width="860" alt="Select a hole edge, run the macro, pick 6808 and 4.5 mm balls, set 24 balls, OK: races and cage are built">

## Made for 3D printing

The bearings are designed to be printed. Races, cage and balls are separate bodies, so
each can be exported and printed on its own.

<p align="center">
  <img src="images/printed-parts.jpg" width="480" alt="Bearing parts from the macro and the printed bearing">
</p>

<p align="center">
  <img src="images/projects.jpg" width="480" alt="Simple projects using the printed bearings">
</p>

<p align="center">
  <img src="images/planetary-gearbox.jpg" width="640" alt="Planetary gearbox with a large printed output bearing: CAD view and printed part">
</p>

## Install and run

1. Copy `DeepGrooveBallBearing.FCMacro` into your macro folder
   (_Macro → Macros…_ shows its location).
2. Select one circular edge (or nothing, to build the bearing at the origin).
3. _Macro → Macros… → DeepGrooveBallBearing.FCMacro → Execute_.

## Task panel

The macro opens a task panel next to the 3D view, so you can still rotate and zoom while
you fill it in.

<img src="images/dialog.png" width="330" alt="The macro's task panel">

### Races

Where the races come from.

- **Groove selected body** - cut the ball groove into the PartDesign Body the edge belongs
  to; the body itself becomes the races, nothing new is added around it.
  - On a **bore**, the bore is the bearing's inner diameter: a thin inner race is split
    off and the rest of the body is the outer race, with the ball groove in it.
  - On an **outer surface**, it's the other way round: the outer race is split off and
    the body keeps the inner race groove.
  - A plain **ring** you modelled simply becomes the inner and outer race.

  The other diameter and the height set where the groove goes. The other diameter starts
  15 mm from the selected one (OD = bore + 15, or ID = outer surface − 15); the height is
  the length of the selected bore or surface.
- **Create races** - build a new ring with both races. The selected edge (on anything, e.g.
  the end of a shaft or a housing bore) sets the bearing's position and axis. The races,
  cage and balls go into one Part named after the bearing's size, OD x ID x Height, e.g.
  **Bearing 32x20x8**, or **Bearing 608 (22x8x7)** for a catalog size; move the Part to
  move the whole bearing. The other diameter starts 15 mm from the selected edge's and the
  height at 8 mm.

<img src="images/races-modes.png" width="560" alt="Races modes">

<img src="images/groove-body.png" width="600" alt="Grooving a part with a bore">

If the groove doesn't cut all the way through the body (e.g. the height is smaller than
the part), the macro warns you that the races aren't separate.

### Selected edge is

Whether the selected edge is the bearing's **inner diameter** or its **outer diameter**.
That diameter is taken from the edge and locked.

- _Groove selected body_: detected - a bore is the inner diameter, an outer surface the
  outer diameter.
- _Create races_: preset from the edge - the end of a shaft is the inner diameter, a
  housing bore the outer diameter - and you can change it.

### Catalog size

Prefills the inner diameter, outer diameter and height from a standard bearing (608, 625,
6204, MR105, R188, …). With a selected edge, only sizes matching its diameter are listed.
It shows **Custom** when the sizes don't match a catalog bearing. Not available when
grooving a body.

#### Supported bearings

176 deep groove ball bearing sizes, the same tables as in the Bearings workbench: ISO 15
boundary dimensions for series 60–69, common metric miniatures and inch R sizes (converted
to mm). Where a shielded (ZZ / 2RS) bearing is wider than the open one, both widths are
recognised (688 is 4 mm open, 5 mm as 688ZZ).

| Series | Sizes | Designations |
|---|---|---|
| 60 (deep groove, light) | 27 | 604, 605, 606, 607, 608, 609, 6000, 6001, 6002, 6003, 6004, 6005, 6006, 6007, 6008, 6009, 6010, 6011, 6012, 6013, 6014, 6015, 6016, 6017, 6018, 6019, 6020 |
| 62 (deep groove, medium) | 28 | 623, 624, 625, 626, 627, 628, 629, 6200, 6201, 6202, 6203, 6204, 6205, 6206, 6207, 6208, 6209, 6210, 6211, 6212, 6213, 6214, 6215, 6216, 6217, 6218, 6219, 6220 |
| 63 (deep groove, heavy) | 27 | 634, 635, 636, 637, 638, 639, 6300, 6301, 6302, 6303, 6304, 6305, 6306, 6307, 6308, 6309, 6310, 6311, 6312, 6313, 6314, 6315, 6316, 6317, 6318, 6319, 6320 |
| 68 / 618 (thin section) | 30 | 681, 682, 683, 684, 685, 686, 687, 688, 689, 6800, 6801, 6802, 6803, 6804, 6805, 6806, 6807, 6808, 6809, 6810, 6811, 6812, 6813, 6814, 6815, 6816, 6817, 6818, 6819, 6820 |
| 69 / 619 (thin section) | 30 | 691, 692, 693, 694, 695, 696, 697, 698, 699, 6900, 6901, 6902, 6903, 6904, 6905, 6906, 6907, 6908, 6909, 6910, 6911, 6912, 6913, 6914, 6915, 6916, 6917, 6918, 6919, 6920 |
| MR (metric miniature) | 15 | MR52, MR62, MR63, MR74, MR84, MR85, MR95, MR105, MR115, MR106, MR126, MR117, MR137, MR128, MR148 |
| R (inch) | 19 | R144, R2-5, R2-6, R2, R2A, R155, R156, R166, R3, R3A, R168, R188, R4, R4A, R1810, R6, R8, R10, R12 |

### Inner diameter, Outer diameter, Height, Ball diameter

- **Inner diameter** - bore of the inner race (the shaft size).
- **Outer diameter** - outside of the outer race (the housing bore size).
- **Height** - axial width of the bearing (_B_ in bearing catalogues).
- **Ball diameter** - the balls run on the pitch diameter, midway between ID and OD, and
  the gap between the two races is always half the ball diameter (a 4 mm ball gives a 2 mm
  gap). Must be smaller than the ring wall, (OD − ID) / 2, and than the height. Default
  4 mm; the status line tells you when it doesn't fit.
- **Ball preset** - common balls to buy for printed bearings: 3 mm, 1/8", 4 mm, 4.5 mm
  steel BB, 5 mm, 6 mm airsoft BB (measures 5.95 mm), 6 mm and 1/4". Picking one sets the
  ball diameter.

<img src="images/section.png" width="600" alt="Section with dimensions">

### Reverse direction

_Create races_ only: builds the bearing on the other side of the selected edge. It is
preset so the bearing goes _into_ a housing bore or _onto_ a shaft; tick or untick it to
build past the edge instead.

<img src="images/reverse.png" width="560" alt="Reverse direction">

### Number of balls

How many balls (and cage pockets) are spaced evenly around the bearing. The maximum
depends on ball size and pitch diameter; the macro tells you if it's too many.

<img src="images/num-balls.png" width="560" alt="Number of balls">

### Cage

Snap-in cage between the races that keeps the balls evenly spaced, built as a separate
**Cage** body. Untick the group to leave it out. The cage is drawn _seated_: shifted along
the axis until its pockets are centered on the balls, as it sits in a real bearing.

- **Cage thickness** - radial thickness of the cage ring. It sits in the gap between the
  races, so it can be at most half the ball diameter (2 mm for a 4 mm ball); anything
  less is running clearance. Default 1.5 mm.

  <img src="images/cage-thickness.png" width="520" alt="Cage thickness">

- **Cage top offset** - sets how tall the cage is: the cage reaches from the races' face to
  this distance short of where the race grooves meet the ball. Larger = shorter cage.

  <img src="images/cage-top-offset.png" width="520" alt="Cage top offset">

- **Pocket clearance** - extra diameter given to each ball pocket so the balls turn freely
  (pocket Ø = ball Ø + clearance).

  <img src="images/pocket-clearance.png" width="520" alt="Pocket clearance">

- **Pocket rise** - how far each pocket reaches past the cage's open edge. Smaller = the
  pocket mouth is narrower than the ball, so the balls snap in and are held.

  <img src="images/pocket-rise.png" width="520" alt="Pocket rise">

### Balls

**Create balls** (off by default) also models the balls as a separate **Balls** body.

<img src="images/cage-balls.png" width="640" alt="Cage and balls options">

### Show preview

While the panel is open, the 3D view shows the inner and outer diameter as labelled rings
on both faces (drawn on top, so you see them through the part) and a see-through view of
the races, balls and cage, in every mode, including when grooving a body. It is only a
preview: nothing is added to the document until OK. Untick it to hide it.

## Changing the bearing later

All values are stored on the **BearingParameters** datum inside the bearing's races Body
(_Races_ when created by the macro). Select it in the tree and edit the values in the
property editor; the races, cage and balls update. Each bearing has its own datum, so
several bearings can live in one document. With _Groove selected body_, the diameter taken
from the selected edge is read-only.

The size in the Part's name is set when the bearing is created; after changing ID, OD or
Height, rename the Part to match.

## AI disclosure

This macro and this README were created with the help of AI (Claude by
Anthropic). The design decisions, requirements and the reference model came from the
author; the code was written by the AI and tested in FreeCAD.
