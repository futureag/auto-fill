# auto-fill
Code for MVP reservoir filler
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
