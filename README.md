# 🧬 Molecular Docking-Based Comparative Analysis of Marrubiin Against Cardiovascular Protein Targets

## 📌 Title Justification
- Molecular Docking-Based → Core computational method (AutoDock Vina)  
- Comparative Analysis → Multiple protein targets evaluated  
- Marrubiin → Ligand under investigation  
- Cardiovascular Protein Targets → Biological relevance  

---

## 📖 Project Overview
This project presents a systematic in silico molecular docking study evaluating the interaction of Marrubiin with selected protein targets. The workflow includes structure preparation, docking simulation, and interaction analysis.

---

## 🎯 Objectives
- Evaluate binding affinity (kcal/mol)
- Identify most stable protein–ligand complex
- Analyze protein–ligand interactions
- Compare docking results across targets
- Assess drug-likeness suitability

---

## 🧰 Tools & Resources

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

## ⚙️ Methodology

### Step 1: Protein Preparation
```bash
delete solvent
delete ions
delete ligand
````

Save:

```bash
protein_clean_XXXX.pdb
```

---

### Step 2: Ligand Preparation

```bash
ligand.pdb
```

---

### Step 3: PDBQT Conversion

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

### Step 4: Grid Setup

| Parameter      | Value        |
| -------------- | ------------ |
| Size           | 70 × 70 × 70 |
| Spacing        | 0.375        |
| Exhaustiveness | 8            |

---

### Step 5: Docking

```bash
C:\CVina\vina.exe --config config_1NIW.txt --out output1NIW.pdbqt
C:\CVina\vina.exe --config config_1GQ4.txt --out output1GQ4.pdbqt
C:\CVina\vina.exe --config config_2R4R.txt --out output2R4R.pdbqt
C:\CVina\vina.exe --config config_2R4S.txt --out output2R4S.pdbqt
```

---

### Step 6: Visualization (PyMOL)

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

### Step 7: Complex Creation

```bash
create complex_XXXX, protein_XXXX_clean or outputXXXX_0001
save complexes/complex_XXXX.pdb
```

---

### Step 8: Interaction Analysis (PLIP)

[https://plip-tool.biotec.tu-dresden.de/plip-web/plip/index](https://plip-tool.biotec.tu-dresden.de/plip-web/plip/index)

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

## 🔍 Analysis

* Best affinity: 1NIW
* Most stable: 1NIW
* Strongest interaction network: 2R4S

```
1NIW > 2R4R > 2R4S > 1GQ4
```

---

## 💬 Discussion

* 1NIW: Hydrophobic + salt bridge stabilization
* 2R4S: Strong hydrogen bonding + electrostatic interactions
* 2R4R: Balanced interactions
* 1GQ4: Weak binding with instability

---

## 🧪 Drug-Likeness

| Protein | Status     |
| ------- | ---------- |
| 1NIW    | Acceptable |
| Others  | Poor       |

---

## 🏁 Conclusion

1NIW shows the best docking performance with stable binding and favorable interaction profile. Other complexes exhibit strong interactions but limited drug-likeness.

