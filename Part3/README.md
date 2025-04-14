# Analog Filter, Adder and Peak Detector

## Introduction
This module attempts to implement a peak detector circuit to get output reference voltage to drive the LED.

## Band-Pass filter
Analog fiters are used to pass desired frequency signals while rejecting others. For our project, the goal is to pass only a fixed frequency tone of the input to an LED Driver and a Class-D Amplifier at a later stage of the whole circuit.
A typical active second-order band-pass filter looks like this -
![image](https://github.com/user-attachments/assets/6e7a0200-a31b-4499-99fb-ccac3aab7a92)

## Adder
If you desire to pass multiple but specific frequency tones to your circuit, then you use multiple filters centred at different frequencies as desired and add the filter outputs. The addition can be done using an opamp based inverting adder.
![image](https://github.com/user-attachments/assets/8ecfddca-29be-4d2c-87cc-f902a81cb5f6)
For a general representation with different values of the resistors, one can achieve any linear combination of the two input voltages.  
Vout = -R3 * (Vin1/R1 + Vin2/R2) = - (R3/R1 * Vin1 + R3/R2 * Vin2)
We get an addition when R1=R2=R3

## Peak Detector
The AC output of the adder is converted to DC (which we finally desire for the LED driver) using a peak detector circuit.

The following circuit shows a simple peak detector:
![image](https://github.com/user-attachments/assets/e75f1bab-a8b8-443b-be1d-cddfbe490c52)

Consider the circuit without the capacitor C1. Initially Vin > Vout. Diode is in forward bias. Suppose Vin is a sine wave. Then, the output follows the positive half of the wave (slightly lower due to forward bias voltage of diode; ~0.7V). Then, Vout > Vin and diode is in reverse bias. Negligible current flows and the output is 0V. This results in Vout being a half-wave rectified sinusoid for a sine input at Vin. With the addition of capacitor C1, the output voltage doesn't porportionately fall with fall in Vin but is held constant by the capacitor. (there is be a slow discharge though, due to the RC discharge circuit). This gives some sort of saw-tooth liek waveform as seen in the image.

Note: The discharge of the capacitor helps in making a 'peak detector' than a 'peak holder'. It allows for new peaks to be detected. This is more important when the input signal can have varying peaks unlike a perioidic input wave we consider here.

![image](https://github.com/user-attachments/assets/70b2b2f6-91c9-429b-8dcc-5a9b3969850c)

The intiial RC High -Pass filter is added to the +ve terminal of opamp to remove an DC bias from Vin.

The choice of parameters R2 and C2 depend on desired behaviour. This provides a discharge path for the output voltage so that it can follow newer peaks. This implies a higher discharge is better to notice potential smaller peaks but peak nonetheless that may appear later. On the other hand, a higher discharge may cause higher ripple in the peak output. In our case, we desire a DC value as output to drive the LED. Generally, it is advisable to set the time constant to be 10 times the signal peak frequency.

Our actual peak detector circuit looks something like this:
![image](https://github.com/user-attachments/assets/4f8c2942-fd7b-4cba-8a53-d5db36101c7f)
We desire to modify Vpeak such that we get the Vref at required DC value and ripple tolerance- hence the resistive divider and low pass filter.

