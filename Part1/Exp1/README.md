# Ramp Generator and PWM Modulator

The Ramp generator is basically an oscillator made using combination of Opamp RC Integrator and Schmitt trigger. The integrator integrates a constant signal to get a ramp which switches slopes at every edge of the schmitt trigger thereby creating a triangle wave.
The PWM signal is created by comparing the triangle wave with a reference (Vctrl). Adjusting Vctrl changes the duty cycle of the PWM.

The circuit diagram looks like this:
![image](https://github.com/user-attachments/assets/1c49814b-a007-4934-bdd8-dd79149c03cd)

Vcm is basically the DC offset about which the AC signal oscillates. Ensure same Vcm as input to OPA1 and CMP1. Before CMP2, we have a Cbias and Rbias supplied with Vbias. This is basically to kill the previous DC offset and load desirable one (Vbias, in this case). If Vbias is same as Vcm, it may not make any difference.

Note: Do not forget to connect a pullup resistor from the supplies to the output for Comparators. (??)
