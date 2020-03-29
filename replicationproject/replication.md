# Assessment 1: Replication project

*Fill out the following workbook with information relevant to your project.*

*Markdown reference:* [https://guides.github.com/features/mastering-markdown/](http://guides.github.com/features/mastering-markdown/)

## Replication project choice ##
### Timing Gates ###
https://makecode.microbit.org/projects/timing-gates

## Related projects ##

### Related project 1 ###
#### Infrared Timing Gate ####

https://bigl.es/micro-bit-infrared-timing-gate/

![Image](images/similar/project_1_infrared.png)

This project is related to mine because it starts with the same project, then advances it to a far higher level. The project finalises by using infrared sensors to record the start and end of the timing as apposed to a crude electrical circuit to record these events.

### Related project 2 ###
#### Wireless Laser Gate ####

https://create.arduino.cc/projecthub/Pablerdo/wireless-laser-gate-timing-system-for-track-and-field-ba8cd9
![Image](images/similar/project_2_laser.jpg)

This project is related to mine because it is also a timing gate, however instead of using basic electrical circuits, it uses lasers and LDRs or *photoresistors*. As well as this, the project employs tranceivers, and is built on the Arduino Uno platform, allowing the different gate modules to be wireless.

### Related project 3 ###
#### Traffic Light System ####

https://www.hackster.io/anish78/traffic-light-system-using-bbc-micro-bit-da2f47
![Image](images/similar/project_3_traffic.jpg)

This project is related to mine because it could be used in conjunction with the timing gate system. In principle, if the timing gates were used on the road, the traffic lights could be used as a system to limit the inflow of traffic between the two gates, allowing one car to pass over both gates before the next care is allowed through.

### Related project 4 ###
#### Microfootball ####

https://make.techwillsaveus.com/microbit/activities/microfootball
![Image](images/similar/project_4_football.jpg)

This project is related to mine because it uses the same principal of connection to trigger an event. When the back of the net (covered in aluminium foil) touches the other foil plate, the connection is completed and the micro:bit reads an input to one of its pins, in turn triggering an event in the code. This is the same system used on the timing gates project where the object crossing the gates completes the connection of the first circuit. 

### Related project 5 ###
#### Frustration ####

https://projects.raspberrypi.org/en/projects/frustration
![Image](images/similar/project_5_frustration.png)

This project also uses the concept in fabrication of completing a circuit to trigger an event. The frustration game is a widely popular board game where when a wand is passed over a wire and every time connection is made, a buzzer is signaled.

## Reading reflections ##
*Reflective reading is an important part of actually making your reading worthwhile. Don't just read the words to understand what they say: read to see how the ideas in the text fit with and potentially change your existing knowledge and maybe even conceptual frameworks. We assume you can basically figure out what the readings mean, but the more important process is to understand how that changes what you think, particularly in the context of your project.*

*For each of the assigned readings, answer the questions below.*

### Reading: Don Norman, The Design of Everyday Things, Chapter 1 (The Psychopathology of Everyday Things) ###

*What I thought before:* 

*What I learned:* Descoverability and understanding are the most important attribute of design. 

*What I would like to know more about: Describe or write a question about something that you would be interested in knowing more about.*

*How this relates to the project I am working on: Describe the connection between the ideas in the reading and one of your current projects or how ideas in the reading could be used to improve your project.*

### Reading: Chapter 1 of Dan Saffer, Microinteractions: Designing with Details, Chapter 1 ###

*What I thought before:* 

*What I learned: Describe what you now know or believe as a result of the reading. Don't just describe the reading: write about what changed in YOUR knowledge.*

*What I would like to know more about: Describe or write a question about something that you would be interested in knowing more about.*

*How this relates to the project I am working on: Describe the connection between the ideas in the reading and one of your current projects or how ideas in the reading could be used to improve your project.*

### Reading: Scott Sullivan, Prototyping Interactive Objects ###

*What I thought before:* 

*What I learned: Describe what you now know or believe as a result of the reading. Don't just describe the reading: write about what changed in YOUR knowledge.*

*What I would like to know more about: Describe or write a question about something that you would be interested in knowing more about.*

*How this relates to the project I am working on: Describe the connection between the ideas in the reading and one of your current projects or how ideas in the reading could be used to improve your project.*


## Interaction flowchart ##
*Draw a flowchart of the interaction process in your project. Make sure you think about all the stages of interaction step-by-step. Also make sure that you consider actions a user might take that aren't what you intend in an ideal use case. Insert an image of it below. It might just be a photo of a hand-drawn sketch, not a carefully drawn digital diagram. It just needs to be legible.*

![Image](images/FlowChart.png)

## Process documentation

*In this section, include text and images that represent the development of your project including sources you've found (URLs and written references), choices you've made, sketches you've done, iterations completed, materials you've investigated, and code samples. Use the markdown reference for help in formatting the material.*

*This should have quite a lot of information!*

*There will likely by a dozen or so images of the project under construction. The images should help explain why you've made the choices you've made as well as what you have done. Use the code below to include images, and copy it for each image, updating the information for each.*

![Image](missingimage.png)

*Include screenshots of the code you have used.*

## Project Code ##

```javascript
let distance = 1;
let t1 = 0;
let t0 = 0;

pins.digitalWritePin(DigitalPin.P8, 0);
pins.digitalWritePin(DigitalPin.P12, 0);

basic.showLeds(`
    . . . . .
    . . . . .
    . . # . .
    . . . . .
    . . . . .
`);

basic.forever(function () {
    input.onPinPressed(TouchPin.P1, function () {
        pins.digitalWritePin(DigitalPin.P8, 1);
        music.playTone(622.25, 100);
        t0 = control.eventTimestamp();
        basic.showLeds(`
            # . . . .
            # . . . .
            # . . . .
            # . . . .
            # . . . .
        `);
    })
    input.onPinPressed(TouchPin.P2, function () {
        pins.digitalWritePin(DigitalPin.P12, 1);
        music.playTone(415.30, 100);
        t1 = control.eventTimestamp();
        basic.showLeds(`
            # . . . #
            # . . . #
            # . . . #
            # . . . #
            # . . . #
        `);
        //Recorded in microseconds, divide by 1 000 000 to convert to milliseconds
        let time = (t1 / 1000000) - (t0 / 1000000)
        basic.showLeds(`
            . . . . .
            . . . . .
            . . . . .
            . . . . .
            . . . . .
        `);
        //distance / time
        let velocity = distance / time;
        console.log(time.toString());
        let velString = velocity.toString().slice(0, 4);
        console.log(velString);
        basic.showString(velString + "m/s");

        basic.pause(100);
        pins.digitalWritePin(DigitalPin.P8, 0);
        pins.digitalWritePin(DigitalPin.P12, 0);
        basic.showLeds(`
            . . . . .
            . . . . .
            . . # . .
            . . . . .
            . . . . .
        `);
    })
})
```

# Project outcome #

## Speed from Timing Gates ##

### Project description ###

*In a few sentences, describe what the project is and does, who it is for, and a typical use case.*
This project is a simlpe system that records the time it takes to travel between two points and calculates the speed. Typically, this system would be used on roads to record time between to road points by vehicles. When the first gate is passed the red light will turn on, signalling that timing is in progress, and a tone will be played. When passing the second gate, the green light will turn on, signalling that the process is complete, and a different tone will be played. The speed of the vehicle will then be dispayed on the LED screen in metres per second.

### Showcase image ###

*Try to capture the image as if it were in a portfolio, sales material, or project proposal. The project isn't likely to be something that finished, but practice making images that capture the project in that style.*

![Image](missingimage.png)

### Additional view ###

*Provide some other image that gives a viewer a different perspective on the project such as more about how it functions, the project in use, or something else.*

![Image](missingimage.png)

### Reflection ###

*Describe the parts of your project you felt were most successful and the parts that could have done with improvement, whether in terms of outcome, process, or understanding.*
The most succesful 


*What techniques, approaches, skills, or information did you find useful from other sources (such as the related projects you identified earlier)?*


*What ideas have you read, heard, or seen that informed your thinking on this project? (Provide references.)*


*What might be an interesting extension of this project? In what other contexts might this project be used?*
