#  Molecular Docking-Based Comparative Analysis of Marrubiin Against Cardiovascular Protein Targets

##  Title Justification
1. Molecular Docking-Based → Core computational method (AutoDock Vina)  
2. Comparative Analysis → Multiple protein targets evaluated  
3. Marrubiin → Ligand under investigation  
4. Cardiovascular Protein Targets → Biological relevance  

---

## 📖 Project Overview
This project presents a systematic in silico molecular docking study evaluating the interaction of Marrubiin with selected protein targets. The workflow includes:

1. Structure retrieval
2. Protein and ligand preparation
3. Molecular docking
4. Binding affinity comparison
5. Protein–ligand interaction analysis

---

##  Objectives
1. Evaluate binding affinity (kcal/mol)
2. Identify most stable protein-ligand complex
3. Analyze protein-ligand interactions
4. Compare docking results across targets
5. Assess drug-likeness suitability

---

##  Tools & Resources

| Category | Tool |
|--------|------|
| Protein Database | RCSB PDB |
| Ligand Database | PubChem |
| Preparation | ChimeraX |
| Conversion | AutoDock Tools |
| Docking | AutoDock Vina |
| Visualization | PyMOL |
| Interaction Analysis | PLIP |

---

## 🌐 Data Acquisition

### Protein Structures
Source: https://www.rcsb.org  
Format: `.pdb`

| Protein | Description |
|--------|------------|
| 1NIW | Endothelial Nitric Oxide Synthase |
| 1GQ4 | Beta-2 Adrenergic Receptor |
| 2R4R | Beta-2 Adrenergic Receptor |
| 2R4S | Beta-2 Adrenergic Receptor |

---

### Ligand
Source: https://pubchem.ncbi.nlm.nih.gov  
Compound: Marrubiin  
Format: SDF (3D)

---

##  Methodology

### Step 1: Protein Preparation (ChimeraX)

Load protein (.pdb)

```bash
delete solvent
delete ions
delete ligand
````
Add hydrogens via GUI (default settings)

Save as:

```bash
protein_clean_XXXX.pdb
```

---

### Step 2: Ligand Preparation (ChimeraX)

Load ligand (.sdf)
Add hydrogens
Perform energy minimization

Save as:

```bash
ligand.pdb
```

---

### Step 3: PDBQT Conversion (AutoDock Tools)

Protein:

```bash
Add Polar Hydrogens
Compute Gasteiger Charges
Merge Non-Polar Hydrogens
```

Ligand:

```bash
Add All Hydrogens
Compute Gasteiger Charges
Detect Rotatable Bonds
```

---

### Step 4: Grid Box Configuration (AutoDock Tools)

Docking approach: Blind Docking

| Parameter      | Value        |
| -------------- | ------------ |
| Size           | 70 × 70 × 70 |
| Spacing        | 0.375        |
| Exhaustiveness | 8            |

---

### Step 5: Configuration File

Example:

```bash
receptor = protein_1NIW_clean.pdbqt
ligand = ligand_marrubiin.pdbqt

center_x = 34.706
center_y = 34.975
center_z = 54.049

size_x = 70
size_y = 70
size_z = 70

exhaustiveness = 8
num_modes = 9
energy_range = 4
```
---

### Step 6: Docking Execution (AutoDock Vina)

```bash
C:\CVina\vina.exe --config config_1NIW.txt --out output1NIW.pdbqt
C:\CVina\vina.exe --config config_1GQ4.txt --out output1GQ4.pdbqt
C:\CVina\vina.exe --config config_2R4R.txt --out output2R4R.pdbqt
C:\CVina\vina.exe --config config_2R4S.txt --out output2R4S.pdbqt
```

---

### Step 7: Visualization (PyMOL)

```bash
load protein_XXXX_clean.pdbqt
load outputXXXX.pdbqt

hide everything
show cartoon, protein_XXXX_clean
color cyan, protein_XXXX_clean

split_states outputXXXX

show sticks, outputXXXX_0001
color red, outputXXXX_0001

zoom outputXXXX_0001

distance hbonds, protein_XXXX_clean, outputXXXX_0001, 3.5
```

### Save Image

```bash
png images/docking_XXXX.png, dpi=300
```

---

### Step 8: Complex Creation (for PLIP Analysis)

```bash
create complex_XXXX, protein_XXXX_clean or outputXXXX_0001
save complexes/complex_XXXX.pdb
```

---

### Step 9: Interaction Analysis (PLIP)

Access:
[https://plip-tool.biotec.tu-dresden.de/plip-web/plip/index](https://plip-tool.biotec.tu-dresden.de/plip-web/plip/index)

Upload: complex_XXXX.pdb
Output:
1. Hydrogen bonds
2. Hydrophobic interactions
3. Salt bridges
---

## 📊 Results

### Binding Affinity

| Protein | Energy (kcal/mol) |
| ------- | ----------------- |
| 1NIW    | -8.299            |
| 2R4R    | -7.136            |
| 2R4S    | -6.802            |
| 1GQ4    | -6.046            |

---

### Interaction Summary

| Protein | Hydrophobic | H-Bonds | Salt Bridge |
| ------- | ----------- | ------- | ----------- |
| 1NIW    | 6           | 0       | 1           |
| 1GQ4    | 3           | 8       | 0           |
| 2R4R    | 2           | 7       | 0           |
| 2R4S    | 2           | 9       | 2           |

---

##  Analysis

* Best binding affinity: 1NIW
* Highest interaction density: 2R4S
* Most stable docking: 1NIW
* Least reliable: 1GQ4 (high RMSD)

```
1NIW > 2R4R > 2R4S > 1GQ4
```

---

##  Discussion

##  1NIW
1. Strong hydrophobic interactions and salt bridge
2. Stable and energetically favorable
##  2R4S
1. Highest hydrogen bonding and electrostatic interactions
2. Strong interaction network
##  2R4R
1. Balanced hydrogen bonding and hydrophobic interactions
##  1GQ4
1. Strong hydrogen bonding but weak affinity and high variability
---

## 🧪 Drug-Likeness

| Protein | Status     |
| ------- | ---------- |
| 1NIW    | Acceptable |
| Others(1GQ4,2R4R,2R4S)  | Poor       |

---

##  Conclusion

1NIW shows the best docking performance with stable binding and favorable interaction profile. Other complexes exhibit strong interactions but limited drug-likeness.

---
##  Author Contribution

This molecular docking study, including protein and ligand preparation, docking execution, visualization, and interaction analysis, was independently performed by **Riya Kundu** as part of a bioinformatics research project.

All computational workflows were designed, executed, and interpreted by the author using standard molecular docking protocols and tools.
