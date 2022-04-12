================================================================================

###                         CCSD(T)/aVTZ PES for FAM/FAD                 
###                       Meuwly Group @ University of Basel        
                       
================================================================================

README / HOWTO for the usage of the transfer learned PhysNet based NN model for FAM/FAD presented in
Käser and Meuwly: Phys. Chem. Chem. Phys.,2022, 24, 5269. The PES is transfer learnt
to CCSD(T)/aug-cc-pVTZ level quality and can be used to predict energies, forces, 
dipole moments and partial charges. The README will walk through the dependencies
which are needed as well as a few illustrative examples for using the PES.

### Installations & dependencies ================================================

The following installation steps were tested on a Ubuntu 18.04 workstation.

a) Install python3 (I recommend 3.5, as I know this is working and we had problems
   with other versions [see: https://tecadmin.net/install-python-3-5-on-ubuntu/])
   
b) I recommend creating a virtual environment because Python applications often
   use specific versions of a library and venv is a good option to handle this.
   Each venv has its own Python binary (which matches the version of the binary
   that was used to create the environment) and can have its own independent set
   of installed Python packages in its site directories. It is invoked by running
   the following command in the terminal:
   
        python3.5 -m venv /path/to/new/virtual/environment
        
   and activated with:
   
        source /path/to/new/virtual/environment/bin/activate
        
   (deactivated simply by typing deactivate)
   
c) With activated venv use pip to install the atomic simulation environment (ase)
   and all its dependencies [see: https://wiki.fysik.dtu.dk/ase/install.html]
   (tested with version 3.19.1)
   
        pip install ase==3.19.1
        
d) install tensorflow via pip (i recommend version 1.12):

        pip install tensorflow==1.12
        

### Folders =====================================================================

i) "tl_models": contains the NN models used throughout the paper. These files
   can be used to predict energies, forces, dipole moments, to run MD
   simulations, to predict normalmodes, etc.
            
ii) "NNCalculator": in ase a calculator is a black box taking atomic number and
     atomic position from an "atoms object" and calculate different properties
     [see:https://wiki.fysik.dtu.dk/ase/ase/calculators/calculators.html].
     ASE offers quite a large number of calculators and it is quite easy to
     implement new ones. The NNCalculator thus uses Physnet models and predicts
     properties based on a molecule.
     


### Files =======================================================================

i) "fam.xyz & fad.xyz": xyz files of the monomer and dimer. The structures are very
    close to the optimum geometry.
    
ii) "output_fam.dat": File containing the output for the prediction of fam.xyz using the
    PhysNet model.
    
### Examples of Use: ============================================================

i) Energy, force and dipole moment prediction of a molecular geometry using
   "predict_mol.py". (The usage of the script is given in itself). Note that the
   units of the prediction are the same as the ones used in the training data
   set. Here, the energies are printed in eV, the forces in eV/angstrom and the
   dipole moments in elementary charges*angstrom. 
   
ii) Having a full dimensional potential one probably wants to perform geometry
    optimizations for different molecules. This can be done with the
    "optimize.py" script.
    
iii) The NN potential can also be used to predict normal mode frequencies. The
    frequencies can be calculated using ASEs "vibrations" class.  A possible
    implementation is given in "ase_vibrations.py".
    


### How to cite: =================================================================

When using this PhysNet PES for FAM and FAD, please cite the following papers:

Unke, O. T. and Meuwly, M "PhysNet: A Neural Network for Predicting Energies,
Forces, Dipole Moments, and Partial Charges", J. Chem. Theory Comput. 2019,
15, 6, 3678–3693

Käser, S. and Meuwly, M. "Transfer learned potential energy surfaces: accurate
anharmonic vibrational dynamics and dissociation energies for the formic acid
monomer and dimer", Phys. Chem. Chem. Phys., 2022, 24, 5269-5281.


### Contact: =====================================================================

If you have any questions about the PES free to contact Silvan Kaeser
(silvan.kaeser@unibas.ch)
