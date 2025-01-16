---
title: CBE 3300 Quickref
subtitle: A working doc
toc: true
colorlinks: true
---

<!-- Resources for 

x- Device fabrication
x- Computer control of instruments
- Lab safety
x- Intellectual property
x- Market research
x- Instrumentation
- Mechanical design
    - CAD
    - 3D printing
    - Dremel/Drill
    - Plumbing
x- Suppliers
x- Project management
    x- QbD
    x- Design Controls
-->

\newpage

# Software

## Get software you use on computers you normally don't

- https://portableapps.com/

## Python

Environment management:

- venv
- Anaconda/Miniconda

Handy libraries:

- pyserial
- matplotlib
- numpy
- pandas
- plotly
- jupyter

## Open Source

Open source can mean different things to different people. At its core, it means that you have access to view the source code of software that runs on your computer. It _may not_ mean that you can get it for free or that you can copy and use it for free -- or at all. It all depends on the license.

Common licenses:

- MIT
- GNU General Public License (GPL v2, v3, AGPL, LGPL)
- Mozilla Public License (MPL)
- Apache
- BSD

Note that this is different from Creative Commons licensing. Bottom line: before you use something you find on the internet, check its license terms. If there isn't a license, you cannot assume that it's available for use, but you can ask the author to license it.

Links:

- https://choosealicense.com/
- https://opensource.org/
- https://creativecommons.org/

# Intellectual property

**Terms:** prior art, freedom to operate, licensing, patent, copyright, disclosure

Technologies available for license from Penn:  
https://upenn.technologypublisher.com/

Other links:

- https://pci.upenn.edu/inventors/how-it-works-commercializing-innovation/
- https://pci.upenn.edu/partners/licensing/

# Market Research

Steve Blank (https://steveblank.com/slides/)  

- Business model canvas
- Get out of the building
- Lean Startup

# Instrumentation

## Communications terms you may hear

- Analog
- Digital
- Serial
- UART
- RS 232
- RS 485
- Modbus
- I2C
- 4-20 mA
- Current loop
- TX/RX
- SPI

## Hands-on activities
- Mini project: Temperature Control Unit
- Mini project: Differential Pressure Transmitter

## Electrochemistry

- https://pineresearch.com/
- https://www.zimmerpeacock.com/

# Technical drawing

- MIT OpenCourseware  
https://ocw.mit.edu/courses/2-007-design-and-manufacturing-i-spring-2009/pages/related-resources/drawing_and_sketching/
- NASA  
https://s3vi.ndc.nasa.gov/ssri-kb/static/resources/Engineering+Working+Drawing+Basics.pdf
- Autodesk Fusion360 online exercises  
https://help.autodesk.com/view/fusion360/ENU/courses/AP-DRAW-TUT-INTRODUCTION
- On-demand manufacturing tutorials: Xometry
    - https://www.xometry.com/resources/design-guides/technical-drawing-best-practices/
    - https://xometry.pro/en/articles/prepare-technical-drawing/

# Mechanical design and fabrication

## Techniques and Tools

- Plastic forming
    - https://www.youtube.com/watch?v=Dxy9CepxhjI
- 3D printing
- CNC
- Lathe
- Mill
- Laser cutter
- Plotter
- Router
- Welding
- It's a list as long as time

## Design for Additive Manufacturing (DfAM)

- https://www.hubs.com/get/3d-printing-guide/
- https://www.hubs.com/knowledge-base/design-for-3d-printing/
- https://www.hubs.com/get/3d-printing-design-rules/

## CAD options

There are many options for CAD software. Implementation strategies differ, but at the end of the day, math is math. Pick one, learn it, and use it until you find something that you like better or makes it easier to solve the problem at hand.

If you've never used Fusion360 before, it's a good place to start.

- Solidworks
- Autodesk Inventor
- Autodesk AutoCAD
- Autodesk Fusion360*
- SketchUp
- Tinkercad
- Catia
- PTC Creo
- Rhinoceros
- Blender (not strictly CAD)
- Alibre
- Ondsel
- Onshape
- FreeCAD
- OpenSCAD
- [pycsg](https://github.com/timknip/pycsg)
- [CadQuery](https://github.com/CadQuery/cadquery)


## Bambu

- BambuStudio Slicer (based on Prusa Slicer, Slic3r): 
  - https://wiki.bambulab.com/en/software/bambu-studio/studio-quick-start
  - https://wiki.bambulab.com/en/x1/manual/introduction-to-bambu-studio  (seems to be an older docs page)
- Wiki for Bambu P1S Printer: 
    - https://wiki.bambulab.com/en/p1
- [Bambu Lab X1 CARBON - Graphic User Interface WALKTHROUGH](https://www.youtube.com/watch?v=3LQCO8PTMxc)
- [Bambu Lab X1 CARBON SLICER - All You Need To Know To Start Using BAMBU STUDIO](https://www.youtube.com/watch?v=Svt4yl7JiZ4)
- Having issues like an offset first layer? Try using OrcaSlicer. It's based on Bambu and Prusa slicers, so you can use it in the same way.  
    [**https://github.com/SoftFever/OrcaSlicer**](https://github.com/SoftFever/OrcaSlicer)

# Suppliers

- McMaster (https://www.mcmaster.com/)
    - Industrial
    - Fast shipping
    - CAD models for spacing, visualization
- Grainger (https://www.grainger.com/)
    - Industrial
- Sparkfun (https://www.sparkfun.com/)
    - Electronics
    - Beginner-friendly
- Adafruit (https://www.adafruit.com/)
    - Electronics
    - Beginner friendly
- Digikey (https://www.digikey.com/)
    - Electronics components
- Thorlabs (https://www.thorlabs.com/)
    - Optics

# Project management

- Basecamp Shape Up (https://basecamp.com/shapeup)
- Asana (https://asana.com/)
- Lean, Six Sigma
- 5S
- Kaizen
- Quality by Design (QbD)
- Design controls (https://www.fda.gov/media/116762/download)

# Other resources

## Course/Education material

- https://fab.cba.mit.edu/classes/865.21/topics/metrology/02_measurements.html
- https://docs.google.com/presentation/d/11ycsc3yQMaL4N5c4obK24_Zhd7gYJszxpyjLKYNrRwo/edit#slide=id.geb73ec9ed9_0_38

## Instrumentation

- https://wiki.epfl.ch/carplat/documents/LowLevMsHandbk.pdf

## Arduino

- https://www.gammon.com.au/adc