# Automating a greenhouse/indoor garden at home

Maintaining a garden in a small apartment is hard; there's hardly any space for plants--let alone the inevitable mess that comes from dealing with soil, you're limited to container-friendly plants, and no matter how excellent your apartment's positioning is (southern exposure being best, but sometimes you don't want your blinds open), light is always a problem. So what's someone with a desire to grow their fresh herbs or other plants to do? Optimize!

Note that this is not yet touching on hydroponics. That's a whole different set of interesting questions to ask at some later point.

## Prior art

Of course, this is not a new problem. There's in-market solutions for growing herbs under full-spectrum lights; [AeroGarden](https://www.aerogarden.com/indoor-garden-comparison-chart) is a big name in that. So what can some hackers at home do that a commercial venture can't? Mostly, learn more about what your garden is doing, when, and own the resulting data. Plus, if you don't care about looks, you can be way more efficient with your lights and pick just the spectra the plants need.

## Variables in gardening

### Light

Plants require light--but not just any light, there's specific frequencies that sunlight offers which normal interior lighting doesn't. This is often why houseplants look wan compared to their exterior counterparts. To ensure that we're getting the correct light frequencies, then, we need to look to either _full-spectrum_ lighting, or plant-specific lighting. This way, plants will be able to optimally grow in otherwise inhospitable conditions. Additionally, different plants have different light level requirements; shade, partial shade, or full sun.

### Soil humidity

Plants almost exclusively acuqire water through their roots, and some require more humid soil than others; that being said, plants shouldn't be left drenched, nor dried out; in the first case, their roots will rot, and in the second, the plants themselves will dehydrate; in either case, the end result is a dead plant. Normally, a gardener checks soil conditions and waters as necessary, but this could potentially be improved as well

### Soil composition and nutrients

Soil is a mixture of carbon and nitrogen sources--sphagnum moss, decomposed plant matter, charcoal, other amendments that form the basis of the soil--as well as micronutrients: plants require calcium, iron, manganese, and a litany of other elements that are only needed in (often) microscopic quantities, but without them the plants will suffer. There's other components, too; moisture retaining materials, aeration improvers, worms and grubs. For container gardening, there is little in the way of active soil biome, but the micronutrient load is often provided by pre-mixed soil, but amendments are available.

The other aspect of soil composition to consider is its pH level; different plants require different degrees of acidity or alkalinity. Each plant you want to grow will have different requirements, and will need to be managed differently. The details of this are beyond the scope of this paper, and should be handled on a case by case basis; see notes from a state university extension service for more details.

### Air movement

Plants should ideally get some air movement. They don't necessarily need a cyclone, but having some motion is better for them.

## Options for automation and first steps

### Lighting

For indoor gardening lights, there's an entire industry around producing Red-Blue lights with a mix of IR, UV, broad-spectrum, and focused red and blue LEDs, all on an E26/E27 mount. Examples abound on [AliExpress](https://www.aliexpress.com/item/120-LED-Full-Range-of-Plant-Lights-80W-E27-Led-Grow-Plant-Light-Plant-Bulb-Full/32836019814.html), or from US-based vendors like [Lush LED Lighting](https://lushledlighting.com/), who target a different specific market than I do--of course a lot of this stuff also looks like a grow-op. Hazards of the occupation?

The really easy task is automating turning lights on and off; that's accomplished with a relay and a bit of logic around timing; that can be accomplished with an ESP8266, based on the Arduino NTP project. As for what lights to automate, I'm currently testing some plant growing-oriented lights with a selection of frequencies that they focus on; specific red, blue, IR, and UV LEDs intended to promote specific traits when growing plants. [AliExpress](https://www.aliexpress.com/item/120-LED-Full-Range-of-Plant-Lights-80W-E27-Led-Grow-Plant-Light-Plant-Bulb-Full/32836019814.html) has a bunch of vendors selling similar lights; they're all very similar designs.

Lights will generally not exceed about 18h in a day; plants do need some time off, and most of these lights have limits mentioned where they should be turned off after a certain amount of time, so we'll aim to automate that too.

### Watering

Watering will involve monitoring soil humidity, and having some method to add water in a way that hydrates the whole vessel -- not just one spot.

For monitoring soil humidity, there's a few options. Mostly they boil down to resistive or capacitive monitoring; capacitive sensors cost a little more (not if you're buying from [AliExpress](https://www.aliexpress.com/item/NEW-Capacitive-soil-moisture-sensor-not-easy-to-corrode-wide-voltage-wire-for-arduino/32832538686.html), but certainly if you're ordering from local sources) however they won't wear out as rapidly, since there's not direct contact with the moisture in the soil. Andreas Speiss points out that the capacitive ones should be plastidipped along the sides, since there's just fibreglass PCB material there which will wick moisture into the sensor.

### Fertilizing

Harder to automate than other steps--and harder to determine when it should be done. Sensors for this are cost-prohibitive, if they exist; manual testing on a regular basis (or just ... ignoring it for a long time ...) is an option.

## Starting points

This project has two major goals: grow some herbs, and generate useful data to explore and improve. The second goal rather implies the first, of course.

### Lighting controlled and reported over wifi

This system should announce state changes, or at least make them available over wifi. Consider MQTT topics and posting, with some service aggregating posts to track lighting over time.

### Drip/pump based watering to manage humidity

After getting soil sensors and setting them up to track the humidity level, we can start working on automating watering. Over on [Instructables](https://www.instructables.com/id/Automatically-water-your-small-indoor-plant-using-/) there's a project that does more or less what I'm looking for, although it appears a little more forceful than the approach I want to take.

The specific watering mechanism I'd like to see is tubing buried around the perimeter of a pot with perforations allowing water to seep out.