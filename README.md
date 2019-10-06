# Plasma MDQT Simulation

A code combining molecular dynamics (MD) and quantum trajectories (QT) to simulate the interaction of ions in ultracold neutral plasmas with cooling lasers.

The MD portion of the code evolves each ion’s position and velocity due to inter-ion forces derived from a Yukawa one-component plasma model. The QT portion of the code evolves the ion wavefunctions and velocities along the cooling axis according to the ion-light Hamiltonian, which includes the effects from a cooling laser
for the *<sup>2</sup>S<sub>1/2</sub> &rightarrow; <sup>2</sup>P<sub>3/2</sub>* transition and a repump laser
for the *<sup>2</sup>D<sub>5/2</sub> &rightarrow; <sup>2</sup>P<sub>3/2</sub>* transition.

The conventions, units and assumptions of the code are explained in reference [[1]](#reference). For simplicity, the MDQT code consist of a single C++ source file (*PlasmaMDQTSimulation.cpp*). Prior to running a simulation, the user must appropriately set the input parameters, which are contained in a clearly-labeled section in the first 100 lines of the MDQT code, and then the code must be compiled into an executable. The code is parallelized using MPI, and for simulations of large systems requires significant computational resources. For best performance we suggest running it on a supercomputer.

## Installation

This simulation code requires:
- a modern C++ compiler, such as the GNU compiler g++, please refer to [GCC, the GNU Compiler Collection](http://gcc.org) for installation and usage;
- loops parallelized with standard MPI to speed up expensive calculation (e.g. force calculations). We recommend the widely available [Open MPI software](https://www.open-mpi.org);
- the [Armadillo C++ library for linear algebra and scientific computing](http://arma.sourceforge.net)


After installing and checking the availability of the above prerequisites, you can download, clone and compile the source from GitHub:

'''
$ git clone https://github.com/vrinceanu/plasma_mdqt_simulation.git
$ cd plasma_mdqt_simulation 
$ g++ -std=c++11 -fopenmp -o runFile -O3 -lm -armadillo
'''

If you wish to know more in detail what git is and what you can do with it, the [github help page](https://help.github.com/articles/set-up-git) has all the references needed.

## Usage


## References
[1] G.M. Gorman, T.K. Langin, M. K. Warrens, and T. C. Killian, *Combined molecular dynamics and quantum trajectories simulation of laser-driven collisional systems*, _submitted_.

[2] T. K. Langin, *Laser Cooling of Ions in Neutral Plasma*, Ph.D. Thesis, Rice University (2019).
