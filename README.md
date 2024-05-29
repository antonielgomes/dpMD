# dpMD

This repository contains all files necessary to perform the enhanced-sampling approach termed `distributed-points Molecular Dynamics` (dpMD), allowing an extensive protein conformational sampling based on `normal mode` combination.
dpMD induces a given protein to explore conformation along normal mode vectors

[PDIM](https://github.com/antonielgomes/dpMD/tree/main/PDIM).
dpMD is composed of three stages:
<p align="center"><img src="https://github.com/antonielgomes/dpMD/blob/main/dpMD.png" width="1000"/></p>
dpMD normal modes and classical MD. For this end, normal modes, an enhanced-sampling approach that mixes .

This article introduces a novel approach to obtaining a uniformly distributed set of NMs combined vectors and generating harmonically restrained structures along them that are further relaxed with standard MD simulations to fill the conformational space efficiently. It was, therefore, termed 'positionally-restrained Molecular Dynamics' (prMD). Its efficiency was assessed by applying it to the hen egg-white Lysozyme and the human Cytochrome P450 3A4 (CYP3A4), comparing it with other methods, and analyzing the extent of the coverage of existing experimental structures. Results demonstrate the efficacy of prMD in extensive conformational sampling that is enhanced as more NMs are considered. Ensembles generated by prMD exhibit broad coverage of experimental structures, providing valuable insights into the functional aspects of Lysozyme and CYP3A4. Furthermore, prMD identifies energetically favorable regions in Lysozyme's NM space in conformity with experimental conformations. The uniform set of vectors allows systematic exploration of the NM space, allowing the study of the transition between conformational states and sampling regions around or away from experimental conformations. Crucially, prMD's versatility extends to various NM sources, calculated by other methods, including principal component analysis (PCA) from MD simulations or experimental structures. This method offers an efficient and rational framework for comprehensive protein conformational sampling, contributing significantly to our understanding of protein dynamics and function. 

### Reference
If you use PDIM or dpMD, please refer to the following publication:

### FAQ
- W
  - S

### FAQ
Testar **name** and **DISTINCT** name
calculate `normal modes`
```
charmm -i scripts/normal-modes.inp
```

**PDIM** is also available in a compiled version for [Linux](https://github.com/soedinglab/MMseqs2/archive/71dd32ec43e3ac4dabf111bbc4b124f1c66a85f1.zip) and Windows.


generate crd and dcd of modes:
```
charmm -i scripts/normal-modes-dcd-crd.inp nmodes=20
```

generating normal mode combination
```
bash scripts/mdenm-modes-combination.sh
```

combine normal modes
```
charmm -i scripts/generate-combined-modes.inp ncomb=6
```

**MDeNM**
```
scripts/mdenm-namd-exc.sh
```

```
scripts/mdenm-namd-md.sh
```

**VMOD**
```
scripts/runvmod-comb.sh = run vmod to obtain displaced conformations
```

**dpMD**

In this step, the equlibrated system will be driven towards all conformations generated by **VMOD**.

Initially, each conformation will be set as a target in the PDB format using `charmm`. In this example, six replicas were set in `nreps`:
```
charmm -i scripts/target.inp nreps=6
```
Following, TMD will be performed using `namd`:
```
bash scripts/tmd-namd.sh
```

```
charmm -i scripts/restraints.inp nreps=6
```

```
bash scripts/tmd-equil-namd.sh
```

```
bash scripts/tmd-free-md-namd.sh
```

