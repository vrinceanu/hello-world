# Plasma MDQT Simulation

This document provides instructions for using the combined molecular
dynamics (MD) and quantum trajectories (QT) code that simulates 1D
optical molasses of the ions within a non-expanding,
uniformly-distributed ultracold neutral plasma, as described in
[1][paper 1]. The MD portion of the code evolves each ion’s position and
velocity due to inter-ion forces derived from the Yukawa one-component
plasma model. The QT portion of the code evolves the ion wavefunctions
and x-velocities (along the cooling axis) according to the ion-light
Hamiltonian, which includes the effects from a 408 nm cooling laser
($^2S_{1/2}\rightarrow\,^2P_{3/2}$) and a 1033 nm repump laser
($^2D_{5/2}\rightarrow\,^2P_{3/2}$).


[paper 1]: <>(G.M. Gorman)
