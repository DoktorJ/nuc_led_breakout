# nuc_led_breakout
Dual RGB LED breakout board for NUC 7/8/10

![Board layout](https://i.imgur.com/WTqZNzC.png)

Author assumes no liability for any damage that may arise through your production, assembly, or use of this board,
whether to the board, to the NUC, or to anything (or anyone) else!

## License
The design and use of this board is licensed under the [Creative Commons Attribution-Sharealike 2.0 license](https://creativecommons.org/licenses/by-sa/2.0/)
(cc-by-sa-2.0) license.

## Intent
This board is for debugging the RGB headers on a NUC10. Attaches via a short Molex Picoblade 4p pigtail.
Dual RGB LEDs mount at each end for redundancy and visibility, with individual current limiting resistors for each element of each LED.
This board may not be suitable for use with the NUC enclosure assembled due to through-hole parts with exposed metal points; attempt this at your own risk.

## Connection
The NUC header consists of a 4-pin 1.25mm pitch connector; pin 1 is +3VSB, and with 2, 3, and 4 sinking red, green, and blue respectively.

## Parts selection
Since the NUC has a common +3V power source, this design takes the simplest adaptation of that and is made for a common anode RGB LED. Since pinouts may
vary by LED, be aware that the board is designed for this specific pinout:

    1. - Green
    2. - Blue
    3. + Common
    4. - Red
    
Be aware that some RGB LEDs reverse the pins for green and blue. If you use one of these LEDs the circuit will still technically work, but the
colors will be reversed (green<->blue and magenta<->yellow; red, cyan, and white will work correctly). An RGB LED with the anode at pins 1 or 4
will NOT work (and may or may not let the magic smoke out).

Beyond that, you will need to do the math for your LEDs and their resistors -- check the LED's datasheet. In most, the green and blue elements will
have a _Vf_ greater than 3V and thus technically will not need resistors; you can shunt them with bare wire, but a low-resistance (<10Ω) resistor
shouldn't affect brightness significantly while providing a bit of protection. The red element almost always has a _Vf_ *below* 3V, so calculate

> (3 - _Vf_) ÷ _If_  (remember, _If_ is in amps, so 20mA = 0.02A)

and round up to the nearest available value.

Note that the resistors are paired; R1 and R4 should have equivalent values (assuming the two RGB LEDs used are the same), as should R2/R5, and R3/R6.

Lastly, the connector is Molex p/n 0530470410 . For the most part, any 1.25mm pitch 4-pin header should work, but the Molex Picoblade jumpers
(e.g. 0151340400) fit the NUC header, so it makes sense to use the mating male header on the board barring availability issues.

## Usage

After assembling the board, take an appropriate Molex Picoblade pigtail and connect to your board. Note which side plugs into pin 1 (the end closest
to the "J1" identifier; appropriate "1" mark coming in a future release), it may help to mark the pin 1 connector on each end of the pigtail with a
permanent marker.

Flip your NUC over and take off its bottom plate. Now, depending on your NUC model, the RGB header will be in different places. Be aware the header
may be occupied if an external LED (e.g. ring on NUC 7) is connected, and would need to be disconnected. Find pin 1 of the header, and plug the
pigtail into the header.

Enjoy, and don't brick your NUC!
