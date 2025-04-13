# BandPass Filters
## Introduction
This part of the circuit is used in combination with the peak detector (Exp7) for finding the amplitude at desired frequecies of interest. To that end, this circuit implements two band pass filters, one centred at 1kHz and another at 3kHz. The goal is to respond to the desired frequency tones and reject the rest from an input fixed frequency signal. The circuit diagram looks like the following:
![image](https://github.com/user-attachments/assets/dc9cf651-0d14-4494-8ef6-0265074094a9)

A fixed-frequency tone input Vin_audio passes through two active band-pass filters implemented using opamps as shown. The outputs Vout_bp1 and Vout_bp2 are the filtered version of the input.

## Specifications
- MCP6004 for Opamps
- Common mode offset, Vcm = Vdd/2 = 2.5V
- Band-Pass filter Gains, Ao1=Ao2=1
- Band-Pass filter Q-factors, Qo1=Qo2=10
- Center frequencies, fo1=1kHz; fo2=3kHz.

One can work out the expressions for gain, quality factor and natural frequency for the filters. (check the note attached)
The final expressions are as follows:  
A0 = R2/2R1  
$w0=(R1+R3)^{0.5} / C*(R1R2R3)^{0.5}$  
$Q0=(R1+R3)^{0.5}* (R2)^{0.5} / 2*(R1R3)^{0.5}$

Choose values approproiately as per the expressions and component availability. There might be a compromise to be made in some terms.
We've chosen the following values for simulation:
R11a=220k R22a=430k R33a=1.2k Ca=2.2n R11b=200k R22b=400k R33b=1k Cb=7.8n.

Note: Due to other real-world effects, one might need to tweak these values to get desired output. One way is to adjust R2 and C to balance gain and frequency to match specifications.

## Experiment
The following image shows the LTSpice circuit:
![image](https://github.com/user-attachments/assets/40cda320-4243-475c-bbec-31d15dd38eb8)

1. If you input Vin_audio as a sine wave of 1kHz frequency and 0.45 amplitude (0.9x that of Vramp in Exp1. Why??), the filtered output should be observed according to each filter present.
![image](https://github.com/user-attachments/assets/9259e6e9-24f3-4fe8-9483-052600176343)
- Note: The amplitude follows that of input signal since gain is 1. (Practically, it reduces a bit.)
2. Repeat the same for Vin_audio at 3kHz.
![image](https://github.com/user-attachments/assets/4288747c-f73a-4e73-814b-8d10403d527d)
3. Sweep the input frequency from 100Hz to 5kHz. This can be done by applying AC 1 at input voltage. The filter outputs should peak only at respective center frequencies.
![image](https://github.com/user-attachments/assets/e5e3d9b6-bacd-4df8-b724-8e4bb30c5baf)
The peaks are approximately at the desired center frequencies.
Note: I suppose due to the simulated real components, exact outputs are not achievable through tweaking values. Even the gain is behaving weirdly. (Why??)

Note: In breadboard implementation, the frequencies may go off further owing to the tolerances in resistors and capacitors.
