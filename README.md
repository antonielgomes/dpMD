# distributed-points Molecular Dynamics

`distributed-points Molecular Dynamics` (dpMD) is an enhanced-sampling approach that allows large protein conformational sampling based on `normal mode` (NM) vectors. dpMD generates harmonically restrained structures along NM vectors that are further relaxed with standard MD simulations to fill the conformational space.

NM-driven enhanced-sampling methods highly depend on the set of NM vectors. To guarantee an optional protein conformational sampling with dpMD, we employed `uniformly distributed NM vectors`, generated by a minimization script developed by our team called [PDIM](https://github.com/antonielgomes/dpMD/tree/main/PDIM).

### How does dpMD work?
Before performing conformational sampling with dpMD, a `preparation` step is necessary. Firstly, the protein of interest must be subjected to an `equilibration` step. Following, the protein is (in this case) minimized before `NM calculations`. Then, uniformly distributed vectors obtained from [PDIM](https://github.com/antonielgomes/dpMD/tree/main/PDIM) are used as weights for a `uniform NM combination` of the most relevant (usually low-frequency) modes.
Once all this information is ready, dpMD will be performed in three stages:
<p align="center"><img src="https://github.com/antonielgomes/dpMD/blob/main/dpMD.png" width="1000"/></p>

- First stage: the same (vacuum minimized) structure used in NM calculations is subjected to a series of positional restraints potentials to generate structures properly distributed along NM vectors using [VMOD](https://doi.org/10.1016/0010-4655(95)00052-H).
- Second stage: [Targeted Molecular Dynamics (TMD)](https://doi.org/10.1080/08927029308022170) simulations are conducted for the solvated system, driving the protein towards those structures obtained in the first stage.
- Third stage: all solvated conformations obtained in the preceding stage are further equilibrated and subjected to standard MD simulations to obtain an equilibrated unbiased conformational ensemble.

The ensemble of structures obtained in the third stage corresponds to the conformational exploration performed by dpMD, which can provide insights into protein structure, dynamics, and function.

### Why use dpMD?

The imposed positional restraints along uniformly combined NM vectors followed by standard MD simulations allow dpMD to generate an extensive conformational exploration, outperforming the powerful enhanced-sampling method developed by our team called [MDeNM](https://doi.org/10.1021/acs.jctc.5b00003). Therefore, dpMD is a promising alternative for conducting protein conformational sampling, providing valuable contributions in the field, such as:
- Rational protein conformational sampling.
- Systematic exploration of the NM space.
- Coverage of experimental structures.
- Identification of energetically favorable regions in the conformational space.
- Insights into dynamical and functional aspects of proteins.

In addition, dpMD can be adapted to `any NM vectors` obtained from other techniques or `Principal Component Analysis (PCA)` obtained by standard MD simulations or experimental conformations.

### Tutorial: hen egg-white Lysozyme
A step-by-step tutorial is available for those who want to perform dpMD. Please access the [tutorial](https://github.com/antonielgomes/dpMD/tree/main/tutorial) directory for further information.

### Contact
Questions or suggestions should be addressed to antonielaugusto@gmail.com

<!-- ### Reference
If you use PDIM or dpMD, please refer to the following publication: -->
