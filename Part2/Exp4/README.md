# Single ended-to-differential input converter and PWM modulator

## Introduction

![image](https://github.com/user-attachments/assets/db972a3c-1b2f-41df-8e8d-3b6505dd37dd)

In this circuit, we attempt to get a differential PWM modulated signal out of a single ended AC input signal.

## Single Ended-to-Differential Converter

The single ended-to-differential converter converts an input signal into two with opposing phases. We need this to drive the speaker using differential inputs which has its own advantages (??) over using a single-ended input to drive the speaker. To this end, the inverted signal with opposite phase is achieved using an opmap based inverting amplifier of gain -1.
![image](https://github.com/user-attachments/assets/ea125ff2-c46c-4999-b45e-bddfe25ac3b0)
choose R1=R2 to get Vout = -Vin (with offset of Vcm, here)
The Cin in the beginning is an AC-coupling capacitor to remove DC components from the signal. We then, bias it around Vcm for our desired DC operating point. The value of Cin must be large enough so that there is little to no attenuation in the AC signal passed through it while effectively blocking DC.

## PWM Modulator
The PWM Modulator is simply implemented using a comparator comparing against the ramp signal (obtained from Exp1). Since we input sinusoidal signal, this would modulate the ramp to result in a PWM signal whose duty cycle varies sinusoidally in phase with the input sin. We repeat the same for both the differential inputs.

## Specifications
- PWM frequency = 100kHz
- Use LM339 comparators and MCP6004 opamp.

Note: Do not forget to add a pullup resistor to the comparator. The LM339 is an open-collector comparator. That is it an only pull low. For high output, it will float without the pullup resistor.

## Experiment
Here is the LTSpice schematic:
![image](https://github.com/user-attachments/assets/545a0e49-f39e-44ae-a505-6e7b40803144)

1. When input a sinusoid of frequency 1kHz and amplitude 1Vpp, the outputs of the differential converter should be two sinusoidal waves, completelt out-of-phase and with same amplitude as input sine wave.
![image](https://github.com/user-attachments/assets/095d800c-fe11-47c9-a959-045c2081470b)
2. The duty cycles of the PWMs should vary sinusoidally and for the differential PWM outputs, the duty cycles of both always add up to 1. (ie, D1 = 1- D2)
![image](https://github.com/user-attachments/assets/edec2df8-e5b6-44e0-87c1-262cab8ba0ba)
![image](https://github.com/user-attachments/assets/926a94ac-6806-45de-a7ba-3c17cba6b83d)
3. To verify one last time, you can add an RC filter at the PWM outputs with a cut-off frequency at 10-20kHz. This should bring you back closed to the input sninusoidal shape (with a little effect of the ramp also. To get a good sinusoid back, tune the cutoff-frequency accordingly)
For R=100k and C=0.5n, you get the following output, confirming our intuition.
![image](https://github.com/user-attachments/assets/88b4ec82-ec20-43b3-a68b-ecf3aa98e920)
