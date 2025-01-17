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
  - SWV is described in more detail in **Testing Anti-Gliadin Conjugated Screen-Printed Electrodes**.

# Procedure

## Functionalizing Carbon Screen-Printed Electrode (NHS-Ester Chemistry)

### Preparing Reagents, Solutions, and Chambers
1. **0.5% BSA in PBS:**
   - Dilute **0.5 mL of 22% BSA** in salt solution to **22 mL** with PBS.
   - Store at **4°C** and prepare in a sterile manner to prevent bacterial growth. Alternatively, filter with a **0.2 µm filter** as needed.

2. **2 mM PANHS in Methanol:**
   - Add **133 mL of methanol** to a 250 mL beaker. Stir rapidly (~8 on a heating plate) and heat gently (~2–3 on the plate, below 50°C).
   - Measure **0.102 g of PANHS (MW: 385.41 g/mol)** and dissolve in methanol within 15 minutes of stirring. Ultrasonication may aid dissolution.

3. **Anti-Gliadin Antibodies in PBS (20 µg/mL):**
   - Dilute **5 µL of antibodies (1 mg/mL)** into **245 µL of PBS**.
   - Store in aliquots to avoid freeze-thaw cycles. Use ~3 µL per electrode, making **25 µL** sufficient for two sets of electrodes.

4. **Wheat Gluten Standard Curve in DMSO/PBS:**
   - Dissolve **80 mg of wheat gluten** in **4 mL of DMSO** with stirring and gentle heating (~60°C).
   - Ultrasonicate for 15 minutes after dissolution. For higher concentration, add an additional **80 mg** to achieve **40 mg/mL**.

5. **Ferro/Ferricyanate Solution:**
   - Prepare **100 mL of DI water** in a 250 mL beaker. Add:
     - **0.7455 g of KCl**
     - **0.42239 g of K₄[Fe(CN)₆]·3H₂O**
     - **0.32924 g of K₃[Fe(CN)₆]**
   - Stir rapidly until fully dissolved (~10 minutes).

6. **Wet Chamber:**
   - Create a humid chamber by adding water to the bottom of a container.
   - Place a platform (e.g., weight boat) and a small beaker of water in the chamber to maintain humidity.

---

### Conjugating Detection Antibody to the Electrode
1. **Prepare Electrodes:**
   - Rinse SCEs with ethanol, PBS, and DI water. Dry after each rinse with Kimwipes.

2. **Coat Electrodes:**
   - Incubate electrodes in **2 mM PANHS** in methanol for **4 hours at 4°C** in a wet chamber.

3. **Antibody Conjugation:**
   - Rinse electrodes with PBS and DI water, then dry.
   - Add **3 µL of antibodies (20 µg/mL)** onto each electrode.
   - Incubate for **4 hours at 4°C** (or overnight if desired).

4. **Blocking Non-Specific Binding:**
   - Incubate electrodes in **0.5% BSA in PBS** for at least **2 hours at 4°C**. Longer durations (up to 36 hours) are also successful.

5. **Storage:**
   - Store electrodes in **PBS at 4°C** or dry them and store at **-20°C**.

---

## Testing Anti-Gliadin Conjugated Screen-Printed Electrodes

1. Prepare gluten solutions (e.g., **0.05–2 mg/mL**).  
   - Incubate electrodes with gluten solutions for **1 hour at room temperature**.
2. Rinse electrodes in PBS and DI water. Dry before submerging into the ferro/ferricyanate solution.
3. Connect electrodes to a potentiostat using alligator clips. **Ensure proper connection to the reference, working, and counter electrodes by fully submerging them**.

Schematic of Zimmer-Peacock SCE where RE is the reference electrode, WE is the working electrode, and CE is the counter electrode. The second image shows the SCE with alligator clips connected.

![Screenshot 2025-01-17 at 3 30 50 PM](https://github.com/user-attachments/assets/ed77da03-1df7-4622-ba0d-233cc5e18850)

---

### Electrochemical Testing Methods Suggested
1. **Cyclic Voltammetry (CV):**
   - Modulates the current over a range of potentials at a set scan rate.
   - Key parameters:
     - **Minimum potential:** -200 mV
     - **Maximum potential:** +600 mV
     - **Scan rate:** 50 mV/s
     - **Number of cycles:** 2

2. **Square Wave Voltammetry (SWV):**
   - Square wave voltammetry (SWV) applies a series of potential steps with small changes followed by short holds, generating a waveform that slowly changes the potential while measuring the resulting current.
   - The potential range should include the **oxidation potential peak** observed from cyclic voltammetry (CV).
   - Key parameters:
     - **Starting Potential:** 0.45 V
     - **Ending Potential:** -0.15 V
     - **Quiet Time:** 100 ms
     - **Quiet Potential:** 0.45 V
     - **Amplitude:** 50 mV (25 mV recommended, but 50 mV yielded better signals)
     - **Step Voltage:** 0.00075 V
       *(Note: Adjusting this step voltage corrects a timing issue in some potentiostat firmware versions.)*
     - **Averaging Window:** 0.05
       *(Lower values result in less averaging and more precise signals. 0.1 also works effectively.)*

---

### Example Python Code

#### Cyclic Voltammetry Example

```python
from potentiostat import Potentiostat
import matplotlib.pyplot as plt
import pandas as pd

port = '/dev/tty.usbmodem1301'       # Serial port for potentiostat device
datafile = 'Gluten_test1_CV_1.0mgmL.txt'       # Enter the path that you want the datafile save time, curr, volt data

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
df.to_csv(r'./Gluten_test1_CV_1.0mgmL.csv')

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

#### Square Wave Voltametry Example

```python
from potentiostat import Potentiostat
import matplotlib.pyplot as plt
import pandas as pd

port = '/dev/tty.usbmodem1301'       # Serial port for potentiostat device
datafile = 'Gluten_test2_SWV_A2NC_FeCN_5.0mgmL_50mV_amp.txt'       # Enter the path that you want the datafile save time, curr, volt data

test_name = 'squareWave'        # The name of the test to run
curr_range = '100uA'        # The name of the current range [-100uA, +100uA]
sample_rate = 100.0         # The number of samples/second to collect

volt_min =  0.45               # The minimum voltage in the waveform (V)
volt_max =  -0.15              # The maximum voltage in the waveform (V)
step_voltage = 0.00075
volt_per_sec = 0.075         # The rate at which to transition from volt_min to volt_max (V/s)
amplitude = 0.05                                # Waveform peak amplitude (V) 

# Create dictionary of waveform parameters for cyclic voltammetry test
test_param = {
        'quietValue' : volt_min,
        'quietTime'  : 100,
        'amplitude'  : amplitude,
        'startValue' : volt_min,
        'finalValue' : volt_max,
        'stepValue'  : step_voltage,
        'window'     : 0.05,
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
df.to_csv(r'./Gluten_test2_SWV_A2NC_FeCN_5.0mgmL_50mV_amp.csv')

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

---

# Troubleshooting

### **I’m not getting a signal or getting a poor signal during square wave voltammetry**
Possible causes and solutions:
1. **Improper alligator clip positioning:**  
   Ensure clips are properly positioned on the SCE (working/counter/reference electrode). At least one metal tooth must touch the silver portion at the top of the SCE.
2. **Alligator clips touching:**  
   If clips touch, the potentiostat signals may malfunction and damage or fry the SCE. Keep clips properly spaced.
3. **Incomplete electrode submersion:**  
   Ensure the counter, reference, and working electrodes are fully submerged in the liquid analyte.
4. **Fried SCE:**  
   Check for visible "burn" marks, particularly on the counter electrode.
5. **Liquid on the SCE in inappropriate areas:**  
   Ensure the SCE and alligator clips are dry before proceeding.
6. **Improper antibody conjugation:**  
   Verify the antibody conjugation process to ensure antibodies are correctly attached to the SCE.
7. **Changing parameters such as scan rate or amplitude:**  
   Adjustments to parameters like scan rate or amplitude can significantly impact results. Test with standard settings before modifying these values.

Example photos:
- **Dipping level for rinsing electrodes:** Ensure liquid levels do not reach the alligator clips.
  ![Screenshot 2025-01-17 at 3 43 35 PM](https://github.com/user-attachments/assets/5edb2397-539f-42e4-a65f-266266e81cc8)
- **Improper alligator clip connections:** Avoid touching connections and ensure each clip contacts the correct electrode.
  ![Screenshot 2025-01-17 at 3 43 59 PM](https://github.com/user-attachments/assets/33ed41c0-a063-4883-be02-f4a74bb50fd5)

---

### **My signal-to-noise ratio is bad during cyclic voltammetry**
- **Scan rate issues:**  
  Changing scan rates can alter the signal-to-noise ratio. Higher scan rates typically improve the ratio but may cause peak shifting or disappearance.
- A visual demonstration of this effect is provided below:
  - [Higher scan rates yield better signal-to-noise ratios but can reduce peak clarity](https://blog.iorodeo.com/tutorial-cyclic-voltammetry/).

---

### **My signal-to-noise ratio is bad during square wave voltammetry**
- **Amplitude and averaging window effects ([Details here](https://pineresearch.com/shop/kb/software/methods-and-techniques/voltammetric-methods/square-wave-voltammetry/)):**  
  - **Amplitude:**  
    Increasing amplitude improves the signal-to-noise ratio but reduces baseline and peak distinction.
  - **Averaging window:**  
    A smaller value (e.g., 0.05) minimizes noise but sacrifices curve smoothness. Higher values (e.g., 0.1) smooth the curve but reduce peak resolution.
    Its generally recommended to start with a lowe value and increase slowly
    ![Screenshot 2025-01-17 at 3 46 18 PM](https://github.com/user-attachments/assets/ff4adf7c-16ec-4526-aafd-d6ca9b176dc7)

---

# Alternative Options and Project Considerations
With all of these options, make sure you discuss with Dr. Osuji and the TA before you proceed.
### **Project Additions for Students**
1. **Determination of Equilibration Times:**  
   - Explore required equilibration times for electrodes in glucose solutions to achieve stable measurements.  
   - Investigate variations based on concentration or solution complexity.

2. **Continuous Measurement:**  
   - Use manual potentiostat controls to perform real-time continuous measurements.

3. **Varied Conjugation Times/Parameters:**  
   - Test different conjugation times, components, and parameters to optimize electrode functionalization.

4. **Complex Mixtures/Food Breakdown:**  
   - Test gluten sensors on digested gluten from food products, both gluten-containing and "gluten-free."  
   - Validate gluten-free claims and measure contamination levels in processed foods.

5. **Determination of SCE Variability:**  
   - Assess the consistency and reproducibility of functionalized SCEs in detecting gluten concentrations.

6. **Flow Cell:**  
   - Implement a flow cell for continuous glucose solution testing. Combine this with in-situ mixing and continuous measurement.

7. **Electrode Housing:**  
   - Design custom housings for SCEs to improve experimental consistency and reliability.
   - Two examples of housing/custom glassware for standard electrodes from Pine Research (Sources [A](https://pineresearch.com/shop/products/cells-and-glassware/low-volume-cells/complete-low-volume-kits/glassy-carbon-working/) and [B](https://pineresearch.com/shop/products/cells-and-glassware/standard-volume/three-electrode-utili-shaft-e/))

---

### **Non-Electrochemical Options**
1. **Paper Strip-Based Evaluations:**  
   - Detect target molecules using paper strips functionalized with antibodies and gold nanoparticles.  
   - **Source:** [Paper-Based Sensors](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6387326/pdf/sensors-19-00554.pdf)
   - **More Resources:** [Article 1](https://pubs.acs.org/doi/epdf/10.1021/ac500835k) and [Article 2](https://pdf.sciencedirectassets.com/272416/1-s2.0-S1046202318X00127/1-s2.0-S1046202317304292/am.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjENX%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQC83zh2d4vz88M08w1VXiohsOTfe4Z9B0cY9TPiWuH0KgIhAJvczc2zjSA%2B9tefDuGkOMDWOlTOCXHCMn63G5UB89OmKrsFCI7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMDU5MDAzNTQ2ODY1Igwe1%2FOFUqufvHAbYtQqjwXUnKY6mNMv3wJUk%2FdNSlxQinIeCaVgzvmnLf2OOFXS1Nu2T%2ByYpizVwGw1rlDUA2HC55vutpn0yb9E4v1QLX1%2B0d11Qg1E6H1yv6zyz5FHgKtQCLEkxlyO0NqOcw5C0iCF%2FLHZHPZbpeVGmCkJ9wDW9nIoFTWRNWINplzSWLcczsDG7lYnfKROtOqhbpmWPrB7jZE90vpY58iSVwFUrLzN6Z61QW1mA5GNK1EjWEYKtLErGh%2FFPNIO%2Bp0vMWQKzCFPuMXrgECETOavymRS%2F2LiphYX7zftiAsD14vLVEEPXT%2FbYdzQpFNrC7SjSZS3y7Gq2QrUTH772CmW0NH%2BHdG%2FVbO3SqiABrUtZPECoo7GVz7QwfBXjiv%2BWy6kHK0ZpE%2FDPDaSNGGlxRQUh52ZJkwpUzSx78uvKbQJ88mN3tb9n%2BTpWgl6bsqBDn%2BB5%2FdTwVhV8tEGAzsED97MoCtuVMwhXzWFdYf1SxCaa01k3Xa08yAmlOm55sj7HiDEnXNEoaikoCjC0DxdkZp4FS%2F8pykWkRPxHoeuOLjZinhm1%2FhDl5REVN50lWgjGAYyVLzhiO5rntJ082pB5bQpAqAdv7pHc3U8wv1pvbpg%2BtRyy4%2FfONlPDkOUi%2F7QbuCw8Uy6EHHrscatz4G47qkZtOJJ5rjLum8SsCkV8Jxj%2BJCqFx6teFEveMgYgaK%2Be1o90np%2BJPRVc81myEwXvKNZRVuVhc9Jr9a20JISZxdDlmbv1yO6SHVb6yxgtlUCSPtMzuQu%2BzGKxGLzy4Rn%2FWKwmeqLclG%2B%2Fcnd2zQUqVgkF0ywe1Qt3hcIDNIIU9xtw6XombHcVmE5X%2B8pRSzjeZmP15DVHIyOzJQ1BaHQaBDw7weaSuc2MJyTlbQGOrABOdcE12RBMpriXxpO8%2FdNomDl8UoLBe3EGCHMTZi%2B1gqfO1kV5XO3KH9Pja4ni64wCtlERpoVdtz8OqGIp2cA9E73ECD5eT1QFEvqBRE9Z5q4G%2Ftq7TbYN%2BuDfNc85hQJy3yLv8Y6Kl0NExnN8X9zDycdb%2Bx4Ek0uJ%2F9w9cxrEa4YrR82M9WUaBHNzNRY3nsTbcO2DA5xHBED8Li6rEX4kcQCz5q8SnXZ7g8bQsZJREE%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240703T135221Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY6TMGZDH4%2F20240703%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=3df758a5afc91f0c974ff304e2563402c54fe092cf170daa7284ad1974fa5bf9&hash=8e70bdc91b9dc1fae54a8874f8ce4cb94fe84520866a5c7e72cedbc8fcf4ff61&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S1046202317304292&tid=pdf-d233c84b-1c18-4f23-b5cd-446dd02d74f1&sid=a2c3cdcb4373e84b891bb43576214bfb0c40gxrqa&type=client)

2. **ELISA (Enzyme-Linked Immunosorbent Assays):**  
   - Detect antibodies or proteins using a well-plate-based assay. This can work for proteins as well with different ordering of items – you can put a binding antibody onto the surface instead of an antigen.
   - **Source for ELISA methods:** [ThermoFisher Guide](https://www.thermofisher.com/blog/behindthebench/developing-your-own-elisa-spike-recovery-experiments/)

3. **Lab-on-a-Chip:**  
   - Utilize miniaturized systems for antibody or RNA detection.  
   - **Source:** [Nature Article](https://www.nature.com/articles/s41551-022-00919-w)

4. **Peristaltic Pumping:**  
   - Create a 3D-printed, open-source peristaltic pump for controlled flow.  
   - **Source:** [Open-Source Pump](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6994627/)

5. **Colorimetric Assays:**  
   - Detect proteins with methods like Bradford assays, although not protein-specific.  
   - **Sources:** [Bradford Method Guide](https://www.qiagen.com/us/knowledge-and-support/knowledge-hub/bench-guide/protein/protein-analysis/quantifying-proteins-using-the-bradford-method)  
     [Bradford Calibration Data](https://blog.iorodeo.com/bradford-calibration-data/)

6. **Optical Sensors:**  
   - Explore optical methods for protein detection.  
   - **Source:** [Development of Biosensors](https://www.medicaldesignbriefs.com/component/content/article/14635-development-of-a-low-cost-portable-biosensor-for-blood-protein-detection)

---

# References and Additional Sources

This list functions as a collection of sources with brief descriptions used to build the project. Inline sources mentioned earlier are generally not repeated here. For additional knowledge, consult the knowledge bases from [**Pine Research**](https://pineresearch.com/shop/kb/), [**Zimmer Peacock**](https://www.zimmerpeacocktech.com/knowledge-base/), and [**PalmSens**](https://www.palmsens.com/knowledgebase/).

---

1. [**Starter Video on Electrochemical Sensing**](https://www.youtube.com/watch?v=em1bBmkj6Xg)  
   - Overview of electrochemical methods for protein detection, conjugation techniques, and expectations for results.

2. [**Review Article on Detecting Allergens with Electrochemical Methods**](https://www.mdpi.com/1424-8220/16/11/1863)  
   - Explores a variety of methods for detecting allergens using electrochemical techniques.  
   - Great reference for advanced exploration beyond the basics.

3. [**Applications of Electrochemical Biosensors Based on Functional Antibody-Modified Screen-Printed Electrodes: A Review**](https://pubs.rsc.org/en/content/articlelanding/2022/ay/d1ay01570b#cit23)  
   - Discusses methods for sensing with and detecting antibodies.  
   - Includes numerous options and descriptions, though some techniques may not be accessible.

4. [**Primary Source for Conjugation and Electrochemical Methods**](https://ieeexplore.ieee.org/document/8759873)  
   - Comprehensive background with parameter variations and detailed CV ranges.  
   - Useful for understanding expectations and refining methods.

5. [**Electrochemical Experiments on Gluten Detection**](https://www.sciencedirect.com/science/article/pii/S0308814615004045)  
   - Focused on gluten-specific parameters and dissolution methods.  
   - Offers basic techniques with expected results.

6. [**Pine Research: Voltametric Methods**](https://pineresearch.com/shop/knowledge-category/methods-and-techniques/)  
   - Detailed descriptions of voltametric techniques and their applications.

7. [**Nanomaterials-Based Electrochemical Immunosensors Review**](https://www.mdpi.com/2072-666X/10/6/397)  
   - Advanced methods for antibody sensing, though reliant on inaccessible technology.  
   - Useful for conceptual inspiration and adapting techniques.

8. [**Electrochemical Detection of Ovalbumin Using Screen-Printed Electrodes**](https://pubs.rsc.org/en/content/articlelanding/2013/an/c3an36883a)  
   - Example methods for detecting a different allergen/protein (ovalbumin).

9. **Zimmer-Peacock Resources on Sensor Fabrication**  
   - [Optimizing Sandwich-Type Assays](https://www.zimmerpeacocktech.com/2017/05/23/optimizing-sandwich-type-assays/)  
   - [Electrochemical Immunoassay FAQ](https://www.zimmerpeacocktech.com/knowledge-base/faq/electrochemical-immunoassay/)  
   - [Forming SAM on Gold Electrodes](https://www.zimmerpeacocktech.com/knowledge-base/faq/forming-sam-on-gold-electrodes/)

10. [**Article on Designing Biosensors**](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2771472/)  
    - Overview of design considerations, including protective barriers to prevent interference.

11. [**Review Article on SPEs for Biosensors**](https://link.springer.com/article/10.1007/s00604-014-1181-1#Sec27)  
    - Covers biosensor applications using screen-printed electrodes (SPEs).  
    - Includes approaches for glucose and other molecules with functionalization schemes.

12. [**Review Article on Electrochemical Biosensors and Architectures**](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3663003/)  
    - Discusses electrochemical biosensors with examples of tests and advanced methodologies.

13. [**Chemistry of Gluten**](https://www.sciencedirect.com/science/article/pii/S0740002006001535)  
    - Details on gluten solubility, protein types, content, and DNA aspects.

14. [**Electrochemical Immunosensor for Zearalenone Detection Using SPEs**](https://www.sciencedirect.com/science/article/pii/S1572665718307240?via%3Dihub)  
    - Methods for detecting zearalenone (a protein in beer and wine) with modified SPEs.  
    - Useful reference for alternative protein detection.

15. [**Capsaicin Detection Using Screen-Printed Carbon Electrodes**](https://link.springer.com/article/10.2116/analsci.33.793)  
    - Advanced methods for capsaicin detection.  
    - Helpful for understanding modifications to carbon electrodes.

16. [**Article on Various Allergens and Biosensing Methods**](https://www.sciencedirect.com/science/article/pii/S2214180417301137#s0060)  
    - General overview of allergen detection methods, including beyond electrochemical techniques.

---

### Notes
- These references provide a mix of practical and conceptual insights for building electrochemical biosensors.  
- For students, these resources can guide further exploration into advanced techniques and alternative project ideas.

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

