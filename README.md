# Class-A headphone amplifier
Simple class A headphone amplifier, made to be easy to build and understand while still sounding great.
The amplifier exclusively uses through-hole components, it doesn't use any integrated circuits and it uses standard values wherever possible.

## Design Philosophy

The amplifier is designed around a simple resistor-coupled class A output stage.
I like the appeal of the simplicity of resistor-coupled output stages and it allowed the amplifier to only have one high-power active device per channel which then could be displayed.
The power-transistor is an MJ2955, chosen for its TO-3 package which I really wanted to include as a center piece of the amplifier.
The transistor comes in one format, where its collector is connected to the case of the transistor. This, in combination with its place in the schematic allows it to have a grounded case, meaning it can be put on display on the outside of the case without any danger to the user.
Unfortunately, the MJ2955 struggles to keep up with fast rise- and fall-times, which led to problems outlined in the performance section.

Preceeding the output stage, a fully discrete pre-amplifier was created to keep THD at a minimum.
It is constructed like a discrete opAmp, with a differential input section and a voltage-amplification stage that then feeds the power-stage.

The output stage is connected to the amplifier's output through capacitive coupling and a delay-board. This delay board keeps the output of the capacitors connected to ground through resistors for the first ~4 seconds, allowing the output capacitors to slowly charge. This means that the output of the capacitors are at 0 V it connects to the headphones, which avoids a "thump" when turning the amplifier on.

To keep complexity at a minimum, the amplifier is powered from a single power supply of 24V, created by an external DC power-brick.
This was done to avoid working with line voltage, keeping the amplifier safe to operate and build up for hobbyists.
The input voltage is filtered by a passive power-supply. This, again, is a nod to vintage amplifier designs and was chosen for simplicity and to avoid having more power-semiconcutors in the regulation path of the power supply boards.

## Construction

As the amplifier is constructed from separate boards, a 3D printed case was designed to screw the boards onto one single frame.
From there, they could be connected to complete the amplifier.

The case additionally houses the power- and output-switches, a potentiometer for regulating the signal coming into the amplifier and connectors for the headphone, the inputs and preamp-outputs and the power-connector.

## Performance

The amplifier works as intended and amplifies the input signal properly. The sound is okay, but heavily compromised by massive noise coupling into the output signal.
This is probably due to the wiring on the bottom of the amplifier, which brings sensitive input audio signals in close proximity of large voltages and currents of the power-supply lines and output signals.
The 3D printed case does not shield the amplifier at all, meaning that even a mobile phone's RF pings were audible loudly.

The amplifier's output-stage is limited by the slow slew-rate capability of the MJ2955 transistor. This can even be seen in the simulations, as the preamp spikes to the positive supply voltage at fast positive edges on the input signal. The MJ2955 can not switch off as fast as the preamp-section commands it to, leading to the preamp to rise positive more and more. In the simulation, replacing the MJ2955 BJT by another BD140 solves this problem completely, indicating further that the MJ2955 is to blame.

Finally, the amplifier gets very hot during operation. Initially, a 500 mA bias current through the output stage was targeted, which would have meant a 22 Ohm power resistor in the output stage. The resistance was increased to 33 Ohms due to thermal concerns and even the 33 Ohm resistor (albeit only cooled convectively) gets far too hot to touch during operation.

All in all the amplifier shows a stable operation without any unexpected oscillations or other fatal flaws. The circuit works, but has weaknesses which make it impractical in a more refined setting after the prototype stage. For this reason, a next iteration may be modified quite extensively, on the basis of the present design.

## Next steps

To adress the noise issue, the next iteration will be build as one single PCB with a continuous ground plane.
A solid case constructed of metal will provide good cooling and shielding from interference from outside signals, allowing for quiet operation and keeping the case- and amplifier-temperature in a safe region.
A thermal safety switch or electronic NTC-control circuit may be implemented for furhter safety.
The output stage will omit the MJ2955 BJT and switch to a BD140. Additionally, the resistor-coupled output stage may be exchanged in favor of a current source or even transition to class AB for more power and cooler operation.
The power-supply will most likely laso be regulated. Without the MJ2955, the argument of having only one high-power semiconductor device is moot, so a simple regulator circuit may replace the hard-to-get and unprecise LC lowpass filter.

The amplifier will still be fully discrete, fully thorugh-hole mounted and fully open-source. I really want to create something which is usable every day though and the steps above feel adequate for that.
