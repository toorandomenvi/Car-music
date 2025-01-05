# Raspberry pi based music player for use in a car

Due to a small demand, I have decided to write up an entire explanation of the music player in my car.
This will include why I chose what I chose, what were my reasons for building this, what are the things I need this to do and reasons why certain things (like specific OS distributions), straight up dont work for my use case.

I have been working on this setup on and off for about 4 years now and using it daily.
It was built for me and it is doing what I need it to do. This is not something everyone will want and I fully respect that.




I will add onto this during the week as I have time, I am hoping to include photos and specifics why I did something the way I did.

TLDR - 

The setup is -
    Raspberry pi 4 (8gb version),
    Hifiberry dac +,
    NVMe M.2 to USB 3.0 enclosure with a NVMe SSD,
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
