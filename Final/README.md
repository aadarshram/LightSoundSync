# Top-Level Integration
![image](https://github.com/user-attachments/assets/cb3185d5-d9e4-4d1e-8d29-8d805cf240a7)

The final circuit integrates all the modules designed during the experiments to build a complete system.

The workflow goes as follows. Given an input sine wave of any frequency, the speaker outputs audio in a proportinate pitch as sound and the LED glows if the frequency is close to 1kHz or 3kHz but minimal for any other.

Specifically, the input sine signal is first band-pass filtered to allow only 1kHz or 3KHz frequency signals to output Vout_bpi. (Depending on Q, the allowed range centred at 1KHz and 3KHz may vary) The filtered signals are then added (Vout_ad) and a peak detector outputs a voltage propoertionate to the amplitude of the adder signal (Vref). This voltage is used as reference to appropriately drive the LED in the LED Driver module modulating the current going through it. The adder signal is also input to the Class-D amplifier module which drives a speaker modulating the current through it similar to the case with LED.

## Note
- In order to prevent noise coupling between modules, one can use seperate Vdd and Gnd for each module instead of using one and shorting locally on the breadboard.
- Decoupling capacitros can be used between the local Vdd and Gnd pins to reduce noise levels.
