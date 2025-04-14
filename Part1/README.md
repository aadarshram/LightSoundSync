# DC-DC Converter Based LED Driver

## Introduction
The objective for this part of the circuit is to light up an LED based on some control. However, a key challenge due to LED characteristics is that even a small change in voltage leads to significant changes in current through it (exponential I-V characteristics). In order to protect the LED (higher current than rated may damage the LED), we need to maintain a stable voltage achieved by voltage regulation.

### Voltage Regulation
This can be divided into two types- linear and switching. 

**Linear Regulators**  
On a high-level, how does this work?   
You have a switch which controls current passing through it from input to output using an opamp feedback system. The opamp drives the switch based on the feedback received from output voltage compared to a reference voltage and the switch appropriately lets more current flow or less to adjust the output voltage back. Linear regulators are simple, low cost, small, fast but however, the linear regulators dissipate a lot of power (Vin >> Vout) and hence are inefficient.

**Switching Regulators**  
In this case a switching element is used to convert input voltage to desirable output by rapidly switching between on and off creating pulses of power. These pulses are filtered using low-pass filter to get regulated DC voltage. The key advantage is that they do not dissipate much power as heat (ideally, switches dissipate zero power) and hence are more efficient.

Switching regulators or dc-dc converters are often preferred over linear regulators due to higher efficiency.

## Working principle
Switching regulators work on the principle of Pulse Width Modulation (PWM). The basic idea is to control the output power by means of the duty cycle of a periodic pulse signal.

Vout = D*Vin (for derivation of all expressions, check notes)

Now, this will be sufficient (open loop control) if Vin is stable and constant. However, that is not the case. Source/Supply volatage can vary and hence, so can Vin. Thus, we need a closed loop system with negative feedback to regulate its value.
![image](https://github.com/user-attachments/assets/00d92965-76c2-4575-9b25-d12f46a87318)

Consider the block diagram of the switching regulator above. The goal is to maintain a certain Vout. This certain value is decided by the reference voltage Vref and gain beta.

Vout = Vref / beta

Controlling these will allow us to change Vout.

Now, suppose Vout is not what is expected by Vref. Then, the error difference is found, passed to a compensator which generates a control signal Vctrl that adjusts the duty cycle of the PWM appropriately. Point to be noted is that this PWM modulator that we build cannot supply high current for the load requirements. Hence, we pass this through a power stage and then low-pass filter the PWM signal to get our desired Vout. Thus, we notice the negative feedback loop for this circuit.

## Building blocks

### PWM Modulator
The PWM modulator is used to convert a control Voltage Vctrl to a PWM signal by comparing with a fixed frequency ramp signal. The duty cycle can easily be varied by varying Vctrl.  
D = Vctrl / Vm (to be adjusted for dc offset)

### Low pass filter
We use an LC low pass filter. Why 2nd order? We desire as pure DC output as possible. So faster roll-off. We need a very low loss low pass filter so that we can still deliver high load current. Ideal low pass filter is the best choice for DC-DC converter.

When there is a series resistance of inductor and/or an external load resistance, things change.
The series resistance is proportional to the damping factor. The load resistance is inversely proportional. Suppose, the load has high impedence, this implies poor cutoff in the filter.

**Choosing values for L and C?**  
The values are selected based on the switching frequency of the input signal and inductor ripple current. Choose such that the cut-off frequency is 50-100 times lower than switching frequency to minimize output voltage ripple. The inductance value is selected such that less current passes ensuring less power loss through its resistance and no saturation (saturation occurs when the current is large enough to align all magentic domains and henceforth the inductor acts like a short). However, this implies I need to increase inductance which increases cost for bigger area- trade-off.

The expressions for ripple current and ripple voltage can be derived. We notice that larger value of L and C ensures smaller ripples.

### Compensator
Because of the second order filter we used, we now have a 2 pole system which can lead to poor phase margin (PM). To make it better we compensate for it by either type-1 or type-3 compensation.

**Type-1 Compensation**
The key idea in this method is to move the other poles away from UGF by inserting a "dominant" pole way early using the compensator. Hence, the unity gain frequency will be much less than the poles effectively acting like a single pole system as far as we are concerned. PM improves. GM also improves. However, this reduces the bandwidth of the system and hence lead to slower responses. A way to do this kind of compensation is to use a single pole low pass filter or integrator to insert a dominant pole.

One can work out and compare the use of RC-filter opamp vs Opamp-RC integrator for the type-1 compensator. Although, the filter opamp provides additional control to reduce pole further, it comes at cost of decreasing DC gain. Hence, we use an Opamp-RC integrator.  
Note: An opamp RC integrator does not have a DC feedback loop. We must ensure this by some other means when connecting the whole circuit so that the operating point is correctly set.

**Type-3 Compensation**
Instead of trying to reduce UGF with a dominant pole, the idea here is to somehow cancel one of the poles using a zero. This also helps extend the bandwidth. We wouldn't go further into its working as its beyond current scope.

### Power stage
The high current complementary switches (power MOSFETs) is used to increase the power of the PWM since the PWM comparator cannot drive high current. To prevent short between switches, a nonoverlap clock generator is used. The capacitors attached can be adjusted to modify deadtime.

![image](https://github.com/user-attachments/assets/5be7ebf4-2522-4e2e-9fbd-4b7bc4858e9d)
Notice that the Vgate_n is never on while the Vgate_p is off.

Note: Other useful expressions to analyze the LED- Driver as whole can be found in notes.
