# Plasma MDQT Simulation

This code combines molecular dynamics (MD) and quantum trajectories (QT) code to simulates optical interaction of ions within a non-expanding, uniform ultracold neutral plasma, as described in [1](#references).

The MD portion of the code evolves each ion’s position and velocity due to inter-ion forces derived from a Yukawa one-component plasma model. The QT portion of the code evolves the ion wavefunctions and velocities along the cooling axis according to the ion-light Hamiltonian, which includes the effects from a cooling laser
for the *<sup>2</sup>S<sub>1/2</sub>&rightarrow;<sup>2</sup>P<sub>3/2</sub>* transition and a repump laser
for the *<sup>2</sup>D<sub>5/2</sub>&rightarrow;<sup>2</sup>P<sub>3/2</sub>*.


# References
[1]: G.M. Gorman
