---
title: "Project: Glucose Meter"
toc: true
toc-depth: 2
numbersections: true
colorlinks: true
abstract-title: Summary
abstract: |
  The Glucose Meter prototype is able to selectively determine concentrations of glucose in aqueous solutions using electrochemical methods because of the breakdown of glucose into gluconolactone and hydrogen peroxide, catalyzed by the enzyme glucose oxidase. The prototype utilizes IO Rodeo’s open source potentiostat to perform measurements but should be considered more advanced because of the enzyme immobilization. Builders will gain experience with chemical processes, electrochemistry, calibration, coding in python, and likely 3D printing.
  
  Further extensions could include in-situ mixing, flow cells, and continuous measurement as well as manual control of the potentiostat used for these measurements.

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
- **Tetraethyl orthosilicate (TEOS)** (50 mL minimum)
- **1750 MW Polyvinyl Alcohol (PVA)** (5 g minimum)
- **D-glucose** (1 g minimum)  
  - Beta form in particular is needed; this is a mixture of both forms, which works fine.
- **Glucose oxidase (GOx)** (0.1 g minimum)  
  - Experiments performed utilized GOx from Sigma-Aldrich, but GOx from Amazon was also tested and is a cheaper alternative.
- **200 proof ethanol** (10 mL minimum)
- **Hydrochloric acid (HCl)** – will be used as 0.1 M HCl (1 mL minimum)

---

## Hardware
- **IO Rodeo Rodeostat** (potentiostat)  
  Other potentiostats could work, but this one was chosen for its ability to program the functionality and acquire/work with the data directly. See section at the end of this page.
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

- **Glucose Oxidase Reaction:**  
  Glucose enzymatically reacts with oxygen to form **gluconolactone** and **hydrogen peroxide**.  
  - The enzyme used is **glucose oxidase (GOx)**.
  - This reaction specifically occurs for **beta-D-glucose**.
    
![Figure1 Glucometer](https://github.com/user-attachments/assets/2bb8fbd1-2b15-47e3-8577-0289a2ddf166)


- **Beta-D-Glucose Equilibration:**  
  - At room temperature, **D-glucose** takes approximately **12 hours** to equilibrate to the expected proportions of:
    - **Alpha (~36%)**
    - **Beta (~64%)**
  - Further details can be found in:  
    - [Wikipedia](https://en.wikipedia.org/wiki/Glucose_oxidase)  
    - A [detailed article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8946809/) (add source link here).

- **Detection Mechanism:**  
  - **Hydrogen peroxide** changes the conductivity of the solution and is detected by an electrode.
  - This device utilizes a **screen-printed carbon electrode**, but the process is adaptable to other systems as well.
  - The change in conductivity is measured as a **change in current** under a **constant potential** applied to the system.

- **Potentiostat Usage:**  
  - A potentiostat measures the current changes as glucose reacts with GOx and produces hydrogen peroxide.  
  - The applied potential typically ranges from **500–700 mV** (constant potential).  
  - A single value within this range is chosen for measurements.

# Procedure

## Functionalizing Carbon Screen-Printed Electrode (Silica Sol-Gel/PVA Method)

### Preparing Reagents, Solutions, and Chambers for Use
1. **0.1 M PBS solution with 0.1 M KCl:**
   - Add **2.34 g of NaH₂PO₄** and **15.13 g of Na₂HPO₄** to **1 L of water** alongside **7.45 g of KCl**.
   - Should dissolve readily with stirring alone.

2. **5% PVA solution:**
   - Dissolve **5 g of PVA (1750 MW)** in **95 mL of DI water**.
   - Note: Dissolution is difficult with standard stirring and heating but possible.  
     Autoclaving the solution leads to more rapid and effective dissolution.

3. **Glucose oxidase (GOx) suspension:**
   - Prepare at **50 units/μL** in DI water.
   - Note: Light ultrasonication is advised. To preserve GOx activity:
     - Freeze aliquots in a **-20°C freezer** and avoid repeated freeze-thaw cycles.
     - Recommend aliquots of ~15 μL (~1–2 uses, depending on electrodes prepared at ~3 μL/electrode).

4. **Prepare a makeshift desiccator (if unavailable):**
   - Fill ~10% of a container’s volume with **MgCl₂ (anhydrous)** or another hygroscopic salt.
   - Add a platform/drying area for electrodes (e.g., weight boats).

5. **Prepare silica sol-gel/PVA composite solution:**
   - Prepare silica sol-gel fresh every time:
     - Mix **0.725 mL of TEOS**, **0.35 mL of DI water**, and **25 μL of 0.1 M HCl** at room temperature for **1.5 h**.
     - Prevent overheating by replacing the sonicator’s water bath with room temperature or slightly cooler water every ~30 min.
   - If TEOS is hydrolyzed (causing phase separation), use this alternative method:
     - Add **1.4 mL of DI water** to a 20 mL beaker with a small stir bar.
     - Stir at high speed, add **0.13 mL of 0.1 M HCl**, **0.7 mL ethanol**, and **2.9 mL TEOS dropwise**.
     - Stir for **30 min** at high speed with no heating.

   - Mix aliquots of silica sol–gel (**25 μL**) and **5% PVA solution (100 μL)** ultrasonically for **60 seconds** to yield the silica sol–gel/PVA solution.

---

### Preparing Screen-Printed Carbon Electrodes (SCEs)
1. Rinse SCEs in **ethanol**, then dab dry with Kimwipes.
2. Rinse SCEs in **water**, then dab dry with Kimwipes.
3. Pre-treat SCEs with **0.1 M phosphate buffer with 0.1 M KCl** at **+1.7 V (vs SCE)** for **3 min**.

---

### Prepare Silica Sol-Gel/PVA/GOx Solution
1. Mix together **10 μL silica sol–gel/PVA solution** and **5 μL GOx suspension (50 U/μL)**.
2. Sonicate the mixture for **60 seconds** before use.
3. Spread **3 μL** of the solution onto the working electrode surface of the SCE.
4. Avoid spreading the solution on other parts of the electrode.

---

### Curing the Sol-Gel/PVA/GOx Solution
1. Place electrodes in a desiccator/drying chamber for **24 h**.
2. Further cure/dry at **37°C for 12 h**.
3. Rinse thoroughly in DI water (dip and dry with Kimwipes 2–3 times) prior to use.

---

### Storage
- Once fully cured, store electrodes in **0.05 M PBS with 0.05 M KCl** at **4°C**.

---

## Testing Glucose-Oxidase Coated Screen-Printed Electrodes
1. Prepare glucose solutions with varied concentrations (5–50 mg/mL).  
   - Allow glucose solutions to equilibrate for ~24 hours at room temperature for mutarotation (~64% β-D-glucose).
2. Connect SCEs to the potentiostat using alligator clips.
3. **Fully submerge all three electrodes** (reference, working, and counter) in the test liquid.

Schematic of Zimmer-Peacock SCE where RE is the reference electrode, WE is the working electrode, and CE is the counter electrode. The second image shows the SCE with alligator clips connected.

![Screenshot 2025-01-17 at 3 30 50 PM](https://github.com/user-attachments/assets/ed77da03-1df7-4622-ba0d-233cc5e18850)


---

### Electrochemical Testing Methods Suggested
1. **Cyclic Voltammetry (CV):**
   - Modulates the current over a range of potentials at a set scan rate.
   - Key parameters:
     - **Minimum potential:** -1000 mV
     - **Maximum potential:** +1000 mV
     - **Scan rate:** 50 mV/s
     - **Number of cycles:** 2–3

2. **Chronoamperometry:**
   - Applies a constant potential (e.g., 500 mV) after transitioning from 0 V.
   - Key parameters:
     - **Potential:** 500 mV
     - **Quiet time:** 1000 ms
     - **Run time:** 29,000 ms
     - **Sample period:** 10 ms

---

### Python Code Examples

#### Cyclic Voltammetry Example

```python
from potentiostat import Potentiostat
import matplotlib.pyplot as plt
import pandas as pd

port = '/dev/tty.usbmodem1301'       # Serial port for potentiostat device
datafile = 'Gluten_test1_CV_nf3_FeCN_0mgmL.txt'       # Enter the path that you want the datafile save time, curr, volt data

test_name = 'cyclic'        # The name of the test to run
curr_range = '100uA'        # The name of the current range [-100uA, +100uA]
sample_rate = 100.0         # The number of samples/second to collect

volt_min =  -0.2            # The minimum voltage in the waveform (V)
volt_max =  0.6             # The maximum voltage in the waveform (V)
volt_per_sec = 0.05         # The rate at which to transition from volt_min to volt_max (V/s)
num_cycles = 2              # The number of cycle in the waveform

# Convert parameters to amplitude, offset, period, phase shift for triangle waveform
amplitude = (volt_max - volt_min)/2.0            # Waveform peak amplitude (V) 
offset = (volt_max + volt_min)/2.0               # Waveform offset (V) 
period_ms = int(1000*4*amplitude/volt_per_sec)   # Waveform period in (ms)
shift = 0.0                                      # Waveform phase shift - expressed as [0,1] number
                                                 # 0 = no phase shift, 0.5 = 180 deg phase shift, etc.

# Create dictionary of waveform parameters for cyclic voltammetry test
test_param = {
        'quietValue' : 0.0,
        'quietTime'  : 0,
        'amplitude'  : amplitude,
        'offset'     : offset,
        'period'     : period_ms,
        'numCycles'  : num_cycles,
        'shift'      : shift,
        }

# Create potentiostat object and set current range, sample rate and test parameters
dev = Potentiostat(port)     
dev.set_curr_range(curr_range)   
dev.set_sample_rate(sample_rate)
dev.set_param(test_name,test_param)

# Run cyclic voltammetry test
#t,volt,curr = dev.run_test(test_name,display='pbar',filename=datafile)
t,volt,curr = dev.run_test(test_name,display='data',filename=datafile)

# Assuming the above are lists, make a dict
d = {'time_s': t, 'voltage_V': volt, 'current_uA': curr}

# Convert to pandas dataframe
df = pd.DataFrame(data = d)

# Save to working directory
df.to_csv(r'./Gluten_test1_CV_nf3_FeCN_0mgmL.csv')

# plot results using matplotlib
plt.figure(1)
plt.subplot(211)
plt.plot(t,volt)
plt.ylabel('potential (V)')
plt.grid('on')

plt.subplot(212)
plt.plot(t,curr)
plt.ylabel('current (uA)')
plt.xlabel('time (sec)')
plt.grid('on')

plt.figure(2)
plt.plot(volt,curr)
plt.xlabel('potential (V)')
plt.ylabel('current (uA)')
plt.grid('on')

plt.show()
```

#### Chronoamperometry Example

```python
from potentiostat import Potentiostat
import matplotlib.pyplot as plt
import pandas as pd

port = '/dev/tty.usbmodem1301'    
datafile = 'glucose_test_E20A_50_mM_Test1.txt'    

dev = Potentiostat(port)
dev.set_curr_range('100uA')
dev.set_sample_period(10)

name = 'chronoamp'
test_param = {
        'quietValue' : 0.0,
        'quietTime'  : 1000,
        'step'       : [ 
            (0,0.0),     # Step 1 (duration ms, voltage) 
            (29000,0.5), # Step 2 (duration ms, voltage)
            ],
        }

dev.set_param(name,test_param)
t,volt,curr = dev.run_test(name,display='pbar',filename=datafile)

# Assuming the above are lists, make a dict
d = {'time_s': t, 'voltage_V': volt, 'current_uA': curr}

# Convert to pandas dataframe
df = pd.DataFrame(data = d)

# Save to working directory
df.to_csv(r'./glucose_test_E20A_50_mM_Test1.csv')

plt.subplot(211)
plt.title('Voltage and current vs time')
plt.plot(t,volt)
plt.ylabel('potential (V)')
plt.ylim(0,max(volt)*1.1)
plt.grid('on')

plt.subplot(212)
plt.plot(t,curr)
plt.ylabel('current (uA)')
plt.xlabel('time (sec)')
plt.grid('on')

plt.show()
```

---

# Troubleshooting

### **I’m not getting a signal or getting a poor signal during chronoamperometry**
Possible causes and solutions:
1. **Improper alligator clip positioning:**  
   Ensure clips are correctly positioned on the working/counter/reference electrode. At least one metal tooth from the clip should touch the silver portion at the top of the SCE.
2. **Alligator clips touching each other:**  
   This can cause signal malfunctions or damage the SCE. Ensure clips are properly spaced and not in contact.
3. **Incomplete electrode submersion:**  
   Make sure all three electrodes (counter, reference, and working) are fully submerged in the liquid containing the analyte.
4. **Fried SCE:**  
   Check for visual "burn" marks, particularly on the counter electrode.
5. **Liquid in the wrong areas of the SCE:**  
   Dry the SCE and alligator clips thoroughly before use.
6. **GOx washing off the electrode:**  
   Ensure the silica sol-gel/PVA/GOx is properly cured. Extend drying times to **36 h** in the drying chamber followed by **16 h at 37°C**.

---

### **The silica sol-gel/PVA/GOx is washing off my electrode**
This issue may arise from:
- **Improper curing:**  
  Extend drying durations during both initial and elevated temperature curing steps.
- **Overheating during sonication:**  
  Keep the water bath cool during sonication. Replace water periodically or use ice to prevent the sol-gel from gelling prematurely.
- **Old or hydrolyzed TEOS:**  
  Always prepare fresh silica sol-gel and ensure TEOS isn’t hydrolyzed.

---

### **I can’t get the TEOS to mix with DI water**
If TEOS is hydrolyzed:
- Verify its appearance. Hydrolyzed TEOS will appear translucent or opaque and won’t flow freely.
- Use ethanol and follow this order of addition:
  1. DI water
  2. 0.1 M HCl
  3. Ethanol
  4. TEOS (add dropwise)
- Mix vigorously for 30 min before sonication.

---

# Alternative Options and Project Considerations
With all of these options, make sure you discuss with Dr. Osuji and the TA before you proceed.
### **Project Additions for Students**
1. **In-Situ Mixing:**  
   - Utilize peristaltic pumps to mix high-concentration glucose solutions with solvents (PBS, water, etc.) directly in a chamber for measurements.
   - Advanced: Add the ability to rinse/wash between runs.

2. **Continuous Measurement:**  
   - Use manual control to record continuous, real-time data instead of pre-formatted potentiostat functions.

3. **Flow Cell:**  
   - Create a setup with continuous glucose solution flow for dynamic testing. Combine with in-situ mixing and continuous measurement for more complex experiments.

4. **Electrode Housing:**  
   - Design custom housings for SCEs to ensure consistent placement and proper alignment of alligator clips.
   - Two examples of housing/custom glassware for standard electrodes from Pine Research (Sources [A](https://pineresearch.com/shop/products/cells-and-glassware/low-volume-cells/complete-low-volume-kits/glassy-carbon-working/) and [B](https://pineresearch.com/shop/products/cells-and-glassware/standard-volume/three-electrode-utili-shaft-e/))

---

### **Electrochemical Additions**
1. **Platinum Electrodes/Systems:**  
   - Use screen-printed platinum electrodes or platinum-plated mesh for enhanced conductivity and sensitivity.
   - Example adaptation:
     - Clean platinum strips with dilute nitric acid, rinse with DI water, and dry.
     - Coat with **50 μL of enzyme solution** (glucose oxidase in BSA buffer) mixed with **20 μL of 2.5% glutaraldehyde solution** for crosslinking.
     - Cure and store in phosphate buffer at 4°C when not in use.

---

### **Non-Electrochemical Options**
1. **Colorimetric Assays:**
   - Example: GOx-HRP system with a 4-APP+phenol colorimetric reaction to produce a purple-colored product proportional to glucose concentration.  
     - **Reference:** [PubMed Article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5713636/)
   - Limitation: Not reusable and requires precise setup for reliable results.

2. **Refractometer Analysis:**  
   - Measure refractive index differences as a function of glucose concentration.  
   - Limitation: Less reliable than electrochemical methods.

---

### Additional References
1. **Platinum Electrode Techniques:**  
   Immobilization methods for glucose oxidase on platinum electrodes using glutaraldehyde.
2. **Enzyme-Coated Strips:**  
   Example adaptation for immobilization on platinum screen-printed electrodes.

---

# References and Additional Sources

This is a non-traditional numbered list of references, functioning as a collection of sources used to build the project with brief descriptions. Inline sources mentioned above are generally not repeated here. For more detailed electrochemistry knowledge, consult the knowledge bases from [**Pine Research**](https://pineresearch.com/shop/kb/), [**Zimmer Peacock**](https://www.zimmerpeacocktech.com/knowledge-base/), and [**PalmSens**](https://www.palmsens.com/knowledgebase/).

---

1. [**Chronoamperometry Using Commercial Glucose Sensors from IO Rodeo**](https://blog.iorodeo.com/chronoamperometry-with-glucose-test-strips/)  
   - Excellent starting point with information on using commercial sensors to determine glucose concentrations.
   - Includes expected results, trends, and instructions, as well as applications like detecting glucose in beverages.

2. [**Enzymatic Determination of Glucose from Pine Research**](https://pineresearch.com/shop/kb/applications/laboratory-exercises/electrochemical-enzymatic-determination/)  
   - Great background on determining glucose concentrations using Pine Research materials.
   - Good electrochemistry background and a strong starting point.

3. [**Silica Sol-Gel-Based Glucose Sensor Using Carbon SCE**](https://www.sciencedirect.com/science/article/pii/S0925400508002311)
   - Primary source for the methods developed above, heavily modified and expanded upon.
   - Procedures are vague and missing key aspects but could be helpful for students.
   - Tests are more advanced and include custom-made SCEs.

4. [**Open-Source Glucose Meter**](https://hackaday.io/project/11719-open-source-arduino-blood-glucose-meter-shield)  
   - Arduino-based project with a detailed parts list and instructions.
   - Uses purchased electrodes from OneTouch glucose sensors.
   - Great information, background, and inspiration for expanding this project.

5. [**Hackaday Glucometer Resources**](https://hackaday.com/tag/glucometer/)  
   - Provides concepts for working with electrochemistry and building glucose sensors.

6. [**Glucose Sensor Immobilizing GOx with BSA and Glutaraldehyde**](https://www.sciencedirect.com/science/article/abs/pii/0956566391870198)  
   - Describes an alternative method for immobilizing GOx on electrodes.
   - Includes details on CV scanning range, rates, and solution preparation.

7. [**Glucose Sensor via Enzyme Membrane on Platinum Net**](https://analyticalsciencejournals.onlinelibrary.wiley.com/doi/pdf/10.1002/bit.260350115)  
   - Method for functionalizing macroscopic glucose sensors with detailed procedures and expected results.

8. [**Glucose Sensing in Solution**](https://www.youtube.com/watch?v=ESCEXPHxU-8&t=197s)  
   - Similar approach to glucose sensing using GOx and platinum mesh.  
   - Good proof of concept for simpler methods.

9. [**Article About Designing Biosensors**](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2771472/)  
   - Overview of design aspects and considerations for biosensors.
   - Includes protective barrier/membrane considerations to exclude other antioxidants from glucose measurement.

10. [**Review Article on SPEs for Biosensors**](https://link.springer.com/article/10.1007/s00604-014-1181-1#Sec27)  
    - Covers various uses of biosensors and approaches with SPEs, including functionalization schemes, detection ranges, and electrolytes.

11. [**Review Article on Electrochemical Biosensors and Architectures**](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3663003/)  
    - Discusses approaches to creating and using electrochemical biosensors.  
    - Includes detailed explanations of different electrochemical tests.

12. [**Perspective Article on Directions/Unaddressed Areas of Glucose Sensing**](https://pubs.acs.org/doi/epdf/10.1021/acs.analchem.6b03151)  
    - Focused on future directions and advances in glucose sensing, particularly for patient-connected devices.
    - Valuable for informing design choices.

13. [**Continuous Monitoring and Control Inspiration**](https://www.bioprocessintl.com/sponsored-content/automated-process-control-based-on-in-situ-measured-glucose-concentration)  
    - Primarily uses commercial products but could inspire control schemes for continuous monitoring projects.

14. [**Positive Control: Pre-Functionalized Glucose SCE**](https://metrohm-dropsens.com/products/electrodes/modified-screen-printed-electrodes/screen-printed-electrodes-for-glucose-detection/)  
    - An option for a positive control to validate solutions and results.

---

# Potentiostat Compatible with Arduino

Reading the voltage difference between the **working electrode (WE)** and **reference electrode (RE)** is most accurately performed using a **potentiostat**. Unlike relying on the Arduino's VRef, a potentiostat dynamically maintains the voltage difference between the WE and RE, ensuring precise electrochemical measurements. A **counter electrode (CE)** completes the circuit by balancing the current generated by reactions at the WE.

## Recommended Potentiostat
The best solution identified is offered by **IO Rodeo**, which provides:
- **Open-source hardware**: Fully customizable and modifiable for specific experimental needs.
- **Associated software**: Includes pre-written scripts and documentation for easy integration with various electrochemical methods.
- **Arduino compatibility**: Easily interfaces with Arduino for data acquisition and control.

### Why IO Rodeo?
- Open-source design allows users to modify and extend the functionality.
- Affordable compared to other potentiostat options, making it ideal for educational and research purposes.
- Comprehensive support and documentation make it accessible for both beginners and advanced users.

**[IO Rodeo Website](https://iorodeo.com/)**

