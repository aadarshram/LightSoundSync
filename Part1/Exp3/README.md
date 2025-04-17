# Compensator and Module Integration

## Introduction

The circuit made thus far has a poor phase margin (PM) which may lead to instability. To improve stability we add a type-1 compensator for dominant pole compensation (addition of a new dominant pole). Then, the complete feedback system looks like the following:

![image](https://github.com/user-attachments/assets/43bb6262-c8db-49af-beb6-8f3dd033c742)

The value of Vref controls the current through the LED.
Iled = Vref/Rsense

To analyze the stability, one can draw the bode plot of the loop gain. We break the circuit at Vout for this purpose. A good system is stable with PM > 60 degrees with real-circuits.

## Specifications
- Iout = 50mA
- Rsense = 5ohms
- Inductor (L=100uH): RCH875NP-101K
- LED: 151053YS04500
- Sense Resistor (RSENSE=5Ω): MOSX1CT52R5R1J

  Hence, Vref = 250mV.

  **Choosing values for R and C in Compensator**
  One can write the loop gain and apply PM>60 degrees to get an inequality condition on the product RC. (Check notes)

  Note: Sometimes, these values wouldn't work due to real-world components.We use C=25nF and R=10k ohms to get a stable output current 50mA after transients.

## Experiment
1. Vref when set at 250mV results in Iout=50mA.
![image](https://github.com/user-attachments/assets/441986d5-77ac-4f08-954a-8a831c666021)

2. AC response- stability analysis??
3. 
