# Power Stage and LPF

## Introduction
![image](https://github.com/user-attachments/assets/aef75a6f-526e-44bf-abb8-b7b26c837c1a)

The power stage is used to allow more current through the LED in the driver since the opamps cannot source high current. To this end, we use a gate driver with power MOSFET switches followed by a low pass filter to provide the DC output Vout with higher current. The non-overlap clock generator is used to ensure a small delay (called deadtime) between switching on of one of the MOSFETs and switching off the other. This is because there will be a huge current through the circuit (short between VCC and GND) in case both are switched on the same time and it will damange the circuitry.

The deadtime can be varied using the capacitors Cp and Cn. Considering a discharge circuit of the capacitances with the inverter's resistance, it can create a time difference between the two inputs as to when they cross a threshold voltage which is effectively translated to deadtime after passing through digital gate, NAND.

## Specifications
- NAND Gates: SN74AHC00N or equivalent alternate part
- Inverters: CD4069UBE or equivalent alternate part
- Gate Driver: TC427EPA or equivalent alternate part
- Power MOSFETs: IPP45P03P4L-11 (PMOS) and NTD3055L104-1G (NMOS) 
- Inductor (L): RCH875NP-101K (100µH) or equivalent
- Capacitor (C): 47µF

## Experiment

![image](https://github.com/user-attachments/assets/0ffc4462-2484-4394-a7af-cef06efc185d)

1. As mentioned before, there needs to be a non-overlap deadtime between the PWM signals to ensure no shorting for safety. The figure below shows the non-overlap region.
![image](https://github.com/user-attachments/assets/6ed76f7f-2f3b-46d3-a2ba-ce7cf96ccc86)

2. Vout will be approximately the average value of the PWM signal proportional to Vctrl (Since Vctrl adjusts the duty cycle).
![image](https://github.com/user-attachments/assets/dcf1cd15-6f93-4c76-8d0d-15fb111221de)
The above graph is for Vctrl=2.5V.

3. The voltage Vout drops if you load it. (Say, add a load of 1kOhm after the LC filter)
![image](https://github.com/user-attachments/assets/0f67bdb9-9a4a-4148-8218-6e58cbe56199)

