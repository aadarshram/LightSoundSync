# H-Bridge Driver and Integration

## Introduction
The H-Bridge Driver is the output stage of the Class-D Amplifier module and is key to obtain good efficiency. The driver basically amplifies the PWM input (from Exp4) and delivers the differential amplified outputs to the speaker.


![image](https://github.com/user-attachments/assets/d40b8f63-bcb2-472b-9373-1afcb72a2d59)

The driver is made using a switching circuit implemented using npn and pnp transistors and driven with CMOS inverter buffers. To limit the base current, we use a few (k Ohms) resistance. The switching behaviour is when the transistors are in the cut-off and saturation mode. If you find that the transistor isn't saturating, one can reduce the base current.

Note: In order to ensure we don't short the two switches simultanously causing a large current to flow, a non-overlap clock generator is used. This enforces a 'deadtime' between the two switchs' operations preventing such a situation.

To model the speaker for simulation testing, one can use a combination of resistors R = 32 Ohms and L = 100uH.

## Specifications
- Use CD4069 inverters and SN74AhC00N for NAND gate.
- Use 2NXXXX series for the BJTs.

## Experiment
The LTSpice schematic is the following:
![image](https://github.com/user-attachments/assets/6cc8de2e-9d7e-443c-8e73-e966a8e88167)

1. In simulation, the inductor current should be the average of the differential output voltage divided by R=32 Ohms.
![image](https://github.com/user-attachments/assets/a78f2146-31d9-4dbe-aeef-69f2594a6fbc)
This does look like what one might expect if he plots out the graphs. (Check notes)
