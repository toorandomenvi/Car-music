# Raspberry pi based music player for use in a car

Due to a small demand, I have decided to write up an entire explanation of the music player in my car.
This will include why I chose what I chose, what were my reasons for building this, what are the things I need this to do and reasons why certain things (like specific OS distributions), straight up dont work for my use case.

I have been working on this setup on and off for about 4 years now and using it daily.
It was built for me and it is doing what I need it to do. This is not something everyone will want and I fully respect that.
I am not selling anything nor making any money off of this. This is purely that my experience might help some other people, solve the problem they did not know they had.

# What is it ?

The "device" itself is a music player. It plays localy stored music and can be controlled via your Phone / dedicated screen, ...
Think of it as an Ipod with remote control capabilities and no built in screen.
It is a combination of off the shelf parts anyone can buy and software that anyone can download.
I did not write this software, I did not engineer the parts.

The extent of my work was trying everything available to me and slowly ironing out all the kinks to make it do what I wanted it to do.
And alot of trial and error and even more configuration...


# What is it supposed to do ? / my personal requirements

What I wanted out of this project are the following features / functions - 

- I dont want to touch anything, car starts, music starts and keeps shuffling.
- Preferably output via RCA, that is then ran through a ground loop isolator (believe me you need one), and then to an AUX input of a radio.
(I am currently using this in a 2007 Lexus IS250, with a built in AUX from factory, hidden in center compartment, this can easily fit the entire player)
- I dont want to pay for subscriptions to play music I already have.
- There has to be an option for Equalization and gain normalization (preferably using tags in the music files).
- The system has to have option to control it via my phone but also has to be able to work without the phone. 
(the best option is currently to have a Wifi hotspot hosted on the raspberry pi and have your phone connect to it, to control the music)
- I would prefer for the UI not to be laggy while using it.
- I need it to be reliable, rebuilding the whole thing once a month is not an option. Preferably "set it and forget it"

I dont personally use Bluetooth for music so this feature does not play a role for me.

TLDR - A box I can hide in my car, that outputs music via RCA, that I can power via a phone charger, that functions on "good enough level" without a phone.

# What Hardware is used for my setup

The current setup is pretty much at the point where I dont want to touch or tweak anything.
There is a thing or two I would like to try to do differently or add onto this but none of that is essential for the experience.
Following is a full list to get the same experience as me. Bellow the list, you can find explanations why I chose what I chose and possible alternatives for you.

- Raspberry pi 4 (8gb version) (75-85$)
- a 32gb SD card (dont bother with no-name cards) (10-15$)
- a Hifiberry Dac+ (20-30$)
- a Raspberry pi 4 compatible cooler with an integrated cooling fan (it does get hot) (10-15$)
- RTC battery with native support for Raspberry pi 4 (5-10$)
- a 3D printed case for the Raspberry pi with support for the Hifiberry dac. (I have my own, this will be shared in the files)
- Velcro tape, some twist ties, some double sided tape (5$)

- an external Sata or NVME to usb 3.0 adapter (Axagon EEM2-U3 USB 3.0 - SATA M.2 box) (10-20$)
- a 512 gb Sata ssd (size is absolutely up to you, my music library is fairly large) (25-40$)
- a good phone charger to power the raspberry pi. (10-30$)
	The Charger I am using is Orsen C8 45W Mini Car Charger, but I have also tested a noname 45w usb C charger and Viking C-DC84 that both worked just fine. 

- a short 90° atlest usb 3.0 rated USB C cable. (I am using PremiumCord USB4™ Gen 3x2 40Gbps 8K@60Hz 240W Thunderbolt 3) (15-20$)
- 1x 90° USB C male to Female adapter. (just to make the connection low profile since finding short double 90° usb C cables is really hard where I live) (5$)
- RCA to RCA Ground loop isolator (this is very important if you dont like the sound of alternator whine) (10-20$)
- a short RCA to 3.5mm jack adapter (with a low profile connector) (5-15$)

- PiCorePlayer (32bit version) https://www.picoreplayer.org/
- Squeezer https://play.google.com/store/apps/details?id=uk.org.ngo.squeezer&hl=en&pli=1

You also need a radio in your car that accepts AUX as an input.
You can also get one that takes RCA and hide the cabling all together.

Total price worst case scenario - 280$

My total price was - 110$  As I either already owned alot of these things or got them for free.

# Hardware continuation - Why I chose what I chose

### Why RBP 4?

The entire setup will work "fine" with a 3b+ even tho its going to be considerably slower.
I went with RBP 4 over 5, as Raspberry pi 4 has way lower power consumption and thus lower requirements on the powersuppply.

one of many comparison available - https://core-electronics.com.au/guides/raspberry-pi-5-vs-raspberry-pi-4-model-b-comparison-and-benchmarking/

One thing why I moved away from using 3b+ is the boot time. When you plug a display to your RBP during boot time, you will see what is taking how long during the boot up of PiCorePlayer.
The big thing I noticed is that it takes about 20-30 seconds on a 3b+ to just check for the RTC module, which I did not have. That mean wasting 20-30 seconds every time, before you get your music.
Upgrading to RBP 4 and the RTC battery, you cut down this boot up time by 20-30 seconds just on the RTC check alone.

From experience when the powersupply is just mildly underpowered or just on the edge of not being good enough, you experience alot of instability and weirdness.
One thing to keep in mind is you are not powering just the raspberry pi but also the USB to SATA / NVME adapter with the SSD.

Also you might be dealing with the temperature in the car being really cold in the mornings during winters. What might happen to you is, that the Raspberry pi comes on just fine but the SSD wouldnt.
To fix that, letting the setup run for a minute or two and then uplugging it and plugging it back in will make it work.
For me its enough to just turn the key to the first position for the RBP to start and then start after couple seconds.

I went through a couple issues, powering the raspberry pi, majority were caused by flaky cables or cheap phone chargers, so make sure both are good when buying them.

------
### Why external M.2 eclosure?

I decided to use the external SSD only for music as you can easily wipe it and load now music on it without having to mess with the system.
The whole process is way easier when you can just unplug it when you get home and plug it into your pc. If you go with the internal SSD route with a dedicated board for the raspberrypi,
Updating your library will be way more complicated.

There is very little difference going with NVME over Sata since this is just music storage.
So if you have a spare M.2 ssd, go with whatever you have.

In the first version of this player I was using a 2.5" Sata SSD that also worked just fine, I just picked the smaller form factor later on to make the size of the unit smaller.
Also if you dont have that much music or its all in mp3, you might get away with using a normal thumb drive and save yourself some money. Dont store your music on the same SD card as your OS... just dont.

------
### Why a dedicated DAC?

This is mostly personal preference. Objetive reason would be, its louder outputting via RCA compared to the built in jack.
Doing DSP thing later also gets a bit easier.
Yes it also sounds a bit better but I doubt you can tell them apart in a A B test.

------
### Ground loop isolator 

This is absolutely mandatory. You will know if you get one that works or doesnt.
If you never messed around with car audio you might have not experience the alternator whine.
What that means is, when you have shared ground between your cars engine and your music player, you get whine in the speakers.
Its VERY noticeable and it gets louder as you accelerate.
This never happens if you just plug your phone to the AUX as your phone has its own powersupply (the battery) and the grounds arent shared.
With some devices you do get to experience this when you are charging the device and outputting audio at the same time. For example using your old Ipod in car mode with a docking cable.

Thats where the ground loop isolator comes in. This "box" splits the grounds for your audio cabling and you get rid of the whine.
It sounds like some placebo audiophile bullshit but this one absolutely works and is mandatory for car audio.

Example - https://www.youtube.com/watch?v=MLC_-yJy2p8

------
### Cables

TLDR - I cant tell you what cables you really need. This is different from car to car.

I personally try to keep the music player out of the way. You dont run into it unless you want to. That means in the trunk, in a compartment somewhere and so on.
In my current car, the AUX input is hidden in a center console along with enough space to fit the player, so the entire setup is using very short cables to cut on the mess.

If you decide to move the player all the way to the trunk, I suggest you wire in a 12v plug back there so you dont have to run long USB cables, and then hide the RCA cabling in the carpet.
In general the cable between your external drive and your RBP is going to be very short, Same goes for your "power cable", this will be fairly short if you put the player close to an outlet.
The audio cabling will be as long as you need it to reach your AUX input. I suggest you run as much of the lenght as possible in RCA, as the cables and connctors are more durable that fragile 3.5mm jack.

# Software - Comparasion and why you should use PiCorePlayer

TLDR - Use PiCorePlayer and dont bother with anything else.

https://www.picoreplayer.org/


### What are the options ?

If you want to use your Raspberry pi as a music player you have a bunch of distributions to chose from based on your needs.
The big ones are Volumio, Moode Player, RuneAudio and so on.
All of these are garbage for one reason or another that I will get into later on, save yourself the time and go with PiCorePlayer.

Other distributions focused on being music players either did not work well enough or were missing mandatory features I needed.
That means the following systems I have tested and decided agaisnt for one reason or another.

HiFiBerryOS, Kodi, Raspberry pi OS with WEB_UI, Ubuntu with automations, RuneAudio ...

### My experiences and pros and cons

Volumio - 
	This is the big one, this will do majority of what you need "well enough".
	Majority of my experiences with Volumio come from 2022.
	
	Pros 
		-Stable
		-Polished
		-Community support
		-The biggest one
		-Alot of money goes into developement
		-Best support for streaming stuff
	Cons 
		-Slow and bloated both to run and to control via your phone
		-The premium plan...
		-Bluetooth input behind a monthly paywall
		-"Infinity playback" behind a monthly paywall
		-Digital inputs and outputs behind a monthly paywall
		-When I was using it, equalization was a beta feature
		-Replay Gain had to be setup via CLI and got reset with an update.
		
------		
Moode Player -
	"The free version of Volumio"
	Everything is free here at cost of stability.
	
	Pros
		-Less Bloated than Volumio
		-Majority of settings available via GUI
		-Multiple choices for equalizers including Camilla DSP
		-Customization of the interface
		-Used to be compatible with the Volumio phone app
		-When it works, it works well
		-Fairly feature rich
		
	Cons
		-From my experience fairly unstable. The installation straight up breaks sometimes
		-A bit slower to control
		-Clunky configuration
		-Slow updates
		-By far the longest boot time
------	
PiCorePlayer
	The "tweek whatever you want" one
	If you need to change a very specific thing about it, you will find a way how.
	Use the 32bit version if you can, 64bit version is time and time again very unpredictable for me.

	Pros
		-By far the most lightweight
		-Very fast to boot up
		-Runs on everything I tried including RBP 0W
		-Supports all the features I need
		-Really snappy to control via an App on your phone
		-Very stable
		-If you dont need it, its not installed
		-Very detailed settings of the hardware
		-Logitech media Server is by far the most mature system for this usecase
		
	Cons
		-Hard to setup (it gets way easier as you do it)
		-Squeezelite gets messed up sometimes during setup
		-64bit version was very unstable for me, some modules straight up did not installation during setup
		-Very poor documentation for anything that isnt basic features
		-Very slow updates
		-Poor support on IOS, as far as I know, the only good way to access the player is via web browser and IP address.











TLDR - 

The setup is -
    Raspberry pi 4 (8gb version),
    Hifiberry dac +,
    Sata M.2 to USB 3.0 enclosure with a M.2 SSD,
    32gb SD card,
    Ground loop isolator (very important),
    A heatspreader with an integrated cooling fan,
    RTC battery (important for boot time times, I did not find a way to bypass this without the RTC battery),
    A 3D printed case for the raspberry pi,
    A good phone charger. I will have a couple I tested listed later on,
    Some cabling, mostly short double 90° usb C cable, Double RCA to a 90° 3.5mm Jack,

An installation of PiCorePlayer -  (https://www.picoreplayer.org/) (https://github.com/piCorePlayer)
Pick the 32bit version, I have experienced ALOT of weirdness during the setup and isntability later on running a 64bit version.
This was both on a raspberry pi 3b+ and now 4.

A phone app / web browser, to control the music player. I personally use the app Squeezer (https://play.google.com/store/apps/details?id=uk.org.ngo.squeezer&hl=en&pli=1) on my Android phone. I did not find a functional app for IOS.
For IOS users, you can just type in the IP of your music player into your browser when you are connected to its hotspot and the UI will come up just fine, it will just be slower.


Optional - 

Dedicated touch screen with a Raspberry pi zero w, also running PiCorePlayer, setup to connected to the main Access point and interface with it via Jivelite. This is a massive pain to setup.
I got it working, please dont make me redo it again for sake of the documentation.

From my testing once you get it working (after about 8 hours), it is very snappy to use, fast to boot and over all a good upgrade to this setup if you have space for a touch screen.
The Screen I used was a Waveshare screen made specifically for Raspberry pi Zero and a 3D printed case - 

7″ Touch Display Kit For Raspberry Pi Zero, With IPS Display Expansion Board, 1024×600, 5-point Capacitive Touch
https://www.waveshare.com/zero-disp-7a.htm
This can be easily bought off of AliExpress if you search the part number Zero-DISP-7A (at the time of writing the are only 2 results, both are valid)

# Updates to come
