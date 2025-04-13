# Adder and Peak Detector

## Introduction
The objective of this circuit is to add the band-pass filtered signals (from Exp6) and convert it into DC using a peak detector.
![image](https://github.com/user-attachments/assets/594401d7-761f-4512-be77-199536107a84)

The circuit is a cascade of the adder and peak detector. Given input signal (Vin1 and Vin2) which are the outputs of the band-passed sine wave of a certain frequency, the first part of the circuit adds them up using an opamp based adder circuit. A common mode offset of Vdd/2 is also set. (Why?)
Then, the resultant signal is passed through a high-pass filter that removes the common mode bias in the adder output which is then input to a peak detector.  
The peak detector is a rectified voltage follower. In the circuit, the output Vpeak tries to follow the input signal as long as the diode attached is in forward bias. If one works it out, he finds that this is true at the rising sections of the input signal. When the diode is in reverse bias, the voltage is held and slowly decreased by the discharging capacitor circuit attached to the output node, Vpeak.  
We desire a DC output Vref for our purposes. A resistive divider followed by a low-pass filtering section can be visualized from the circuit diagram for this purpose. The resistive divider adjusts the mean value to the outcome desired while the low-pass filter further removes the ripples from Vpeak to get output Vref.  

## Specifications
- Max pp ripple at Vpeak = 100mV
- Max pp ripple at Vref = 10mV
- Max pp amplitude of Vin1 and Vin2 = 0.9 Vm (pp of ramp in Exp1) [taken care of in input of Exp6]
- Max vaue of Vref = 250mV

We use MCP6004 opamp and 1N4148TR diode for the rectification.
One can work out the values for each of the components using the given specification. (Check notes)
We finalize on values as follows:
 R=100k, R1=100k, C1=100n, R2=400k, C2=5nF, R3=500k, , C3=5nF.
This was based on theoretical calculation + tweaking in sim to satisfy the amplitude mean and ripple threshold.

## Experiment
The LTSpice schematic looks as follows:
![image](https://github.com/user-attachments/assets/803c36af-e4bb-4ab8-81bc-c88309ba6d87)
1. When input a sine wave of amplitude 0.9 * Vm and 1kHz/3kHz frequency at Vin1 and Vin2 (or output of Exp6), the adder should result in an inverted addition of the two signals.
![image](https://github.com/user-attachments/assets/165a900f-a83e-449d-b5bc-11fdc3e9c04b)
2. After the adder, the high-pass filter should remove the DC bias.
![image](https://github.com/user-attachments/assets/06a2c889-bd8a-4888-b25e-0ed43b95021d)
3. The mean value of Vpeak would be approximately same as input Vin_ac (=450mV) but slightly lower because of charging of the capacitor circuit. Here, it is around 400mV. The peak-to-peak ripple is 88mV which is within the maximum threshold of 100mV.
![image](https://github.com/user-attachments/assets/3675690c-0579-420f-a393-2f57b51850a0)
4. In case of Vref, the average is around 218mV (should be less than 250mV threshold) and the ripple is around 5mV.
![image](https://github.com/user-attachments/assets/f9c94799-427e-42ff-a30c-c385431b458d)
Note: We try to have a margin below the threshold because when all modules are connected in the circuit, some values might increase.
5. When swept across multiple frequencies, Vref should be high only at 1kHz and 3kHz frequencies and almost zero everywhere else. (My plot right now does not have significantly lower values at other frequencies. Work in progress.)
