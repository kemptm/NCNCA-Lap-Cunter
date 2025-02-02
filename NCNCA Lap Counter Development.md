# Development Journal

Some emails:

From Mike Hardaway 8/22/2023:
Hi Tim,

I don’t know if I told you, but it’s my intention, if the lap counter can be made to work, to donate it to NCNCA’s equipment stash, after I build a protective transport case for it.  Between Robert’s crew and some technophobic officials, it will get some rough handling at and between races.  It’s pretty important that it gets protection before being released to general use.

Good luck with the puzzle.

Mike

---

To Mike Hardaway 8/22/2023:
Hi Mike,

I've taken a first look at it.  It doesn't look too complicated.  The Arduino drives the relays, which power the segment set and reset solenoids. I need to look inside the Arduino to see if I can get it to barf out the code. The solar panel is controlled by a controller that can charge the batteries.  The box can also take power through another interface.  I haven't figured out the remote control or what the USB input is for. There are a few broken wires that I don't have any ideas about, yet. I'll have to find power supplies, but I probably have something that will work.

I will create a schematic of the thing as I figure it out.  

Before I try to apply any power, I'd like to figure out its current state. Can you remember in what way it is broken? Won't listen to commands? Segment failures on the numbers? Power supply failure? Short? Dead computer?  

Thanks,  
Tim.

---

From Mike Hardaway  8/22/2023:
Hi Tim,

If I remember right, it was accepting a number, then would click down once and freeze.

I think the remote control was for increment, decrement, double zero, and blank.

Mike

---

To Mike Hardaway 8/23/2023:
Did it ever work completely?

Tim.

---

From Mike Hardaway 8/23/2023:
I’m not exactly sure.  My son called me happily saying it was finished, then a while later called me again saying it had a problem. He flailed at it for a week or so then gave up.

------------------;

To Mike Hardaway 9/4/2023:
Hi Mike,

I haven't been idle on the lap counter.  I've been researching the components to be sure that I could replace one if it seems bad.  The Arduino seems to be a model that was discontinued some time before 2016 (How old is this thing??).  The good news is that the current model is pretty much a one-for-one replacement.  The solar controller, buck converter, relay boards and radio all seem to have equivalent models available today.  The stand out are the numbers themselves.  That technology is so obsolete that I can't even find any references to equipment that works that way. I'll have to measure .

I have been looking at the power supply.  As I have been documenting the circuit in a schematic I think that I can see a very good candidate for why the thing froze after a couple of operations.  The way the numbers are wired is that relays are picked for each segment of each digit set or reset.  Then all of the circuits are energized firing 7 solenoids at once.  This whole thing is driven from the 5 volt supply that serves the Arduino.  The 12V-5V converter can source only 3 amps.  Given the current draw of some or all of the relays and a solenoid for each segment of a digit at the same time, that thing has to be stressed, not to mention being subjected to the fly-back current from the coils. I'm not surprised that the Arduino lost its mind.  I think that I am going to separate the power supplies of the relays and solenoids from the electronics.  I'll probably have to beef up the converter as well.

The investigation goes on.

Tim.

---

Hi Tim,

Your diligence is impressive and your analysis of the NCNCA use cycle is inciteful. \[He means insightful\]

I had questioned the usefulness of the solar cell when my son told me he’d added it.  I think getting rid of it is fine.  

My memory makes me want to think these are 12v relays.  Is my memory not accurate?  

The battery system not only functions as a built-in UPS for the gadget, it also lets us use the counter when we mount it on a scaffold or other high point out of reach of available extension cords.  Furthermore, there are occasionally races at which there isn’t any available utility power or available generator output.  Having a battery power option, even if it’s an external source, can be very desirable. Also, the passive current draw on this gadget is potentially a bit lower than it would be on a counter with actively lit digits. If it’s possible to make the battery work, we should keep it.

An alternative use lifestyle might be for me to maintain the counter, charging it at home between races.  It might not make it to every race but it would be more available than it is now.

Another option is to add a battery holder for a stack of alkaline cells, preparing to replace batteries every few races.  (I have a pretty good idea how well that would(n't) work.)  

If we opt for wired-only operation, the power supply you found looks fine but the ad specifically says it does not have a cooling fan.  Does it require a passive cooling airway?

1st  priority is to get the counter increment/decrement function working.

2nd priority is to operate it with its functional wireless remote up/down button.

3rd priority is the battery power option.  

4th priority is the above by the 2024 Early Birds.  

Mike.

## 8/22/2023

Did some searching on 7 segment displays.  These solenoid-driven displays are totally obsolete.  No one seems to sell them any more.  I'll have to take the box apart to see if they have builder plates on the back.  I'll also need to see how the solenoids are wired.

I did some searching for the remote control of the NCNCA Lap Counter.  It's made by a Chinese company called ??? and sold by a company called SensorBoard. It can be bought on eBay for about $8.25.

## 8/25/2023

I have spent the last couple of days searching out the major components: Arduino, relay panels, Solar Charge Controller, DC-DC converter, radio remote control, batteries and solar panel.  Many of these parts are obsolete, but very similar things can be found.  The only things that I haven't found anything about are the numbers themselves.  I'll learn more as I work out the schematic.

## 8/26/2023

I imported and installed [[KiCad]], an electronic CAD program that I intend to use for the NCNCA Lap Counter. It'll take a bit of learning, but it will do things like produce a BOM.  Started the tutorial for it.

## 8/28/2023

I figured out how to create a new symbol in the [[KiCad]] symbol editor.  I created a model of the DC-DC voltage converter.  A few more symbols and I can start building the schematics for the counter.  I'm beginning to have a suspicion that the reason that this thing would freeze after a bit is that the power supply, in particular the 5V power supply isn't up to changing all of the segments at once.  The design has that the coils are picked for a particular digit and then _all_ of the solenoids are energized.  The 5V power supply is only good for 3 amps.

## 9/3/2023

I have entered symbols for all of the major components of the NCNCA Lap Counter. I'm ready to start the schematic.  Since I'll Probably scale the pages for 8"x11" paper, I'll have to do a hierarchal drawing.  Perhaps I should use 11"x17" and try to get it all on one page.

I spent some time looking at the NCNCA Lap Counter power supply.  It consists of two 12v batteries, a solar panel, which may or may not have a charging regulator in it, a solar panel charging regulator and a 12v-5v 3a buck converter.  Documentation for the components is sketchy.  I don't know whether or not the buck converter has a regulator on its output.

The 5v supply powers the Arduino, the relays, radio and the solenoids of the numbers. Every segment of the digits have two solenoids, one to set and one to reset. I notice that the wiring of the numbers is such that when a change is requested for a digit, it simultaneously fires some number of relays, which then fire solenoids. The circuit a solenoid, either a set or reset, for every segment of the number.

Looking back at communications with Mike Hardaway, he mentioned that after counting up and down a couple of times, the box would lose its mind and freeze.  I have a suspicion that by firing all of those relays and solenoids at the same time, the 5v power supply is getting overwhelmed and drooping the voltage.  That would cause the Arduino to lose its mind.

## 9/5/2023

I'm researching what I have to do to replace the battery charger and 12v-5v converter for something more powerful.  I'm also going to move the Arduino to 12v using the barrel connector to power the Arduino and the radio.  That will put it on the other side of the 12v-5v converter which may provide some noise immunity.

## 9/7/2023

In looking at the fact that I am going to have to rework the power supply of this thing, I started musing about the use cases.  The lap counter will be managed by Robert Leibold on behalf of the [[NCNCA]].  Here is what I imagine will be the sequence of events:

1. Counter lives in case at NCNCA's storage.
2. Counter transported to race.
3. Counter is removed from case and set up.
4. Counter is used during race.
5. Counter returned to case.
6. Counter transported to NCNCA's storage.

Notice that the only time that the device is receiving power, either by solar or from the line, is during the race. That will hardly be time enough to charge the batteries by the solar charger, which is only 1.5 watts nor through the solar controller, which handles only 36 watts when powered by another source (an arrangement of which I'm skeptical). The device will have to be externally powered, as the batteries will surely be dead.  Robert is simply not going to manage charging it ­-- He doesn't do it for the laptops or the UPSs. So, we are going to have to provide power to it at the races. That isn't really a problem, since we always (at least almost always) have power at the finish line to power the laptops.

Now, given that we have to power the device every time, what is the point of the batteries and solar charger?

I'm thinking of eliminating the 12v system entirely.  This would remove the solar cells, the solar controller, the 12v-5v converter and the batteries. I'd replace them with a double-output 5v power supply capable of supplying at least 10w.  I'll have to measure the current draw of the number solenoids to determine whether or not 10w is sufficient.  I have found one that will fit inside the case.  [Amazon Link](https://www.amazon.com/SHNITPWR-Converter-Adapter-Transformer-WS2812B/dp/B07TZ2TRRB/) I prefer that as it is more clean to handle than having a brick, since there will only be an external cord, which is more robust than a brick on a line.  If I have to size up to a supply that won't fit, then I'd go with a brick.

## 9/8/2023

I read Mike's reply and tested the connection of the number solenoids.  They are, in fact, hooked to the 12 volt supply.  That means that I have to keep the 12 volts in the system.  I thought about modernizing it and using Li-ion batteries.  They are much more energy dense.  I bought a 5200 mAh battery.  That should have the capacity of lasting for several days without recharging.  The down-side to Li-ion batteries is that if you discharge them too far, it wrecks them.  Further if you try to charge an over-discharged battery, it could catch fire.  I'll have to have circuitry that will detect low voltage and disconnect the battery from the load.  Further, I should have the device power itself down after it's been idle for a time, to prevent screwups such as not turning it off before storage.  I bought some supplies to help me with that.  I have to design the circuit, now.

## 9/11/2023

I think that I have a powering solution.  I'll have a relay whose switch will separate the battery from all of the power consuming equipment. A SP NO momentary button switch will bypass this relay powering the Arduino.  The Arduino on powering up will pick the relay and hold it such that the power continues when the button is released. That will cause some number of mA, I think around 71 to flow all the time that it is on. The other solution would be to use a MOSFET pass through with the Arduino holding the  gate active all the time.  That would yield a circuit with 0.2v drop from the battery power and may have a problem with the big current draw of the number solenoids.  I'm going with the former.  If the battery pack doesn't last long enough -- about 2 days in idle state -- then I'll get a bigger one.

The MOSFET idea isn't going to work out because all the circuits that I can find have some sort of voltage divider in them which would lead to continuous, though minimal, power draw.

I received a bunch of the items I need to build the new power supply.  I think that I am going to go with a toggle relay for the power supply.  That way there isn't any current draw or attendant heat while the system is operating.  The  "OFF" button will raise an input to the Arduino that will cause it to toggle the relay the other way. That will help make the buttons idempotent.

## 9/15/2023

I think that the next thing that I really should do is be sure that all of the number solenoids work.  That will be a little tedious, because I have to disconnect the common power buss from each one as I test it.  Slow, but necessary.  I have to finish cleaning up the workbench first.

## 9/18/2023

I've been thinking about the power surge when the digits are updated.  The current mechanism fires seven of the solenoids at the same time.  Between 1 and 8 of the other relays fire.  Those are powered by the Arduino.  I'm going to change that for sure.  The question is whether seven solenoids is too much for the power supply, which is about 1 amp at 12 volts. Looking at the battery description, it looks like it can handle 6 amps briefly.  Another thing that I notice is that it has its own over-discharge protection, so I won't need that extra board that I bought for that.  All I will need is the latching relay so that the Arduino can power everything down rather than run the battery down when not used.

Side thought: I might be able to use a single momentary power button to energize the latching relay to turn it on and off.  That would be in parallel to the Arduino. No, I think that I would rather have the two buttons be idempotent.  "On" turns it on or does nothing and "Off" turns it off or does nothing.

## 9/23/2023

I have nearly completed the schematic for the NCNCA Lap Counter.  I should add the terminal blocks though.  I'll have to create them as symbols. On the other hand, I might just make them dotted rectangles around all of the connections.

## 9/25/2023

Now I'm ready to test the segments of the digits.  If any of the solenoids that drive the digit segments is non-functional, the project is over.

I separated the inputs of the units digit and energized each of the solenoids.  They all work.  Now I need to do the same for the 10's digit.  If they clear, we are go for more work.

Given the arcs that I saw while energizing them, the solenoids obviously don't have back EMF protection, which will eventually fry the relay contacts driving them.  I need to put in diodes to protect the switches.  Have to work out where to put the diode(s).

## 9/27/2023

I  was going to build the power supply, but I found that I ordered latching switches for the on-off buttons.  I ordered new ones, and they will be here on Friday, along with flyback diodes.  

I probably shouldn't be, but I'm a little concerned about the fact that the common wiring for the solenoids all comes back to a terminal block.  I might try to remove the numbers to put the diodes close to the coils, but that would mean disassembling the whole thing, which I'm loath to do. I'm going to try to put the diodes at the relays closest, circuit-wise to the solenoids, even those relays won't be the switching relays that would be taking the arc.  I need to put a diode from each coil to ground. So, first experiment will be to add diodes, from my Arduino kit, if they are big enough, to the circuit to see if I can quell the arc.

Ordered some stuff, which won't be here until Saturday, which will be too late to work on it before trip.

Just read that the 8 relay board can sink 480 mA.  Two of those boards, switching all "88" would completely sink the 1A 12v-5v buck converter.  Adding the third relay panel, will save things.

## 9/28/2023

I had a thought last night.  I could create a crossbar switch for the segment solenoids simply by putting the digit select relay at the ground side of the segments rather than the power side.  It's like a row-column select where the power goes from the segment (row) select to the set/reset select to the solenoid to the digit (column) select to ground.  This allows for individual addressing of every solenoid.  Now I can save power by not energizing solenoids that wouldn't move the segments.  Have to draw this up.

## 10/19/2023

I started up work on the Lap Counter today.  I'm looking at making the flyback diode board.  I'm studying the KiCad board layout software.  I found that I can use that software to generate and get made a 2-layer board for about $5/sq.in. I could get 3 boards for $15. That could be easier than building a perf board. First I have to learn how to use the software.  I drew the schematic of the board.  Now to do the layout.

## 10/20/2023

Worked more on the Lap Counter. I have the flyback diode PCB  pretty well laid out.  Now I have to route the nets.

## 10/21/2023

I finished routing the nets and generated Gerber files.  I know that I want to add a via for the common side and place mounting holes.

## 10/22/2023

I finished the flyback diode layout.  Depending on whom I choose to do the build, it will cost me $20-$25 for 3 boards.  I received the A27 battery for the remote control.  I had never heard of that one.  It's a 12 volt battery in the form of an AAAA battery cut off short.

## 10/23/2023

I worked on correcting the Design Rules errors in the main lap counter schematic.  I have to fix some power annotation issues yet.  I'm going to do a mechanical drawing of the system so that I can rework the placement.

## 10/24/2023

I'm using FreeCAD as a mechanical design tool to do a layout for the electronic boards in the lap counter.  It'll be a lot easier to move stuff around.  However, I've forgotten how to use it!  I'll have to run the sketching tutorial again to remember.

## 10/25/2023

I looked at the tutorials and practiced how to use the sketcher.  Figured it out and developed a dimensionally correct Arduino board.  Now to do the other boards.

## 10/26/2023

I designed the mechanical shape for the 8 Relay Module in FreeCAD.  Only a couple more to go.  I found a new iteration of the Mega 2560 R3 that has a 2 Ampere voltage regulator in it. Given that, I don't think that I'll need the standalone regulator.  I'm only going to be driving 3 relays at a time. It was $21.

## 10/28/2023

I did mechanical design for another part, the radio receiver.  What's left are terminal blocks, and the power disconnect relay.  Then I can do a layout.  A problem to work out is removing the back panel where the buttons and the power plug will be mounted.

## 10/31/2023

I redid the flyback diode board without the passthrough.  I think that it will be OK with two wires in the terminal block, especially if I solder them or tin them.  If I decide to make the boards, it will be cheaper, since a lot of real estate got removed.  On the other hand, the prototypes may be easier (and faster) to make using perf-board.

## 10/30/2023

I added terminal barrier strips and the battery.  I think that I'm about ready for the layout.  First, though I have to test the power mechanism.  My big question is whether the power will last long enough for the Arduino to pull the relay that will throw the bistable switch.

## 11/9/2023

I worked on the mechanical design of the layout of the back of the counter.  I struggled with FreeCAD a good deal, but finally got it under control and have a preliminary layout.  I haven't done the power yet, and I'll get to that presently.  Next thing to do is be sure that the flyback diodes will work.  Then I'll build the circuit boards.  I also have to test and build the power system.

## 11/14/2023

I'm designing a new flyback diode board.  I think that it is bad form to branch a wire under a screw-down terminal.  Thus, I'll split the solenoid driver lines on a board I'm designing.  I'll only need one, so I might just build it on protoboard, rather than have it fabricated.

## 11/28/2023

I finally dropped the shoe and ordered a custom PC board for the flyback diodes.  It cost about $41 including shipping from China.  I ordered the parts that I don't have from Amazon and Digi-Key.  The total financial involvement is about $60.  I still have to test to see that the diode solution will work.  I'm pretty confident.

## 11/30/2023

I worked on the lap counter today by redoing the schematic to include the new Flyback Board 3 design.  I think that it will be cleaner.  I still have to try out the diode idea to see if it will work at all.

## 12/2/2023

I just tried on [Wokwi](https://wokwi.com/)  to run a simulated Mega 2560 driving a relay.  It was about 5 lines of code, and it worked! I might use this site to develop further.

## 12/3/2023

I worked on installing the Arduino IDE on my small Linux laptop so that I can drive the Arduino that will be on the device.

## 12/4/2023

Installed the Arduino AppImage onto my Linux laptop.  I'll use it to debug the Lap Counter software. I loaded my first program into an Arduino and made it go.  Blinking a LED.

I did the the diode experiment on the Lap Counter.  It did improve the arcing.  I'll proceed with the full Flyback Card 3 design.  I discovered that I don't have enough diodes to build the board, so I ordered another 20. Next is to dismantle the Lap Counter electronics and label the wires going to the solenoids. Then I'll breadboard the power supply.

## 12/5/2023

I loaded VSCode into my Linux laptop and discovered that it has an Arduino extension.  It doesn't use the 2.2.1 IDE components, but brings along the Arduino CLI from GitHub.  The extension is written by Microsoft.  I think, but am not sure, that this can coexist with the official IDE. The IDE is in an Appimage, so VSCode won't see it. I got VSCode going and loaded a simple blink program into the  Arduino Mega 2650.  That's going to be my development IDE.

I received the flyback board PCBs.  The traces are really tiny.  I thought that the narrow traces that I saw on the screen were schematic, but they are real.  I'm a little nervous that they won't carry the necessary current and will fry.  I'll build up just one segment of the board and then exercise it to see if it heats up.  If so, then I'll have to do another build.

## 12/6/2023

As I hold the Flyback PCB up to the light, the traces don't look so bad.  I'll still build just a small part of the board and try it.  First, the power supply.

## 12/14/2023

I worked more on the power circuit of the lap counter.  I decided that powering the relay boards might be too much for the Arduino, so I reinstated the 3a 12V-5V converter.  The one that was in the counter before was designed to output to two USB ports.  Those are usually current limited to 1A per port.  I decided to replace it with a pure 3A converter.

## 12/15/2023

I cleaned up my workbench and removed the old 12V-5V converter from the lap counter. I'm making space to breadboard the power supply, which I hope I'll get to tomorrow. I'll be getting the new one today.  I played with the solar panel.  It still does generate a voltage around 22 volts when unloaded.  I still have the panel controller, so I might be able to do something with it.

## 12/18/2023

I added a few things to the physical layout.  I think that I'm getting closer to the design.  I really have to build that power supply.

## 12/27/2023

I put a bit more together with the toggle relay and the switches. I'll hook up the power and see that I can switch that relay with the buttons.

## 12/28/2023

I finally put together the buttons, toggle relay and power supply to see that my power supply will work.  Now I add 5V converter and relay to make sure that the relay can turn the system off.

## 12/29/2023

I breadboarded up the power on/off circuits of the Lap Counter.  I wanted to be sure that the power supply would hold up long enough for the toggle relay to fully disconnect when driven by the Arduino.  It all worked.  Apparently, there is a capacitor in the DC-DC converter that held the 5V relay long enough to get the toggle relay.  It worked ... at least in isolation.  The circuit so far draws 10 mA while on.  One LED is lit from the 5V supply.

## 12/31/2023

Worked just a bit on the lap counter.  I redesigned the physical implementation of the card for placement into the box.  It wasn't really necessary, but I didn't like the previous incarnation. Now we should be ready to rock for the physical layout.

## 1/7/2024

I worked on the Lap Counter today.  I stripped off all of the electronics except the radio and all of the wiring except the wires going to the numbers.  I left the radio because it is glued to the board.  The next steps are to carve out the backboard so that it can take the LI-ion battery and to test the radio.  That should be pretty easy.  Just have to power it and then put a meter on the signal lines.  Maybe I'll hook an Arduino to it and light LEDs when the signals are detected. I'm a little behind schedule, overall.

## 1/13/2024

I worked on the Lap Counter by getting the programming environment up and going again on my Linux laptop.  Things got pretty screwed up after I replaced the HDD with an SSD.  It's taken me nearly two days to sort it all out. I think that I am ready to proceed with the software.

## 1/15/2024

I got a program going that reads an input and writes on the serial port that it changed.  This is the first step to reading the radio receiver.  I did hook some wires to the radio receiver so that I can test it with an Arduino. I'll try to do that tomorrow.

## 1/16/2024

I worked on the Lap Counter today.  I stripped off all of the electronics except the radio and all of the wiring except the wires going to the numbers.  I left the radio because it is glued to the board.  The next steps are to carve out the backboard so that it can take the LI-ion battery and to test the radio.  That should be pretty easy.  Just have to power it and then put a meter on the signal lines.  Maybe I'll hook an Arduino to it and light LEDs when the signals are detected. I'm a little behind schedule, overall.

## 1/17/2024

I need to route out some of the back panel to make the Li-Ion battery fit.  I ordered a router bit for my Dremel, which should be here tomorrow.

![The Empty Chassis](doc/images/PXL_20240118_220118669.jpg)

## 1/19/2024

 I routed out the space for the battery.  I made it bigger than it needed to be, but It seems to be OK.  I used a chisel to remove stuff faster than the Dremel was getting it, but that made the bottom rough.  I used the Dremel to smooth it.  Should get some black paint to make it look nice. Next, mount the electronics. Then I can run it.

![Battery Hole Routed Out](doc/images/PXL_20240120_010845676.MP~2.jpg)

## 1/20/2024

I have a little problem in that using the vertical DuPont connectors on the Arduino, there isn't enough clearance for my intended connection method. There is one version of the Arduino, called the Due, which replaced the Mega 2580, that doesn't have the connectors soldered on.  The downside is that it is Arm-based and VS Code doesn't support it.  So, next plan is to remove the connectors from one of the Arduinos that I have and put right-angle connectors on.  I bought some on Amazon and they should be here tomorrow.

## 1/21/2024

I did more work on the lap counter. I _may_ be able to use the regular pin slots of the Arduino.  It's looking really close.  Plan B is to use an Arduino Due, an ARM-based computer on the MEGA form factor but without the headers.  The software support for it isn't nearly as good. Another problem is that the processor and I/O pins are all 3.3 volts.  I'll have to buy a bunch of level converters to interface with the relays and radio.  I bought a Due, but I think I'm going to have to send it back.

## 1/22/2024

I'm going to practice de-soldering on the dead Arduino board that came in the lap counter.  First, I'll do a final test to be sure that I can't fit the vertical connectors into the case.  I tested the two relay boards that were in there.  One is fine. The other has a flakey connector under the silicone.  I'll have to cut that out.

## 1/25/2024

I designed and did a drawing for the acrylic back panel.  I'll take it over to [[TAP Plastics]] to get it made. I also worked out a way to use a prototyping shield to create some right-angle connections for the Arduino.  This will solve my vertical challenge.

## 1/26/2024

I bought some paint and wood to dress up the box a little.  I'll put it to use this weekend.

## 1/27/2024

Today I carved the silicone goo off of one of the relay boards because the connection was bad.  I pulled all of the individual headers off the wires and put a 10 p header on.  It holds very well.  I now know how to put pins into and pull them out of the headers.  Next, I learn how to crimp.  I think that I should probably get the silicone off the other relay too.

## 1/29/2024

I cleaned the silicone off the 2nd relay board.  Unfortunately, I scarred the circuit trace for relay 2.  I kind of pushed it back together and it's working for the moment, but I'll have to do better if I'm going to use the board.  I dug out the soldering iron.  That thing goes back more than 50 years.  Amazingly, I can still (just barely) get tips for it.  I bought some new tips and some soldering sponges for doing the work.

## 1/30/2024

Carpentry, or perhaps more closely, cabinetry today.  I cut basswood out to make a tight battery holder for the Li-ion battery.  I'll paint all my woodwork black next time the weather permits.  It's supposed to rain for several days

## 1/31/2024

Until the soldering stuff gets here, I'll be doing some programming. Wound up doing mostly getting the GIT stuff in synchronization.

## 2/1/2024

A couple of good things today.  I got my soldering gear out and my soldering chops up and repaired the relay board that I had cut a trace on.  I soldered a bypass wire in.  It appears to work now.  Those Dupont connectors are going to be a problem.

I also started programming up the Segment class.  Arduino is C++ and so I can use classes.

## 2/2/2024

I did a bunch of programming today.  I finished all of the segment and digit  logic.  What's left is to do the radio buttons logic and direct the digits based on button push.

## 2/4/2024

I finished the code for the lap counter.  Now I have to assemble the box to try the code out.

## 2/5/2024

I reread the programs I've written and fixed several bugs.  I also added a POST routine to show all of the segments working.

## 2/6/2024

I did more desk-checking of the code and found a couple more bugs.  I'm rusty at C++.  I also documented the classes and methods.

## 2/8/2024

Did a pull request and merged my changes to GitHub.  I generated HTML documentation using Atomineer and Doxygen. Next is soldering and painting.

## 2/14/2024

All I did today was prep my workspace for soldering the flyback diode board. Should be ready to rock tomorrow.

## 2/15/2024

I painted the case today.  The raw wood, cuts and scratches became black. I also did a bit of assembly for the Flyback Diode Card.
![Case painted](doc/images/PXL_20240215_231144668.jpg)

## 2/18/2024

I finished mounting the components and soldering the flyback diode board.
![Flyback Diode Board](doc/images/PXL_20240219_010652824.jpg)

## 2/19/2024

I laid out all the parts and the schematic for the power supply ready to mount in the case.  I'll get to that after we come back from our trip.

## 2/27/2024

I did a preliminary layout of the parts in the box.  It'll be a little tight and it will have a few long wires running around.  Wiring the solenoids will be the worst part, because it will be really tight with lots of wires.

## 2/28/2024

I have been thinking about the wiring.  I'm not terribly pleased with the physical layout that I have. There are too many wires just running all over the place and the grounds are widely separated from their associated power lines.  This will take a bit of thought.

## 3/10/2024

I started assembling wiring for the buttons.  I found that my back panel is clear, but is transluscent. Question: do I want to spend another twenty-odd bucks to get a clear one? I'm having a little trouble crimping the DuPont connectors without mashing them.  I'll keep working at it.  I have been tinning the leads, but maybe it's OK to use untinned leads or maybe you can only use solid wire for these crimps.

## 3/11/2024

I built my first connector today, after a bunch of failed attempts. First of many.
![First connector](doc/images/PXL_20240312_001918273.PORTRAIT.jpg)

## 3/12/2024

I built the matching connector to the one I built yesterday.  I still haven't mastered getting the crimp right the first time.  I have to fiddle around doing some crimps with needle nosed pliers. to make sure that the insulation part of the crimp is tight enough to go into the connector.

## 3/13/2024

I installed one connector on the back panel.  Now I have to screw down the components in the chassis and hook them up. I need to work out a strain relief on  both sides of the connecting cable.

## 3/14/2024

I did more work on wiring.  I mounted two of the connector blocks and then mounted the toggle relay.  It wasn't working, so I dismounted the relay and started building the harness that will go from the battery to the main power connector blocks through the toggle relay. It's mostly finished, so now I need to wring it out to be sure that my connections are good and mount the toggle relay again.

## 3/15/2024

I finally installed the toggle relay, battery connector with fuse and the harness to get to the buttons on the back panel.  This is measurable progress.  If I charge the battery, I should be able to turn the system on and off.
![Toggle installed](doc/images/PXL_20240316_000836459.jpg)

## 3/18/2024

I soldered the connector onto the hat for the Arduino. I also collected documentation and instructions for the battery charger and the battery. I charged the battery with the charger and all seems well.

## 3/21/2024

I built another power harness today.  This one for the Arduino.  Only need to power the relays now.

## 3/26/2024

I spruced up the documentation before sending the URL to Mike.

## 3/28/2024

I finalized the locations of the circuit boards.  I'm not crazy about the arrangement as it has a lot of long wires.  I just couldn't make my desired configuration fit.  The wires between the relays don't have enough room.
![Proposed layout](doc/images/PXL_20240329_000630082.jpg)
What I'm going to have to do is something like this:
![Another try](doc/images/PXL_20240329_000749985.jpg)
It requires longer runs of wires, but there's enough room for the flyback diode board and all the wires to the digits.

## 3/29/2024

I thought of another layout that I like a whole lot more. Short wires except for the radio.
![Final layout](doc/images/PXL_20240329_220929935.jpg)

## 4/1/2024

I worked on the 5 volt power system.  With the re-layout, it required some amount of rewiring.  I got the 5v regulator in and have in mind where to place the barrier blocks.

## 4/2/2024

I did a bunch more wiring. The power control circuitry is now all installed. Next, bolt in and power the relays. I have left a gap along the left side for installation of the local control buttons, A, B, C, D.
![Next the relays](doc/images/PXL_20240403_002900285.jpg)

## 4/3/2024

I mounted the segment select relay board and powered the relay ouputs.  I need to power the relays yet. That will come from the two barrier blocks just below the relay.
![First relay board mounted](doc/images/PXL_20240403_235702629.jpg)

## 4/4/2024

I wired the solenoid power from the segment select relay board to the set-reset relay board and mounted it.
![More Relay wires](doc/images/PXL_20240404_231234369.jpg)

## 4/6/2024

I mounted the digit-select terminal block and the Arduino.  The tough part was getting the pins aligned from the Arduino to the relay blocks so that there won't be a strain on the cables.
![First relay wired](doc/images/PXL_20240406_234918092.MP.jpg)

## 4/7/2024

I wired the power to the Arduino and wired the digit select lines between the relay blocks and the terminal strip. I tested the power and most seems well.  The power killing relay seems to have come up picked, but it didn't force a shutdown. its input was open.  I'll have to see what's going on.
![Relays wired](doc/images/PXL_20240407_225614828.jpg)

## 4/10/2024

I wrote most of the key state management software for de-bouncing the keys both membrane and radio.  I'm assembling a test case to work the bugs out.

## 4/11/2024

I finished writing and debugging the membrane key device driver software.   It handles both pressing and releasing de-bouncing. Now I'll convert the radio buttons to be members of the same class so that the interface is smooth. i'd rewritten the main loop in LapCounter.ino to use the new interfaces. Here's an image of my test bench. I integrated the new code into the existing LapCounter code.
![Program running](doc/images/PXL_20240412_025851559.jpg)

## 4/12/2024

I got the local buttons fully working and pushed the code. I wanted to clean up the compiler include path, but I couldn't manage to make it work with the includes anywhere but in the same directory as the main compilation unit.  I also cleaned up the Development Log and pushed that.

## 4/13/2024

Having the buttons working, I added a bunch of debug print lines to the LapCounter.ino file. And ran it.  I had to do a little hack to make the non-existent radio buttons quiet.  After that, with just a few tweaks, increment and decrement seem to be working.  I haven't made a complete test, by any means, but this is exciting.

## 4/14/2024

I did some more research on the matter of include files.  It is apparently a fact that the Arduino compiler looks only in the current folder for local includes.  I can have them elsewhere if I build a library and identify that library to the compiler.  I won't bother for now.

I mounted the local keypad and preliminarily routed the cables.
![New key pad](doc/images/PXL_20240414_222815417.jpg)

## 04/16/2024

Today I connected the local buttons to the Arduino with a temporary cable and then loaded and tested the LapCounter program. All good so far. I started wiring the Flyback Diode Board.  I'm leaving the lengths of the wires alone, for now, merely trimming bad ends off.  I decided to wire the board before mounting it, as it's easier to get the wires in with the board tilted towards me.  After I get all of the red and orange wires going to the solenoids in, I'll mount the board and run the wires from the relay board. I also started to wire the final path to ground for the solenoids.  I put a pull-up on the timeout relay so that it won't react until I am ready to test it.
![Paritally wired Flyback Board](doc/images/PXL_20240416_222703595.jpg "The Chassis")

## 04/17/2024

Today I was busy trying and failing to make ribbon cables.  The ribbon cables are a very fine wire and not tinned. The nature of the things tied together means that I have to be perfect on putting the connectors on.  If I fail on one connector, the whole thing is junk.  I decided to make the main signal cables out of single wires and then bind them into a harness with cable ties.  That way, if I fail on one wire, that's the only one I fail on. So, not much progress, but I have added understanding.

## 04/18/2024

I continued to build the cables. I'm building the short cable from the Arduino to the set/reset select relay.  The cable is 4" long.  A very slight difference in the wire lengths is a significant problem about making the cable work.  The short wires will always be tight.  I have built 6 of the 9 wires required. Two of them may be too short. I have over 3 hours in this cable, so far.

## 04/19/2024

I just had a thought about making short cables.  Start out by cutting them all the same length. put the connectors in one end and then into the connector shell.  bundle the harness and then cut the other end so that they are all flush the same.  That way they'll go into the connector shell evenly. For Cable 2, I won't harness them, but leave them loose. I probably won't bother for Cable 3 either. BTW, the cables are:

| Cable No | Use |
| :--------: | --- |
|1|Arduino to Segment Select Relay Board|
|2|Arduino to Set/Reset Select Relay Board|
|3|Arduino to Local Membrane Buttons|
|4|Arduino to Radio Module and Power Down Relay|
|5|Toggle Relay to Power Buttons|

I intend to label them and provide photos for how they are supposed to be installed.

I finished and wrung out my first big cable.
![Cable 2](doc/images/PXL_20240419_230446970.jpg)

It's cable 2.  It goes from the Arduino to the Set/Reset Relay Board.
![Cable 2 in place](doc/images/PXL_20240419_231935977.jpg)

This took me over 4 hours to make.  I ran into a bunch of problems: stripping wire, getting the lengths correct, the shortness of the bundle.  At least, if I screwed up a wire, I just threw it away and started another.  I didn't have to remake the whole cable. Note that I used wide connector bodies rather than individual ones.  The wide connecter bodies make the connections stay on better as the gripping force of the connector is multiplied by the number of wires bound together.

I just noticed that the Digit Select Relays are wired wrong. The wiring should go from the segment grounds to the Flyback Board and then to the Digit Select relay. I need to correct that.

## 4/21/2024

The electronics are all mounted!  Just wiring from here.
![All Electronics Mounted](doc/images/PXL_20240421_214329725.jpg)

## 4/22/2024

I fixed the error in wiring that I noticed on Friday.  The Digit Select Relays should be wired through the Flyback Diode Board.
![Correctly wired digit select relays](doc/images/PXL_20240422_224525143.jpg)

## 4/24/2024

I added the power for the two relay boards. This power is separate from the Arduino's power. This powers the relays, while the Arduino only powers the opto-isolators.  Note that VCC is yellow, GND is black.  The white wire is deliberately not hooked to anything.  It's there so the connector has one more grabbing point, but doesn't make a circuit.
![new power for relays](doc/images/PXL_20240425_002044705.jpg)

The next pic is for documentation.  It shows that the yellow wire connects to the pin marked VCC on the board.
![yellow is VCC](doc/images/PXL_20240425_002113026.jpg)

## 4/25/2024

Today all I did was test out the power supply circuits to see that the proper power was being delivered to the right places.  All good.

## 4/26/2024

I wired up one connector of Cable #1.  Next, I bundle it and then put the connector on the other end.

## 4/27/2024

I finished Cable #1.  I still have to wring it out, but it's looking pretty good.  It's stiff, so I'll have to do some amount of cable bending and twisting to get it to stay low enough for the cover.
![Cable #1](doc/images/PXL_20240427_215246577.jpg)

## 4/28/2024

I tweaked Cable #1 to make it size up to the distance between the boards and pressed it down so that the cover will clear it. I think that tomorrow will be the smoke test.

## 4/29/2024

I powered up the whole thing.  It didn't work. Now I get into debugging.  I resurrected a program that will blink all of the relays.  I'll try that next.

## 4/30/2024

Just a thought. I should probably explicitly jump the ground systems of the 12v powered devices and the 5v powered devices. That solved the problem. I made it work, through POST.  The POST routine sets the display to '88', waits 3 seconds and then resets everything.  Here's a movie:

<video src="doc/images/PXL_20240430_235422093.mp4" width="640"  controls></video>

## 5/1/2024

I added the wires from the Segment Select Relay to the Flyback Diode Board. I tested the connections with my  VOM. It's weird, everything seems to be shorted together.  I'm not sure what do to.  The VOM could be confused by the coils of the display, but I'm not sure.  Gotta think on this one.

## 5/2/2024

I have a thought that the circuits on the lap counter may be fine, rather than shorted out. I should disconnect the 12V power from the relays and test the circuit from there.  I think that feedback through the power supplies might have been confusing the VOM. What I want to see is no clear path to ground from the power supplies when the relays are not activated.


## 5/3/2024

I powered the whole thing up today. The POST ran fine, though one segment, "F" on the 10's digit seems reluctant to reset properly. It mechanically is OK. It might not be getting enough current due to bad connections or my other little problem. That is that the two digits take all of the signals whether or not the digit select relay is picked for that digit.  Somehow, the grounds of the digits are connected.  I'm going to have to wring that out.  Anyway, here's a movie of the first time the segments moved:

<video src="doc/images/PXL_20240503_232853053.mp4" width="640"  controls></video>

## 5/4/2025

I probed around to try to find why the corresponding segments of the two digits always move together, regardless of the digit select relays.  The grounds to the segments are shorted together. This is about the worst case scenario.  I am going to have to pull the digits to find the short(s). I started to take out the digits, however one screw deformed. I tried drilling it out, but it is actually threaded into the plastic of the number frame. I couldn't get it open by taking the head off the screw. I can't make the drill sit on what's left, so I'll have to drill around the screw to get the frame off of it.  A mess. Now that I have taken the thing apart, I checked the grounds again.  Not shorted. ARGH! The problem is with the diode flyback board. Have to continue tomorrow.

## 5/5/2024

While the numbers are all unwired, I tried to diagnose why the segments seem to be joined. I made a number of observations:

1. When the leads are all separated the set lead (SET) and the reset lead (RESET) are not connected to the common lead (COMMON) of the opposite number.
2. SET and RESET do form a DC path from one to the other. Since the COMMON are all connected together, There is a DC path from any lead on a digit to any other.
3. When the  from the two digits are connected together, applying a DC power will flip both segments.

I think that I might have to rework the Flyback Diode Board to prevent some of the paths.

## 5/6/2024

I built up a circuit that I think will work.  It adds two more diodes on each solenoid coil that prevent current from running backwards through other coils and creating a circuit for the other digit. I am going to have to build a new flyback diode board with twice as many diodes. I went through several iterations of the circuit on a protoboard.

## 5/7/2024

I worked on designing the new flyback diode card.  The new one puts diodes on all of the inputs so that current can't backflow connecting the wrong digit. It's looking like it will be a good deal bigger than the existing card.  I may have to move the Arduino.

## 5/8/2024

I spent most of the afternoon developing the physical layout of the new flyback diode card (version 4).  I did several iterations first figuring out the layout of parts that would simplify the wiring and then working on shrinking the size of the card.  I got it down pretty well, a lot by setting the grid to  50 mils rather than 100 mils. I still need to finish the wiring, but I'm not expecting a problem.  I'll send it for fab tomorrow.  First, however, I really need to test the circuit with the breadboard that I have built.  I'll do that tomorrow.

## 5/9/2024

I tested the basic circuit as breadboarded and found that it works. I re-verified it against the schematic and board design.

![Breadboard](doc/images/PXL_20240510_004104692.jpg)

 I finished the PCB layout and submitted the board design for manufacturing. I should have the results by May 15.

![Flyback board 4](Flyback_Diode_Card_4/Flyback_Diode_Card_4.png)

## 5/10/2024

While waiting for the new boards to arrive, I inventoried the parts that I will need to put on the board.  I'm in good shape for connectors, but not enough diodes. I ordered 125 1N4007 diodes, for about the same price as 20. They'll be here Monday, while the boards arrive Tuesday. I received word that they have completed manufacturing and have shipped. I have a tracking number, DHL 1660975326.

## 5/15/2024

I received and inspected the new boards.  I tidied up the build area so I can start assembling first thing tomorrow. 

## 5/17/2024

I soldered all of the connectors to the board and then did three diodes, individually.  I'm going to have to figure out a mass production scheme for the diodes.  There are a lot of them.

## 5/18/2024

Half of the diodes are soldered in now.

## 5/19/2024

The card is finished.  I wrung it out and it looks good.

![Finished Card](doc/images/PXL_20240519_204000619.jpg)

## 5/22/2024

I wired all of the solenoids to the Flyback Diode Board. Next, I mount the board and hook the relays and the common wires.

## 5/23/2024

I finished wiring the Flyback Diode Board in.  I'll wring it out again and then test it.

![New Board wired in](doc/images/PXL_20240523_215415701.jpg)

## 5/24/2024

I got it working! Initially, I was running it with really conservative solenoid hold times. That was taking up to two seconds to do the update.  Cranking the hold times down resulted in some of the solenoids not moving reliably. I changed the code so that I could set the solenoid hold times individually by segment.  There are only two slow segments. Here's a show:

<video src="doc/images/PXL_20240524_222607096.mp4" width="640"  controls></video>

## 5/26/2024

I unfurled the back cover and installed it for the first time. I have to be careful with the charging cable when I put the cover on, as if the cable is inserted wrong, there seems to be some kind of stress and two segments won't work. I'm going to have to work this fragility out of the system.  At any rate, here are two pictures, front and back showing what it looks like:

![Front](doc/images/PXL_20240526_200522543.MP.jpg)

![Back](doc/images/PXL_20240526_200437968.MP.jpg)

## 5/27/2024

I think that I have to redo the wires from the back panel into something cleaner. I'm going to shorten the wires on the panel until they just hang below the edge of the panel. Then I'm going to fix the mates so that they only will connect when the panel is a couple of inches up, with strain relief. I may have to redesign the panel, moving the buttons higher or to the other side.  The other side may work better as it involves dragging less wire all the way across the device.

I decided to do it. I measured the clearance to the radio and it works. I'll have to be careful about the power wire, as it wants to go straight down. The switch wires, two of which will terminate at the relay right there and one of which will have to go all the way across.  That's a bunch better than what I had.

## 5/28/2024

I continued work moving the power switches to the other side. In retrospect it might not have been a good idea. Things are tighter there and the buttons tend to hook wires going to the relays. I'll finish it and live with it a while. I may move them back.

## 5/29/2024

I finished moving the power buttons. I'll live with it for a while.  The next thing to do is make the cable to go to the radio.

## 5/30/2024

I worked on building the cable to the radio.  I have it about 1/2 done.

## 6/3/2024

I finished the radio/power down cable today. I also modified the program to look for the radio signals.  I'll try it tomorrow.

## 6/4/2024

The radio seems pretty sketchy.  It only seems to reliably work form about a foot.  I hooked up the  USB to follow the detection.  I noticed that with the USB, it worked a lot better.  I know that the regulator on the Arduino is outputting 6.5 Volts with a 12 Volt input.  the radio must not like this.  I should consider:

1. Power the radio with the 5V power supply.
2. Change the Arduino to one that will produce the proper voltage.

I'll investigate both of those tomorrow.

## 6/6/2024

It all works. I made the radio work, though the range is pretty poor, and I made the power down do its thing too.

On the power-down, I just had to wring out some bad connections. That may be a robustness problem for this device. The cables should probably be remade by someone who is really good at it.

The radio works, but gets really sketchy at more than about 10 feet. Maybe I should buy a new one. They're pretty cheap. The antenna length that's in there seems to be roughly correct. It's stuck to the backside of the cabinet, up against the metal plate of the number. That might be affecting its performance.

## 6/7/2024

As I researched about the radio, I found some threads from 9 years ago that indicate that the performance of these radios will never be very good. Perhaps a really good antenna may help. I've been looking around for a suitable antenna, but haven't found one. Coil antennas are available for cheap. They will be the right length, but coil antennas have poorer performance than the straight ones.

## 6/8/2024

I received and did a quick initial test of the new transmitter/receiver.  Works **_MUCH_** better. It was totally solid from 15 feet away in the garage. 

## 6/9/2024

Since I'm about to install the new radio receiver, I thought that I should take a picture of the Version 1.0.0 internals:
![Exit Old Radio](doc/images/PXL_20240609_214423457.jpg)

After that, I started on putting the new receiver in.  After a bunch of agonizing contemplations, I decided to put the new one where the old one was.  I'll remove it, and rotate the  power down relay to make room for it. This means that I'll have to return the buttons to the right side and build cabling to support it.  This is a bit more work that I had in mind, but the end is that the receiver didn't work on the upper right side.

## 6/12/2024

It's been too hot the past few days to work on the Lap Counter.  I went back at it today. I ripped out the radio and power disconnect relay. The radio was held to the cabinet with silicone putty. I then remounted the relay and mounted the new radio. I'm now ready to hook up the signal wires to the Arduino.  I think that the cable I made before will be long enough to use.  Otherwise, I'll have to make a new one. I changed the code to program the inputs to be active LOW in INPUT-PULLUP mode.  I also updated the schematic.

## 6/13/2025

I wired the radio up. Fortunately, I didn't have to build a whole new cable. It works from more than one foot away.  I tried it from about 12 feet away, and it works fine. I had trouble with some segments not clearing. I wiggled the connectors and it solved itself. This could be a reliability problem.  I'll try it out at the races and see how it does.  I reversed the back panel again and wired the buttons.  It now powers up and down correctly.  The remaining items include build the power cable that runs from the connector to the battery. I have to remember to have enough slack so that the power input cable can bypass the battery and hook directly to the circuit. Cable 3, from the Arduino to the membrane keypad needs to be built.  That will be about it.

Here's a picture of the insides of the chassis with the new radio:
![New Radio Installed](doc/images/PXL_20240613_231536460.jpg)

## 6/17/2024

I finished and installed cable #3.  It isn't tacked down yet, as I want to test the whole box at a Race before I tack everything down. Here are some pictures showing the cable and its connections.

![Cable 3 Arduino End](doc/images/PXL_20240617_231442009.jpg)

![Cable 3 Keypad End](doc/images/PXL_20240617_231448555.jpg)

![Chassis with Cable 3 in](doc/images/PXL_20240617_231506390.jpg)

## 6/19/2024

I added the charging cable that goes from the back panel to the charging port on the battery. I installed it loosely.  It needs to be tied down. I put the back panel on and installed window screen clips to keep both the front and back panels in place. It's ready for its debut. I plan to fix down the cables, spackle the holes and paint them before I turn it over to the NCNCA.

## 6/21/2024

I'm preparing to put the labels on the box instructing users what the keys mean and warning about the charging port. I'm also running it for several hours so that I can be sure that the charging cable is working. The box has correctly powered down after 2 hours.

## 6/22/2024

I  have continued testing the device by leaving it on. It has gotten pretty bad at resetting the segments. Recently I recycled the power and it left 3 segments showing after a reset.  I did a couple of resets after that and they wiggled the segments, but didn't reset them.  Maybe I should make the reset more aggressive.  A possibility is that as the battery voltage declines that the current isn't enough to do the reset. I need to test the voltage in the circuit now.

## 6/23/2024

I tried a reset of the Lap Counter this morning and it left 3 segments un-reset. I tried forcing a reset, but it didn't help. Then I plugged the charger onto the battery. It's only a 1 amp charger, so it could take a while.  If things are up-to-snuff when charging completes, then I'll know that voltage droop is the culprit. Now given that the measured current flow when the system is on and idle is about 100 mA and about 400 mA when the solenoids are moving, a 5.2 Amp-hour battery should last from 40 to 50 hours.  That may be for a voltage drop to 9 volts, which might be too low. I will run it to the point where it leaves segments un-moved and then measure the battery voltage. After 4 hours, it left one segment standing. This isn't good. I'm running it for another couple of hours.

## 6/24/2024

The battery power is not drooping. The voltage is pretty solid at 12.25V after running the box for 4 hours. When the relays and solenoids are energized, the voltage is 12.15V. My problem seems to be the "F" segment in the tens digit.  Sometimes the "F" segment in the units digit sticks as well. Both segments seem to set just fine. They don't reset. I tried holding the power on the reset for seconds, but that didn't work. I checked the circuits from the 12V line, through the segment select relay and the set-reset relay to the fly-back board and off to the segment. All connections are tight and with adequate cable diameter. I'm going to write a test program that will agitate the segment, hoping to break it loose and then slam it into reset position. 

## 6/25/2024

I tried several different methods of jiggling the segments.  Some were worse than  nothing. Nothing, in fact, worked. I'm charging the battery and will see what voltage will make the segment go when the battery is fresh. Then I'll look at increasing the voltage that the segments see. Perhaps I'll use a buck converter to raise the voltage to 13 or 14 volts.

## 6/26/2024

I recharged the battery and got it to where it is outputting 12.6V.  The segment works. When the battery settles to 12.1V, which is where it runs most of its life, then the segment doesn't work. I bought two cheap voltage up converters. One from Amazon and one from Digikey.  We'll see if I can run just a little more voltage on those coils. Then I'll have to figure out how to fit the converter into the box.

## 6/27/2024

I tried out the DC-DC Boost Regulator and it works just fine.  All segment moves are very crisp with a 12.7V supply.  Right now, the battery is providing 12.6V.  I'm going to run it a while to be sure that running the regulator doesn't run the power down too fast.  I don't want to have to control the power to the regulator to only when I'm going to move the solenoids. Here's a picture of the regulator in action, before being installed.

![Regulator](doc/images/PXL_20240627_221937660.jpg)
