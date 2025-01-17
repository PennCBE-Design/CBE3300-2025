---
title: "Project: Protein Detection"
toc: true
toc-depth: 2
numbersections: true
colorlinks: true
abstract-title: Summary
abstract: |
  The Protein Detector prototype is able to selectively determine concentrations of gluten in solution using electrochemical methods thanks to the selective detection of gluten by conjugated gluten-specific antibodies. The method can be generalized to many types of protein/antibody combinations. The prototype utilizes IO Rodeo’s open source potentiostat to perform measurements but should be considered relatively more advanced because of the conjugation strategy. Builders will gain experience with chemical processes, electrochemistry, calibration, coding in python, and likely 3D printing.

  Further extensions could include continuous measurement, varying parameters, determination of consistency, testing of complex mixtures, as well as manual control of the potentiostat for measurements.

  Approximate time: 35 person-blocks.
  (1 block = 1.5 hrs)

header-includes:
#   - \usepackage{draftwatermark}
  - \usepackage{xurl}
---


# Components

## Consumables
> **Note:** Many of these items (chemicals in particular) are available from several vendors – these are mostly from Sigma-Aldrich, arbitrarily.

- **Zimmer Peacock hyper value carbon screen-printed electrodes** (10 count minimum, recommend at least 30)  
  Other companies have these as well and are interchangeable.
- **1-Pyrenebutyric acid N-hydroxysuccinimide ester (PANHS)** (1 g minimum)
- **Anti-gliadin antibodies** (25 µL minimum at 1 mg/mL)  
  This is interchangeable with almost any other antibody/antigen pair for detection. Gluten was chosen since it can be detected in complex foods/mixtures, is a relevant allergen whose antibody can be readily obtained, and whose antigen (gliadin from gluten) is easily obtainable as well.
- **Potassium ferrocyanide tri-hydrate** (5 g minimum)  
  Hydrate isn’t necessary but was the available compound at the time of ordering.
- **Potassium ferricyanide** (4 g minimum)
- **Bovine serum albumin** (2 mL minimum at 22%)
- **Phosphate-buffered saline (PBS)** (~100 mL minimum)  
  Could also be made if necessary, using the formula [here](https://en.wikipedia.org/wiki/Phosphate-buffered_saline), but PBS is fairly cheap anyway.
- **Gluten from wheat** (1 g minimum, recommend 5 g to be safe)
- **Dimethyl sulfoxide (DMSO)** (5 mL minimum)  
  - Solvent to dissolve your protein/antigen.
  - Gluten is soluble in DMSO at ~20–40 mg/mL.
- **Sulfuric acid** (5 mL minimum)
- **Potassium chloride** (5 g minimum)

---

## Hardware
- **IO Rodeo Rodeostat** (potentiostat)  
  Other potentiostats could work, but this one was chosen for its ability to program the functionality and acquire/work with the data directly.
- **Personal computer** with USB 2 or 3 connection available.

---

## Software

### Python
- Code is written in Python to operate the potentiostat, but it is also usable via a web app or a program installed on your computer.  
  Instructions: [Rodeostat Installation](https://blog.iorodeo.com/rodeostat-software/).

#### Python Installation Instructions for Mac
1. Use the Terminal application to help with the installation of some packages and software.
2. **VS Code**:  
   - Part text editor, part IDE, part terminal, part content management system, part PDF viewer, part browser substitute.  
   - Download link: [Visual Studio Code](https://code.visualstudio.com/download).
3. **Git**:  
   - Check if Git is installed by typing the following in the terminal:  
     ```bash
     git
     ```
   - If Git isn’t installed, follow the installation process: [Git Installation](https://git-scm.com/downloads).
4. **Miniconda**:  
   Miniconda will be the environment manager for Python. Install it using the command line in the terminal (make sure you run these line by line):  
   ```bash
   mkdir -p ~/miniconda3
   curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
   bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
   rm -rf ~/miniconda3/miniconda.sh
   ```
   Then:
   ```bash
   ~/miniconda3/bin/conda init bash
   ~/miniconda3/bin/conda init zsh
   ```
# Key Working Principles

- **π-π Stacking Interaction:**  
  Utilizes π-π stacking between the carbon electrode and **1-Pyrenebutyric acid N-hydroxysuccinimide ester (PANHS)**.  
  - PANHS also contains an NHS-ester group that can be used for conjugation.

- **Conjugation Chemistry:**  
  This scheme should work with most antibodies since the conjugation chemistry is based on the presence of amine groups.  
  More details can be found [here](https://www.thermofisher.com/us/en/home/life-science/protein-biology/protein-biology-learning-center/protein-biology-resource-library/pierce-protein-methods/amine-reactive-crosslinker-chemistry.html).

![Screenshot 2025-01-17 at 2 38 38 PM](https://github.com/user-attachments/assets/7bc0ec1d-6964-4138-bb4e-13cba19010c5)


- **Specific Binding and Detection:**  
  - The conjugated antibodies will recognize and specifically bind to a protein/analyte of interest.  
  - This binding causes a measurable change in the electrochemical signal.

- **Detection Method:**  
  The signal change is detected using an electrochemical method referred to as **square wave voltammetry (SWV)**.  
  - SWV is described in more detail in **Section 3.2**.
