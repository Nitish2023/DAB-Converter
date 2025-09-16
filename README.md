# DAB-Converter

This design provides an overview of the implementation of a single-phase Dual Active Bridge (DAB) DC/DC converter. DAB topology offers advantages like soft-switching commutations, a decreased number of devices, and high efficiency. The design is beneficial where power density, cost, weight, galvanic isolation, high-voltage conversion ratio, and reliability are critical factors, making it ideal for EV charging stations and energy storage applications. Modularity and symmetrical structure in the DAB allow for stacking converters to achieve high power throughput and facilitate a bidirectional mode of operation to support battery charging and discharging applications

Power density and system efficiency are two important requirements of a converter in a DC charging station. Operating at high switching frequencies enables the reduced size of magnetics. By moving to higher bus voltage to facilitate fast charging, more power can be transferred at the same current level. This helps to reduce the amount of copper, thereby improving the power density of the converter. The converter must also be highly efficient as it results in significant cost savings and reduced thermal solution.<img width="740" height="487" alt="203494995-dea3e1b7-c0b1-445a-b61e-7a7c7adc6b52" src="https://github.com/user-attachments/assets/7f0b50dd-a30e-4efc-b398-2284df113953" />

MATERIALS AND METHODS

We are using Simulink to simulate and demonstrate this project.

We have a DC source and we are converting it into AC using an inverter. This AC voltage is increased or decreased using a transformer and it is given to the rectifier section. Consequently, AC is converted to DC and a capacitor is used to filter out the DC. Transformer:

The transformer provides isolation between the input and output sides if there is any damage concerning the load consequently it does not affect the source terminals. Also based on the transformer's turn ratio we can step up or down the voltage.

Mosfets and Thyristors:

Due to the total of eight switching elements in this topology, the number of different control methods is very high and there are several degrees of freedom that can be used for optimization. The two bridge branches of a full bridge have a phase shift of 180°. Only the phase shift φ between the primary and secondary full bridge is used to control the power flow. image Switich operations

Each switch is on for 50% of its respective switching period. The switch pairs in the two bridges all have the same switching period but are operated such that between each bridge a phase shift is introduced that varies based on the modulation derived from feedback measurements. The efficiency achievable with the DAB topology lies between 96% and 99% and is primarily determined by the nominal input and output voltage as well as by the switching frequency. A further influencing factor is the desired range of the input and output voltage. This is due to the fact that at low voltages and high powers the ohmic losses represent the dominant loss component and scale these quadratically with the RMS current. In addition, when phase shift control is used in combination with a wide voltage range, there are inevitably working ranges in which an increased reactive current component is created in the transformer resulting in higher losses in the transformer winding. The other loss components in the DAB are given by the switching losses in the semiconductor switches, and the core losses in the transformer. The switching losses of the power semiconductors represent a not negligible proportion of the total losses. In order to select suitable semiconductor switches, the operating conditions in the circuit must first be analyzed. These include the maximum RMS current through the respective switches, the maximum reverse voltage, and the switching currents when the semiconductors are switched on and off. The operating frequency of the converter is also an important criterion. In order to achieve a high-power density, it is necessary to increase the switching frequency. As a result, the usable switches are limited to MOSFETs. IGBTs are no longer suitable for frequencies above 100 kHz due to their high switching losses. If the MOSFET is now switched on, its drain-source voltage is nearly 0 V. This means that there are no significant switch-on losses, which reduces the overall loss balance.
<img width="353" height="389" alt="203495059-e32e969c-07d0-40c4-9978-a2178d5e74fa" src="https://github.com/user-attachments/assets/0b6cb5a4-77df-4697-aa80-9e330740ff16" />

If one considers the switching behavior of the components when operating the DAB with a high power, it quickly becomes apparent that all MOSFETs can be switched here with Zero Voltage Switching (ZVS). In the ZVS, the energy stored in the inductive components is used to recharge the switching nodes of the MOSFETs with virtually no loss. To achieve this, a positive drain-source current must be switched off. The current driven by the inductance then recharges the switching node of the MOSFETs and commutates into the body diode of the second MOSFET of the half-bridge. If the MOSFET is now switched on, its drain-source voltage is nearly 0 V. This means that there are no significant switch-on losses, which reduces the overall loss balance.

If, however, the DAB is operated at very low power using the standard phase shift control, it is no longer possible to switch with ZVS). Then, when the MOSFET is switched off, the current commutates into its own body diode and the voltage of the switching MOSFET corresponds to the input or output voltage. This means that all the energy stored in the output capacitors of the MOSFETs must be converted into heat. In addition, the current flowing in the body diode to be disabled at the time of switching must commutate into the transistor to be switched on within the switching time. During this so-called reverse recovery of the body diode, a cross current flows over the half-bridge, which is completely converted into heat. In order to avoid extreme losses and dynamic over voltages, the body diodes of the MOSFETs must, therefore, have a very short reverse recovery time (trr).

Placing Mosfets and switching them accordingly can convert the DC voltage source to AC voltage source and it will act as an inverter.

Rectifier : image Full bridge rectifier

Rectification converts an oscillating sinusoidal AC voltage source into a constant current DC voltage supply by means of diodes, thyristors, transistors, or converters. This rectifying process can take on many forms with half-wave, full-wave, uncontrolled and fully-controlled rectifiers transforming a single-phase or three-phase supply into a constant DC level. We can use SCRs or other thyristors and convert the modified output from the transformer to DC voltage. The thyristors act as full wave rectifier and provide controlled DC output voltage. It is popularly used in grid-to-grid vehicle applications where it is used as a battery charging section and in case an AC supply is required, we can directly take the tapping from the inverter section. It can provide multiple opportunities to use the nature of supply (Both DC and AC)

Inverter :

The inverter is an electrical device that converts DC input supply to symmetric AC voltage of standard magnitude and frequency at the output side. It is also named as DC to AC converter. An ideal inverter input and output can be represented either in a sinusoidal and non-sinusoidal waveforms. If the input source to the inverter is a voltage source, then the inverter is said to be called a voltage source inverter (VSI) and if the input source to the inverter is a current source then it is called as current source inverter (CSI).

A full bridge single phase inverter is a switching device that generates a square wave AC output voltage on the application of DC input by adjusting the switch turning ON and OFF based on the appropriate switching sequence, where the output voltage generated is of the form +Vdc, -Vdc, Or 0.

2.3 Full bridge inverter

2.4 Waveform of full bridge inverter

2.5 Capacitor:

The capacitor acts as a filter in this circuit. The capacitor increases the DC voltage and decreases the ripple voltage components of the output. Thus providing the output to be the smoothened DC<img width="974" height="248" alt="203495235-26716270-870e-4a5f-b92d-6fd815cd6a3d" src="https://github.com/user-attachments/assets/3e7a2b62-d190-480f-b11f-7c02ce26a9d9" />

3.4 Phase modulation : Phase-shift modulation is probably the simplest modulation technique for dual active bridge converters. It uses D1=D2=0.5 (i.e. 2-level switched voltages), reducing the degrees of freedom to ϕ only. The switched voltage and inductor current waveforms are depicted below: image

3.4 phase modulation waveforms Dual Active Bridge switched voltage and inductor current waveforms With this method, the power transfer between the primary and secondary has the following simple expression and has a maximum for ϕ=0.25. P=(nV1V2/(fswL)) ϕ (1−2ϕ) Some of the benefits and drawbacks of this method are summarized in the following table: Benefits Drawbacks Simplicity (1-D of freedom) Higher RMS transformer current Highest achievable power flow Limited operating range with low switching losses Due to a high RMS current (hence conduction losses), and high switching losses, phase-shift modulation cannot be used for high-efficiency applications. Nevertheless, the best ratio between transferred power and inductor RMS current is optimal when V1=nV2, making phase-shift modulation attractive when operated close to that operating point.<img width="800" height="378" alt="203495380-fc85fe76-db64-492b-a66b-ad467d2de468" src="https://github.com/user-attachments/assets/d796e91b-ae40-406f-a0ec-6bc547eee266" />


