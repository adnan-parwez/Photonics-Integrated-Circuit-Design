# Simulation 
Designing and simulating a CWDM (de)multiplexer based on cascaded Mach-Zehnder Interferometers (MZIs) on a silicon-on-insulator (SOI) platform.


# Waveguide
The first step of the project was to study the propagation modes of a silicon-on-insulator (SOI) waveguide.
An SOI waveguide with a width of 450 nm and a thickness of 220 nm was defined
<br>
<br>
<table  align="center">
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/Waveguide_Str1.png" width="100%"/><br>
      <sub><b>Fig. 1.</b> Cross-section of the SOI waveguide structure.</sub>
    </td>
  </tr>
</table>
<br>
<br>

The waveguide was simulated using the Tidy3d  mode solver

<table>
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/Te0.png" width="100%"/><br>
      <sub><b>Fig. 2.</b> Fundamental TE Mode field profile.</sub>
    </td>
    <td align="center" width="50%">
      <img src="Images_Sim/TM0.png" width="100%"/><br>
      <sub><b>Fig. 3.</b> Fundamental TM Mode field profile.</sub>
    </td>
  </tr>
</table>
<br>

From these simulations, the effective refractive index (neff) and the group index (ng) were extracted. The electric field distribution of each mode was also examined to understand how the optical field is confined inside the waveguide.

The simulations confirmed that the selected waveguide dimensions support the fundamental guided modes with good optical confinement. The calculated effective and group indices provide the basic design parameters required for later stages of the project, including interferometers and directional couplers.
<br>

<table align="center" border="0" cellpadding="0" cellspacing="0">
  <tr>
    <td align="center" width="500">
      <img src="Images_Sim/NeffvsWavelength.png" width="80%"/><br>
      <sub><b>Fig. 4</b> Effective index (n<sub>eff</sub>) of the TE₀ and TM₀ modes as a function of wavelength.</sub>
    </td>
  </tr>
</table>
<br>


# Design of Directional Couplers

Directional couplers are one of the most important passive components in photonic integrated circuits because they divide optical power between two waveguides. The objective of this part was to design directional couplers with different coupling ratios required for the cascaded Mach–Zehnder interferometer.

There are two common ways to design a directional coupler for a specific coupling coefficient: by varying the gap at a fixed length, or by varying the coupling length at a fixed gap. In this project, the gap was fixed first, and the beat length (L_π) was extracted from the mode simulation. The required coupler length for each target coupling ratio (κ) was then calculated from the ratio L_coupler / L_π, using the relation κ = sin²(π·L_coupler / 2L_π). This is what Fig. 9 shows κ plotted against L_coupler/L_π, with the five target coupling ratios marked on the curve.

A parameter sweep was performed by changing the gap between the waveguides and the coupling length. For each design, the optical power transferred between the two waveguides was simulated, and the corresponding coupling coefficient was calculated.
<br>

<table  align="center">
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/DC1.png" width="80%"/><br>
      <sub><b>Fig. 5.</b>Beat length (L_π) as a function of gap size, used to determine the coupler length needed for each target coupling ratio </sub>
    </td>
  </tr>
</table>
<br>

A parameter sweep was performed by changing the gap between the waveguides and the coupling length. For each design, the optical power transferred between the two waveguides was simulated, and the corresponding coupling coefficient was calculated.
<br>
<table>
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/DC_str.png" width="100%"/><br>
      <sub><b>Fig. 6.</b> Cross-section of the directional coupler structure.</sub>
    </td>
    <td align="center" width="50%">
      <img src="Images_Sim/DCTE0.png" width="100%"/><br>
      <sub><b>Fig. 7.</b> Fundamental TE₀ mode field of the coupled waveguide pair.</sub>
    </td>
  </tr>
</table>
<br>


Different combinations of coupling gap and interaction length were investigated until the required coupling ratios were achieved. The target coupling coefficients included values such as 0.50, 0.30, and 0.23, which are required for the final CWDM (De)Multiplexer design.
<br>


<table  align="center">
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/DC_BL.png" width="100%"/><br>
      <sub><b>Fig. 8.</b> Coupling ratio (κ) as a function of L_coupler / L_π.</sub>
    </td>
  </tr>
</table>
<br>

# Cascaded MZI Filter Using SAX Model

Using the simulated waveguide and coupler parameters, a circuit-level model of a single MZI stage was built using SAX, a scattering-matrix-based photonic circuit simulator. Two MZI variants (S1 and S2) were defined, matching the two building blocks used in the cascaded filter architecture. The arm-length difference (ΔL) between the two MZI arms was calculated from the effective index at the center wavelength (1.55 µm) to set the correct free spectral range (FSR).



<table  align="center">
  <tr>
    <td align="center" width="50%">
      <img src="Images_Sim/Sax.png" width="70%"/><br>
      <sub><b>Fig. 9. </b> </sub>
    </td>
  </tr>
</table>



Simulated transmission spectrum of the S2 MZI stage, showing the through and drop ports.


<table align="center">
  <tr>
    <td align="center" width="70%">
      <img src="Images_Sim/MZI1.png" width="80%"/><br>
      <sub><b>Fig. 10.</b> Simulated transmission spectrum of the S2 MZI stage, showing the through and drop ports.</sub>
    </td>
  </tr>
</table>

The individual S1 and S2 stages were connected into a four-stage cascaded network, forming the full 4-channel CWDM (de)multiplexer. The final circuit model was simulated across the 1.5–1.6 µm range to confirm that each of the four wavelength channels (1510 nm, 1530 nm, 1550 nm, 1570 nm) is correctly routed to its own output port.

<table align="center">
  <tr>
    <td align="center" width="70%">
      <img src="Images_Sim/DeMux.png" width="80%"/><br>
      <sub><b>Fig. 11.</b> Simulated transmission spectrum of the full four-channel cascaded MZI CWDM (de)multiplexer.</sub>
    </td>
  </tr>
</table>

# Related Work

The physical GDS layout of this filter (component placement, routing, and die-level layout) was built separately using GDSFactory. See Layout folder.

# Note

As noted above, this simulation uses identical-width MZI arms and therefore does not reproduce the paper's fabrication-tolerance result (Figs. 4 and 6–8 of the paper), which relies on differing arm widths to cancel fabrication-induced spectral shift.

# References

T.-H. Yen and Y.-J. Hung, "Fabrication-Tolerant CWDM (De)Multiplexer Based on Cascaded Mach–Zehnder Interferometers on Silicon-on-Insulator," Journal of Lightwave Technology, vol. 39, no. 1, pp. 146–153, Jan. 2021.



