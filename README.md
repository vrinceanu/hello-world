# Plasma MDQT Simulation

A code combining molecular dynamics (MD) and quantum trajectories (QT) to simulate the interaction of ions in ultracold neutral plasmas with cooling lasers.

The MD portion of the code evolves each ion’s position and velocity due to inter-ion forces derived from a Yukawa one-component plasma model. The QT portion of the code evolves the ion wavefunctions and velocities along the cooling axis according to the ion-light Hamiltonian, which includes the effects from a cooling laser
for the *<sup>2</sup>S<sub>1/2</sub> &rightarrow; <sup>2</sup>P<sub>3/2</sub>* transition and a repump laser
for the *<sup>2</sup>D<sub>5/2</sub> &rightarrow; <sup>2</sup>P<sub>3/2</sub>* transition.

The conventions, units and assumptions of the code are explained in reference [[1]](#references). For simplicity, the MDQT code consist of a single C++ source file (*PlasmaMDQTSimulation.cpp*). Prior to running a simulation, the user must appropriately set the input parameters, which are contained in a clearly-labeled section in the first 100 lines of the MDQT code, and then the code must be compiled into an executable. The code is parallelized using MPI, and for simulations of large systems requires significant computational resources. For best performance we suggest running it on a supercomputer.

## Installation

This simulation code requires:
- a modern C++ compiler, such as the GNU compiler g++, please refer to [GCC, the GNU Compiler Collection](http://gcc.org) for installation and usage;
- loops parallelized with standard MPI to speed up expensive calculation (e.g. force calculations). We recommend the widely available [Open MPI software](https://www.open-mpi.org);
- the [Armadillo C++ library](http://arma.sourceforge.net) for linear algebra and scientific computing.


After installing and checking the availability of the above prerequisites, you can download, clone and compile the source from GitHub:

```
$ git clone https://github.com/vrinceanu/plasma_mdqt_simulation.git
$ cd plasma_mdqt_simulation 
$ g++ -std=c++11 -fopenmp -o runFile -O3 -lm -armadillo
$ ./runFile 1
```

If you wish to know more in detail what git is and what you can do with it, the [github help page](https://help.github.com/articles/set-up-git) has all the references needed.

The executable *runFile* accepts an integer 'job number' argument (1 in the above example), which provides a straightforward way for submitting multiple instances of the code at once. Each time the program is run with a different job number, the output files will be saved within a folder named **'jobX'**, where X is the integer provided as argument. The formats of input parameters and output files are detailed in the sections that follow.

## Analyzing the Output Files

The analysis of MDQT results is facilitated by the MATLAB analysis scripts collected in the **Plasma-MDQT-Analysis** folder. These scripts can be used to reproduce simuation data found within [[1]](#references). 

To run the program, open ‘mainSimAnalysis.m’ in MATLAB and ensure that the folder containing the scipts is added to the MATLAB search path, which may be done by modifying the ‘addpath’ command on line 7. Once that’s done, press ‘Run’ and the program will allow the user to select one or more simulation folders via a dialogue box. MATLAB will then prompt the user to select which program options to use via the command window.


## Input Parameters

All input parameters are grouped into a clearly-labeled section within the first 100 lines of the MDQT code, are defined below.

-   __saveDirectory__ *(string)*: The folder in which simulation data will be saved, relative to the path of the executable file. 

-   __newRun__ *(boolean)*: Tells the program whether to run a new simulation from random initial positions and zero velocity (true) or whether to continue a simulation from previously-saved conditions (false). See Sec. [Continuing a Simulation](#continuing-a-simulation) for more details.

-   __c0Cont__ *(integer)*: Only used when loading previously-saved conditions (newRun = false). **c0Cont** is a 6-digit integer that corresponds to the number of MD time steps undergone in the loaded simulation, and should match the 6-digit integer found in the previously-saved files (e.g. there is an output file with name ‘ions\_timestepxxxxxx.dat’). c0Cont should be set equal to xxxxxx. See Sec. [Continuing a Simulation](#continuing-a-simulation) for more details.

-  __tmax__ *(double)*: Time at which the simulation will end in units of 
_&omega;<sup>-1</sup><sub>pE</sub> = (3)<sup>&frac12;</sup> &omega;<sup>-1</sup><sub>pi</sub>_ ,
where  _&omega;<sup>-1</sup><sub>pi</sub> = [n e<sup>2</sup>/(&epsilon;<sub>0</sub> m)]<sup>&frac12;</sup>_
is the plasma oscillation frequency. A new simulation will run from *t = 0 &rightarrow; tmax*. A continued simulation, which starts at time *t'* (loaded from the save files), will run from *t = t' &rightarrow; tmax*.

-   density (double): Uniform, time-independent plasma density in units of *10<sup>14</sup>  m<sup>-3</sup>*.



## Continuning a Simulation

Due to the MDQT code being computationally expensive, you may run into a situation where the simulation will need to run longer than the time you’re allotted in a single session. For example, some clusters may only allow you to run a simulation for 8 hours at a time, but in order to reach the desired tmax it will take 10 hours. At the end of a simulation we record the ion positions, velocities, and wavefunctions. The code has the ability to continue a simulation by loading these previously-saved conditions.
It’s important that the program finishes running without interruption because the last line of the code saves the particle conditions. If the program is terminated early, the particle conditions will not be saved and you will not be able to continue the simulation. How long the simulation takes depends on the system it’s run on, the number of particles, the density, and tmax. To obtain an estimate of how long the program will take to run, run a simulation with ∼3500 particles, density = 2, and tmax < 1, which should take less than an hour.
Assuming you have successfully completed a simulation, you may continue the simulation from the previously-saved conditions in the following way. First, except for ‘newRun’, ‘c0Cont’, and ‘tmax’, all the input parameters must be the same as they were for the original simulation. Then, set newRun = false and set c0Cont equal to the 6-digit integer found within the most recent ‘condi- tions timestepXXXXXX.dat’ file. Finally, remember that tmax is not the duration of the simulation, it is the time at which the simulation ends. You must change tmax to be greater than it was in the previous simulation, otherwise the continued simulation will end immediately.
Once the input parameters have been changed appropriately, save and recompile the C++ pro- gram following the instructions from Sec.3. Make sure that the new executable file is contained within the same directory as the original executable file because the save directory is relative to the its location.


## References
[1] G.M. Gorman, T.K. Langin, M. K. Warrens, and T. C. Killian, *Combined molecular dynamics and quantum trajectories simulation of laser-driven collisional systems*, _submitted for publication to Physical Review A_.

[2] T. K. Langin, *Laser Cooling of Ions in Neutral Plasma*, Ph.D. Thesis, Rice University (2019).
