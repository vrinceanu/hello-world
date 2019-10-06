Introduction 
============

This document provides instructions for using the combined molecular
dynamics (MD) and quantum trajectories (QT) code that simulates 1D
optical molasses of the ions within a non-expanding,
uniformly-distributed ultracold neutral plasma, as described in
@glk2019. The MD portion of the code evolves each ion’s position and
velocity due to inter-ion forces derived from the Yukawa one-component
plasma model. The QT portion of the code evolves the ion wavefunctions
and x-velocities (along the cooling axis) according to the ion-light
Hamiltonian, which includes the effects from a 408 nm cooling laser
($^2S_{1/2}\rightarrow\,^2P_{3/2}$) and a 1033 nm repump laser
($^2D_{5/2}\rightarrow\,^2P_{3/2}$).

These instructions assume the user has basic knowledge of the C++
language and the g++ compiler. Additionally, they assume the user is
familiar with reference @glk2019. For simplicity, the MDQT code consists
of a single file (‘PlasmaMDQTSimulation.cpp’). Prior to running a
simulation, the user must appropriately set the input parameters, which
are contained in a clearly-labeled section in the first 100 lines of the
MDQT code, and then the code must be compiled into an executable. Note
that our simulation code is computationally expensive, so for best
performance we suggest running it on a supercomputer and not a
general-purpose computer.

The rest of this document is organized as follows. The MDQT input
parameters and program options are discussed in Sec.[input parameters].
In Sec.[compiling] we provide instructions for compiling the code with
the g++ compiler on a Linux-based computer. The output file architecture
is described in Sec.[output files], and Sec.[plotting data] provides
instructions for using our MATLAB analysis code that produces all plots
found in @glk2019. Finally, Sec.[continue simulation] discusses how to
continue a simulation from previously-saved conditions.

[introduction](#introduction)
