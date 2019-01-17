# auto-fill
Code and instructions for the MVP reservoir filler
Date: 1/17/2019
Author: Howard Webb
Description:
A relay is used to control a pond pump that moves nutrient from a 5 gallon bucket to the reservoir.
Activiation of the pump is determined by water level, which is judged via electrical conductivity.

# Parts:
- 5 gallon plastic bucket (used to mix and store nutrients)
- 1/2 inch black plastic hose (black prevents algae growth)
- 90 degree 1/2 elbow (used to direct flow into reservoir)
- [440 gph (gallon per hour) pond pump](https://www.amazon.com/gp/product/B01LHC8UX8/ref=ppx_yo_dt_b_asin_title_o04__o00_s00?ie=UTF8&psc=1)
- [ADC Converter](https://www.amazon.com/HiLetgo-Converter-Programmable-Amplifier-Development-x/dp/B01DLHKMO2/ref=sr_1_2?s=digital-skills&ie=UTF8&qid=1547735402&sr=8-2&keywords=ADC+chip)
- [moisture probe](https://www.amazon.com/HONG111-Sensitivity-Moisture-Arduino-Watering/dp/B01NCI629O/ref=sr_1_5?ie=UTF8&qid=1547734531&sr=8-5&keywords=arduino+moisture+probe)

Though I just saw this, and it may be a good alternative

- [avoids building your own probe](https://www.amazon.com/Fevas-Moisture-Detection-Corrosion-Resistance/dp/B07MKCX1NZ/ref=sr_1_3?ie=UTF8&qid=1547735325&sr=8-3&keywords=arduino+moisture+probe)


If building your own probe, you will need from the hardware store:
- 2 1/8 inch stainless steel threaded rods
- 4 stainless steel nuts (1/8 inch)

# Software
Relay.py should already be in the MVP code, so you need to add only three more files:
- Reservoir.py - the actuator logic 
- Pump.py - proxy for the pump (controls the relay)
- EC.py - reads the EC (moisture) sensor

The code assumes:
- You wire the pump relay to the Raspberry Pi GPIO #35.
- A fill time of 4 seconds, and timeout of 10 seconds. The 440 pump is a fast fill; if you use a different pump, you may need to adjust these parameters.


# Hardware
Below is the wiring diagram for this project.  Ignore the SI7021 sensor on this diagram.
![Fritzing Diagram](https://github.com/futureag/auto-fill/blob/master/images/MoistureProbe_bb.png)

# Construction
If you bought the cheap moisture probe, you will need to build a more robust sensor from the stainless steel rods.  Basically you mount the rods into a block of plastic (I used an old cutting board).  Drill two 1/8 inch holes about 3/4 inches apart and screw in the rods.  Solder a loop in the wire (so it doesn't slip off later!), then clamp the wire loop between two nuts.
![EC probe](https://github.com/futureag/auto-fill/blob/master/images/EC-sensor.jpg)
It may be cheaper and easier to buy the fancier probe - though I have not tested it to see how well it holds up over time.

# Instructions
- This assumes you have a relay wired up 'normal off' with 110 V for the pump.  When working with 110, I advise you to enclose the relay with an electrical outlet in an outlet box to avoid the risk of shock.  This should be connected to a GFI controlled power source.
- Copy the python code to /home/pi/MVP/python
- Build the circuit (I use a breadboard)
- Connect the tubing to the pump, and put the elbow on the end (heat the tubing in hot water so the elbow fits in easier).  Zip tie the elbow to the reservoir (you want a filler, not a fountain!)
- Place the bucket on the floor near your MVP, fill the bucket with nutrient, place the pump in the bucket.
- Plug the pump into the relay outlet
- Modify cron to call ```/home/pi/MVP/python/Reservoir.py on a regular basis (once an hour)```

```15 */1 * * * python /home/pi/MVP/python/Reservoir.py >> /home/pi/MVP/logs/cron.log 2>&1```
