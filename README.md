# dpMD

This repository contains all files necessary to perform `distributed-points Molecular Dynamics` (dpMD), an enhanced-sampling approach that allows a large protein conformational sampling based on `normal modes` (NM). dpMD generates harmonically restrained structures along NM vectors that are further relaxed with standard MD simulations to fill the conformational space efficiently.

The main novelty of dpMD is uniformly distributed vectors
induces a given protein to explore conformation along normal mode vectors

[PDIM](https://github.com/antonielgomes/dpMD/tree/main/PDIM).

dpMD is composed of three stages:
<p align="center"><img src="https://github.com/antonielgomes/dpMD/blob/main/dpMD.png" width="1000"/></p>

### Why using pdMD?
The imposed positional restraints along uniformly combined NM vectors allow extensive conformational sampling of proteins, outperforming the powerful enhanced-sampling method developed by our team called [MDeNM](https://doi.org/10.1021/acs.jctc.5b00003). Therefore, dpMD is a promising alternative for conducting protein conformational sampling, including:
- Rational protein conformational sampling.
- Systematic exploration of the NM space.
- Broad coverage of experimental structures.
- Identification of enegertically favorable regions in the conformational space.
- Insights into dynamical and functional aspects of proteins.

dpMD is **versatil**, being adaptable to `any NM vectors` obtained from other techniques or even from `Principal Component Analysis (PCA)` obtained by standard MD simulations or experimental conformations.

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

