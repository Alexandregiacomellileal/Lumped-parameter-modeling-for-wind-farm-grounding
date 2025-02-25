# A new lumped parameter modeling for wind farm grounding measurement circuits based on clamp-on ground meters.

![LPM_030124](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/3421fd54-5b76-458d-a13e-525662ec4fb8)

## Associated research papers
- A new lumped parameter modeling for wind farm grounding measurement circuits based on clamp-on ground meters
- Integrated approach for wind turbine grounding resistance estimation: Bridging clamp-on ground meter, computational simulations, and machine learning

### Overview

This work delves into the impact of mutual impedance between grounding elements when measuring the grounding resistance of wind turbines using clamp-on ground meters. The repository provides files and resources related to the study, including simulation models, results, and visual representations.

### Article Highlights

The research article addresses:
- The impact of mutual impedance in measuring wind turbine grounding resistance.
- Proposal of a novel lumped parameter model for wind farm grounding.
- Simulation of turbine ground resistance readings through lumped parameter modeling and electromagnetic field modeling.
- Demonstration of the accuracy of the proposed solution in estimating the impedance of the measuring loop in a wind farm grounding system.

### Case study

A grounding section of the São Bento Wind Complex (SBC) located in northeastern Brazil was chosen to present and validate the proposed model. Figure 1 shows the grounding of the case study containing three wind turbines interconnected by horizontal electrodes of 300 m. Such a grounding represents a typical section of a conventional wind farm grounding system. The grounding of the turbine consists of a reinforced concrete foundation and bare copper wires and has an approximately cylindrical shape with a radius of 7.88 m and a height of 17.2 m. The horizontal electrodes consist of a 300 m long bare copper wire with a cross-section of $95 \ mm^2$, buried at a depth of 1 m. The horizontal electrode wires are drawn into the turbine tower through an insulated conduit and connected to the main earth bonding bar. The closest distance ($s$) between the turbine grounding edge and the horizontal electrodes is 11.4 m.

**Figure 1**      
<img width="900" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/6048e2cf-13a8-4319-aeac-8d547ca9a82b">

The instrument chosen for the case study was a UT278A clamp-on meter whose induced voltage signal in the measurement circuit has a sinusoidal waveform with a constant amplitude of 0.028 V and a frequency of 1572 Hz. The instrument must be clamped to the measurement circuit branch in series with the turbine grounding of interest. If a single cable down to the turbine ground is not available, an alternative would be to make the meter claw hook all the horizontal electrodes connected to the grounding turbine of interest before its connection with the grounding bar, thus ensuring that the current that will pass through the instrument is the same as that flowing through the turbine grounding of interest - Figure 1. All power and communication cable screens, armor, or concentric earth wire must be disconnected during the measurement procedure. 

This work will consider that the case study grounding system can be installed in different homogeneous soils with a low-frequency resistivity $\rho$ of 100, 300, 5252, and 10240 $\Omega \cdot m$. Additionally, it will be evaluated its installation in a typical two-layer soil with a resistivity of 5252 $\Omega \cdot m$ in the first five meters of depth and 300 $\Omega \cdot m$ in the deepest layer. The relative permeability and permittivity of the soil were assumed to be constant and equal to 1 and 9, respectively. 

### Lumped Parameter Modeling using ATP

The lumped parameter model for the ground impedance measurement loop of Figure 1 was established and simulated in ATP (Figure 2-B) \ [[celulapi_COMSOL_k_RLC.acp](https://github.com/Alexandregiacomellileal/lumped_parameter_model_experimental_validation_alternative/blob/main/celulapi_COMSOL_k_RLC.acp)] to acquire the meter readings Zmed<sub>LPM</sub> following the procedures detailed in Section 2.2 of the associated research paper. Furthermore, the lumped parameter modeling used in [our previous work](https://github.com/Alexandregiacomellileal/A-New-Approach-Towards-Error-Reduction-in-Ground-Resistance-Measurements-Based-on-Clamp-on-Method) [^1] was also established and simulated in ATP (Figure 2-A) for comparative purposes [[23_model.acp](https://github.com/Alexandregiacomellileal/lumped_parameter_model_experimental_validation_alternative/blob/main/23_model.acp)].

**Figure 2**     
<img width="700" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/c9220f19-cd84-405b-9b2a-04bf79b8b76c">



In Figure 2-A, the following parameters are defined:

- **$R_f$:** Turbine grounding resistance (Ω)
- **$L_p$:** Horizontal electrodes' self-inductance (H)
- **$R_s$:** Horizontal electrodes' self-resistance (Ω)
- **$R_p$:** Horizontal electrodes grounding resistance (Ω)

Figure 2-B extends the model for improved accuracy by introducing additional components:

- **$C_f$:** Turbine grounding capacitance (F)
- **$C_p$:** Horizontal electrode capacitance (F)

To represent the mutual couplings between the grounding of the turbine under test and its adjacent horizontal electrodes and compensate for the distortion caused by the representation of a cylindrical horizontal electrode by two hemispherical ones, the following parameters are introduced:

- **$k$:** A dimensionless parameter related to modeling error, varying from 0 to 1, to be estimated in the next section of this document.
- **$R_c$:** Resistance (Ω), calculated as $R_c = (R_f + R_{eq}) \frac{k}{1-k}$ (Ω).
- **$C_c$:** Capacitance (F), calculated as $C_c = (\frac{C_f \cdot C_{eq}}{C_f + C_{eq}}) \frac{1-k}{k}$ (F).

Here, the equivalent values of the electrical quantities of the return electrodes located close to the measuring point are represented by $R_{eq}$ (Ω) and $C_{eq}$ (F).
These resistance $R_c$ and capacitance $C_c$ elements serve to establish a path for the portion of the test current flow that doesn't circulate through measurement circuit branches referenced to the remote ground.

### $k$ Parameter Estimation

In our quest to mitigate the impact of mutual coupling in measurements and address distortions arising from the utilization of an equivalent semi-spherical representation of the horizontal electrode, we are engaged in refining the estimation process. Our focus is on enhancing accuracy and reliability by systematically assessing and adjusting the parameters involved in the measurement system. In this way, this section applies the methodology described in Section 3.1 of the associated research article to tune the $k$ parameter in the lumped parameter model. 

In the context of low-frequency conventional measurement procedures involving the injection of a known current (I) into a grounding electrode, while simultaneously measuring the resulting voltage (V) from the electrode to a point theoretically located at infinity, it becomes imperative to account for mutual couplings between nearby grounding electrodes. These couplings should be appropriately represented by introducing an impedance in series with each grounding electrode's impedance.
Specifically, when modeling the measurement equivalent circuit of the clamp meter method in a wind farm ground system, the aforementioned series impedance serves to represent the influence exerted by nearby return current electrodes situated at a considerable distance (greater than 10 times their largest dimension) from the measurement point where the meter is clamped. Moreover, it is crucial to incorporate an impedance in parallel with the measurement loop to account for the mutual couplings between the grounding of the turbine under test and its adjacent horizontal electrodes. This parallel mutual impedance encapsulates the cumulative coupling effects that these electrodes impose on each other. In the newly proposed lumped parameter model, the integration of mutual impedances into the measurement circuit is achieved by introducing a multiplicative factor referred to as $k$. This parameter heightens the meter's perception of the impedance along the earth return paths situated farthest from the measurement point while concurrently diminishing it in the immediate vicinity.

The parameter $k$ is determined by the expression $k = (1 - e_{\text{total}})$, where $e_{\text{total}}$ is the sum of the measurement errors induced by two factors. The first factor is the mutual coupling impedance between the turbine grounding and the horizontal electrode, separated by a distance $s$ meters. The second factor accounts for the error introduced by representing the horizontal electrode using a pair of hemispherical electrodes in a lumped parameter model. 

Mathematically, $e_{total}$ is calculated as $e_{total} = \frac{Zmed_{wire}^\infty - Zmed_{lumped}^{short}}{Zmed_{wire}^\infty}$. Here, $Zmed_{wire}^\infty (\Omega)$ represents the clamp-on reading obtained with the turbine grounding and the horizontal electrode positioned at a considerable distance, ensuring negligible mutual couplings between these elements. Conversely, $Zmed_{lumped}^{short} (\Omega)$ is the clamp-on reading obtained with the turbine grounding and the horizontal electrode separated by a smaller distance $s$, with the horizontal electrode represented by two semi-spherical electrodes spaced to avoid mutual influence. For a single lumped parameter cell representing the horizontal electrode, each semi-spherical electrode is designed to have twice its grounding resistance.

In this study, we conducted computational simulations of the clamp-on method within a single grounding cell of the case study using COMSOL Multiphysics&reg; to determine its $k$ parameter.  Figure 3 illustrates the grounding cell models simulated in COMSOL, which consist of a turbine grounding and a horizontal electrode. 

Figure 3-A depicts the schematic representation of the grounding system electromagnetic model simulated in COMSOL Multiphysics&reg; for the $Zmed_{wire}^\infty$ survey. The turbine grounding was modeled as a cylindrical copper electrode with a radius of 7.88 m and a height of 17.2 m. The horizontal electrode took the form of a cylindrical geometry with a cross-sectional area of 95 mm², buried at a depth of 1 m, and varied in length from 80 to 800 m. All electrodes were embedded in a soil volume with hemispherical geometry, with a radius 30 times the length of the horizontal electrode under test. In the FEM's discretization step of the study case, extra-fine meshes with edge refinement composed of tetrahedral elements were used in all case study domains to obtain more accurate results. The measurement circuit was energized through a feed-lumped port connecting the closest surface points between the turbine grounding and the horizontal electrode. To prevent the high reactance of the feed-lumped port from affecting the measurement results, the simulation was conducted in a stationary regime. The low-frequency soil resistivity values ranged from 20 to 10240 Ω·m. The relative permeability and permittivity of the soil were assumed to be constant at 1 and 9, respectively. Meter readings, taken with a separation between electrodes of 10 times the horizontal length, were estimated based on these parameters.

Figure 3-B illustrates the schematic representation of the grounding system electromagnetic model simulated in COMSOL Multiphysics&reg; for the $Zmed^{short}_{lumped}$ survey. The turbine grounding and horizontal electrode were modeled similarly to the previous scenario. The horizontal electrode was represented by two hemispherical electrodes, each designed to have twice the grounding resistance value of the actual horizontal electrode under test. All electrodes were inserted into a soil volume with hemispherical geometry, with a radius 30 times the length of the horizontal electrode under test. In the FEM's discretization step of the study case, extra-fine meshes with edge refinement composed of tetrahedral elements were used in all case study domains to obtain more accurate results. The measurement circuit was energized through an 11.4 m long COMSOL feed-lumped port connecting the turbine grounding to the nearest hemispherical electrode. This simulation was conducted in a stationary regime for the reasons described earlier. The low-frequency soil resistivity evaluated ranged from 20 to 10240 Ω·m. The relative permeability and permittivity of the soil were assumed constant at 1 and 9, respectively. Meter readings were estimated with an 11.4 m separation between the turbine and the horizontal electrode.
<br><br>

**Figure 3 - COMSOL models used for the survey $Zmed_{wire}^\infty$ (A) and $Zmed_{lumped}^{short}$ (B)** 

<img width="4376" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/151cb6ca-bcad-43e5-933a-3cca3fa8c2bf">
<br><br><br>


Subsequently, the parameter $k$ is computed using the formula $k = \frac{Zmed_{lumped}^{short}} {Zmed_{wire}^\infty}$. This calculation ensures that $k$ accounts for the relative difference between the clamp-on readings under conditions where mutual couplings are significant and when the horizontal electrode is accurately represented by the lumped parameter model. The final value of $k$ quantifies the extent of deviation from the ideal case, with $1 - k$ representing the overall measurement error. Therefore, the parameter k was estimated to be 0.7 for a distance between the turbine grounding and the adjacent horizontal electrode of 11.4 m (defined as $s$). Table 1 displays results obtained at an average soil resistivity of 300 $(\Omega.m)$.

**Table 1**
| $s \ (m)$ | $\rho \ (\Omega.m)$| ${Zmed}_{lumped}^{short} (\Omega) $ | ${Zmed}_{wire}^\infty (\Omega)$| $k$             |
|---------|---------|------------------------|-----------------------|-----------------|
| 11.4   | 300  | 3.2              | 4.6              | 0.7     |

Notably, the COMSOL simulation results reveal that the parameter $k$ remains consistent for a specified value of $s$ across a wide range of soil resistivities, spanning from 20 to 10240 $(\Omega.m)$. Furthermore, variation in the length of the horizontal electrode, ranging from 80 to 800 meters, does not lead to significant changes in the observed value of $k$. Therefore, in instances where simulation software is unavailable for researching the parameter in the measuring circuit, the attached graph of Figure 4 serves as a valuable tool for estimating it according to the distance between the grounding elements in a conventional wind farm. This estimate is particularly relevant in cases where the grounding configuration involves cylindrical-shaped turbine foundations with multiple driven pillars, constructed of reinforced concrete, and horizontal electrodes. To facilitate this estimation, we have developed a Python algorithm, available in [[k_parameter_estimator_SBC.py](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/k_parameter_estimator_SBC.py)].

**Figure 4**       
<img src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/defc7caa-dfa5-4450-b958-91beb23f02a1" width="600" height="375">

### Electromagnetic Field Modeling using COMSOL Multiphysics&reg;

The case study's grounding system of Figure 1 was faithfully implemented in the Electromagnetic Waves and Frequency Domain interface of COMSOL Multiphysics&reg;, according to the design parameters of the wind farm - Figure 5. This physics interface is used to solve the harmonic wave time equation for the electric field. The grounding of each one of the three turbines is represented by a cylindrical copper electrode with a radius of 7.88 m and a height of 17.2 m. The horizontal electrodes are represented by a cylindrical copper electrode with a cross-sectional area of $95mm^2$, a length of 300 m, and buried at 1 m from the ground. All electrodes are inserted in a volume of soil with hemispherical geometry with a radius of 30 times the length of the horizontal electrode under test. In the FEM's discretization step of the study case, extra-fine meshes with edge refinement composed of tetrahedral elements were used in all case study domains to obtain more accurate results. A lumped-feed port was used to simulate the operation of the UT-278A meter clamped to the 11.4 m long insulated cable that connects the horizontal electrodes to the turbine grounding. This simulation was performed at a test frequency of 1572 Hz. In this way, the measurement circuit impedance read by the lumped-feed port is obtained in its rectangular form as $Z_{ feed \ port} = R_{ feed \ port}+jX_{ feed \ port}$ ($\Omega$ ), where $R_{ feed \ port}$ and $X_{ feed \ port}$ is its real and imaginary components, respectively. Thus, the magnitude of the measurement loop impedance, which corresponds to a clamp-on ground meter reading predicted through electromagnetic field modeling $Zmed_{EFM} (\Omega) $, can be calculated as $Zmed_{EFM}= \sqrt{R_{feed \ port}^2+X_{ feed \  port}^2}$.

**Figure 5**       
<img width="976" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/f7c000cc-be28-439f-87c1-9a2979e539ae">


### Distributed Parameter Modeling using ATP

The distributed parameter modeling used in [Nappu et al. (2022)] [^2] was also established and simulated in ATP (Figure 6) for comparative purposes [[DPM_model.acp](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/DPM_model.acp)]. In the course of our simulations, we systematically varied the representation of horizontal electrodes, employing configurations with 10 and 100 RLC cells per electrode, respectively. Notably, the results obtained at the specific frequency of the test signal demonstrated a remarkable concordance between the two scenarios. At the specific low frequency of your test signal, the system's response might be sufficiently captured with a lower resolution (10 cells per electrode). The increased resolution (100 cells per electrode) not have introduced substantial differences in the outcome at 1572 Hz frequency. While the results align closely at the current frequency, it's essential to recognize that different frequencies or varied conditions may reveal divergent behaviors. Further analysis and potentially exploring additional frequencies or refining simulation parameters could provide a more comprehensive understanding of the system's response.

**Figure 6**  
<img width="700" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/121dac6a-2986-4493-a3eb-6feeeb0c8a7d">


### Results

Table 2 juxtaposes the meter readings $Zmed_{LPM}$ acquired through lumped parameter modeling as utilized in [^1], and $Zmed_{DPM}$ obtained via distributed parameter modeling from [^2], alongside the readings proposed in this paper. In addition, Table 1 showcases the readings derived through Computational Electromagnetic Modeling with COMSOL denoted as $Zmed_{EFM}$. The measurement circuit was simulated under different homogeneous soil with a low-frequency resistivity of 100, 300, 5252, and 10240  $\Omega \cdot m$. A computer simulation was also carried out using a typical two-layer soil with a resistivity of 5252  $\Omega \cdot m$ in the first five meters of depth and 300  $\Omega \cdot m$ on the deeper layer. The results obtained by the computational simulation of the electromagnetic model of the case study were not significantly affected by the variation between 1 and 10 of the relative permittivity of the soil, so we assume that its value is constant and equal to 9 in this study. In the context of electric circuit modeling, the expected absolute percentage error ($APE_{model}$) is calculated based on the standard $Zmed_{EFM}$. The formula for calculating $APE_{model}$ (%) is given by:


$\ APE_{model} = |\frac{{Zmed_{model} - Zmed_{EFM}}}{{Zmed_{EFM}}}| \times 100 \$

Where:
- $APE_{model}$ is the expected absolute percentage error for the electric circuit modeling.
- $Zmed_{EFM}$ is the standard value taken for comparison.
- $Zmed_{model}$ is the observed value from the electric circuit modeling.

This formula provides a measure of the percentage difference between the observed and standard values, allowing for an assessment of the accuracy of the electric circuit model.

**Table 2: Comparison of Meter Readings**   
| $\rho \ (\Omega \cdot m)$ | $Zmed_{EFM} (\Omega)$ | $Zmed_{DPM} (\Omega)$ [^2]| $Zmed_{LPM} (\Omega)$ [^1]| $Zmed_{LPM} (\Omega)$ (Proposed) | $APE_{DPM}$ (%) [^2] | $APE_{LPM}$ (%) [^1]| $APE_{LPM}$  (%) (Proposed)|
|---------------|------------------------|------------------------|------------------------|----------------------------------|------------------|------------------|------------------------|
| 100             | 1.26              | 2.21                | 1.97                | 1.38                       | 75.45            | 56.25            | **10.27**              |
| 300             | 3.65              | 5.12                | 5.22                | 3.82                         | 40.23            | 42.84            | **4.70**               |
| 5252            | 59.92             | 77.69                | 76.08                | 60.09                          | 29.65           | 26.96            | **0.28**               |
| 10240           | 116.80            | 151.38                | 149.59              | 117.08                         | 29.61            | 28.07            | **0.24**               |
| 5252/300          | 5.38           | 6.51                | 6.67               | 5.91                          | 21.04            | 24.08            | **9.88**               |

Table 2 illustrates a robust agreement in the outcomes obtained between the proposed lumped-parameter model and the electromagnetic method. When considering homogeneous soil, the model adeptly captures the behavior of the actual measurement circuit across a spectrum of apparent soil resistivity, spanning from the lowest to the highest values encountered in wind farms. Notably, the error approached zero for soils characterized by high resistivities, a common scenario in wind farm environments. The simulation results demonstrate that the proposed solution excels in accurately estimating the low-frequency impedance of the measuring loop. On average, the proposed model exhibits an error rate that is 85.8% lower compared to the model used in [^1].

### Files

- [[paper_results.xlsx](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/paper_results.xlsx)]: Excel file comprising two spreadsheets: (i) "Results of Section 3" containing input parameters for both computer simulation models in the study case, along with the corresponding results, and (ii) "Results of Section 3.1" encompassing input and output data employed for investigating the parameter $k$ in the case study through electromagnetic modeling using COMSOL Multiphysics.

- [[case_study_COMSOL.mph](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/case_study_COMSOL.mph)] : COMSOL Multiphysics model file used for the computer simulation of the case study through its electromagnetic field modeling according to Section 2.3 of the associated research paper. Such file can also be used to survey the $k$ parameter according to Subsection 3.1, simply making changes to the electrodes' geometry and spacing between them. 

- [[lumped_parameter_model.pdf](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/lumped_parameter_model.pdf)] presents the equivalent measurement circuit of the case study modeled by lumped parameters, in which, $R_f$ corresponds to the turbine grounding resistance (Ω), $C_f$ corresponds to the turbine grounding capacitance to earth (F), $R_s$ is the horizontal electrode self-resistance (Ω), $L_p$ is the horizontal electrode self-inductance (H), $R_p$ is the horizontal electrode grounding resistance (Ω), and $C_p$ corresponds to the horizontal electrode capacitance to earth (F) . Furthermore, a resistance $R_c$ (Ω), a capacitance $C_c$ (F) and an adjustment parameter $k$ were added to the lumped-parameter model to represent the impact of mutual resistance between the grounding elements and mitigate distortions due to modeling.

- [[DPM_model.acp](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/DPM_model.acp)] presents the equivalent measurement circuit from the case study modeled by distributed parameters and simulated in ATP (Alternative Transients Program).

- [[k_parameter_estimator_SBC.py](https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/blob/main/k_parameter_estimator_SBC.py)] : Python algorithm for estimating $k$-parameter in wind farms based on the distance $s$ (m) between the grounding turbine and horizontal electrodes.

### Apendice - Understanding $e_{total}$ behavior

As previously stated, the parameter $k$ is determined by the expression $k = (1 - e_{\text{total}})$, where $e_{\text{total}}$ is the sum of the measurement errors induced by two factors. The first factor is the mutual coupling impedance between the turbine grounding and the horizontal electrode, separated by a distance $s$ meters ($e_{\text{mutual}}$). The second factor accounts for the error introduced by representing the horizontal electrode using a pair of hemispherical electrodes in a lumped parameter model ($e_{\text{hemispherical}}$). The parameter $k$ reflects the overall correction, considering both sources of measurement errors. 

Figure 7 illustrates a graphical representation of the error in assessing the impedance of the measuring loop concerning the variation in the length of the horizontal electrode under test. The dimensions of the turbine grounding and the separation distance $s$ are kept constant, as reported in case study. This graph is specifically generated for soil with a resistivity of 300 $\Omega.m$; however, its applicability extends to represent soils within a resistivity range of 20 to 10,240 $\Omega.m$. 

**Figure 7**      
<img width="494" alt="image" src="https://github.com/Alexandregiacomellileal/Lumped-parameter-modeling-for-wind-farm-grounding/assets/96079504/28cd16d6-f6c9-4c65-8b22-9fba267d491d">

In Figure 7, we observe that the error arising from the mutual impedance between the grounding elements ($e_{\text{mutual}}$) is not constant and decreases as the length of the horizontal electrode increases. Conversely, the error resulting from the distortion introduced by representing the horizontal electrode with two hemispheres (\($e_{\text{hemispherical}}$) increases with the size of the horizontal electrode. The combination of these factors produces an interesting effect, yielding a total error (\($e_{\text{total}}$) that remains practically constant regardless of the horizontal length. This consistency proves highly advantageous for our modeling. Consequently, we can employ a specific value of ($k$) for any combination of turbine grounding and horizontal electrode length, as long as we maintain a constant separation distance ($s$).

Through our proposed modeling of concentrated parameters, we can estimate the value of ($k$) for a clamp-on ground measurement circuit in a conventional wind farm, given knowledge of the standard separation distance ($s$) between the turbine grounding and the adjacent horizontal electrode. The ability to apply a consistent value for ($k$) across various wind farm configurations significantly simplifies the modeling and analysis of the measurement circuit, assuming the separation distance ($s$) remains constant. This approach holds the potential to enhance the efficiency and accuracy of characterizing the measurement system.


[^1]: A.G. Leal, H.L. L ́opez-Salamanca, A.E. Lazzaretti, D.C. Marcilio, A new approach for ground resistance measurements in onshore wind farms based on clamp-on meters and artificial neural network, Electric Power Systems Research. 210 (2022) 108161.

[^2]: Nappu, M.B., Arief, A., Noor, M.G.: A specific modeling of ground protection system for wind power plants. Energy Reports 8, 647–651 (2022)
________________________________________________________________________________________________________________________

### Contact us:
Please send an email to: alexgiacomelli@yahoo.com

________________________________________________________________________________________________________________________

### Contributors:
Federal University of Technology – Parana (UTFPR) and Institute of Technology for Development (LACTEC)

________________________________________________________________________________________________________________________
<p align="center">
  <img src="https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2FAlexandregiacomellileal%2FLumped-parameter-modeling-for-wind-farm-grounding&label=Visitors&labelColor=%23697689&countColor=%23ff8a65" alt="Visitors Badge">
</p>
