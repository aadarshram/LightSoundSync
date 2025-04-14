# Class-D Audio Amplifier
## Introduction
The Class-D audio amplifier, consisting of a single ended-to-differential converter and a peak detector, is basically a pulse width modulator followed by a switch that drives the speaker. The PWM modulated switching mechanism and differential drive is often chosen for its high power efficiency and robustness.

## Details
The PWM modulator gets you a PWM signal with a modulated duty cycle based on the inputs. This modulated output is then used to alternately turn on and off the output transistors as switching amplifiers to give the resultant signal. Sine the transistors are either fully on or fully off, they dissipate very little power. (for a switch, either I=0 or V=0; thus, VI=0 always) This way, you get high power efficiency.

**Note:** One needs to ensure a deadtime in the switching drivers. It should be short such that it causes low-distortion but long enough to ensure both transistors aren't switched on at the same time leading to a short circuit and huge current flows (shoot through condition).

![image](https://github.com/user-attachments/assets/56563313-a91c-40ac-805e-839695b5f3ee)
