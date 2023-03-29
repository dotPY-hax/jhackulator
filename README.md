# jhackulator
## JHACKULATOR is a JTAGULATOR clone designed for cheap production and hand soldering

I need a JTAGULATOR to sit with the cool kids so I decided to make my own.

Fortunately the JTAGULATOR is open hardware and the schematic is readily available at http://www.grandideastudio.com/jtagulator/ ! After some inspection of the schematic and reading the [Propeller documentation](https://www.parallax.com/download/propeller-1-documentation/) I had a vague idea of how it works and I could get to KiCAD. But first a few decisions had to be made:
1. The board must be as cheap as possible -> 2 layers 10x10cm maximum
2. It must be as conveniently hand solderable as possible -> through hole where possible
3. FUCK FTDI

## Schematic

![image](https://user-images.githubusercontent.com/67259802/228602237-59398d7c-660e-4c9b-b701-7e299982f688.png)

This part of the original JTAGULATOR schematic looks like it was borrowed from the Propeller documentation and seems like a pretty standard Propeller development board. FTDI chips are massively expensive and one of the design goals was to cut costs so I replaced it with an ol reliable chinese CH34x series USB serial chip. Also nobody should be using FTDI chips anyways since FTDI-Gate. FUCK FTDI you cant just break peoples stuff because your managers throw a hissy fit! FUCK FTDI!

![image](https://user-images.githubusercontent.com/67259802/228603723-a6825012-9d70-4ad5-962f-0d0cf6194300.png)

This part of the JTAGULATOR is a big bus with level shifters which also act as bus tranceivers with output enabling. I omited the small ESD protection diode packages since the data sheet of the TXS0108EPWR already claims to have good ESD protection. I replaced the resistor arrays (to reduce part count for the pick and place ???) with single resistors.

## The board

The gerbers and the bom can be found in the repo!!


![IMG_20230329_145106](https://user-images.githubusercontent.com/67259802/228597561-b281a742-05c0-4484-ae83-dcc9a04f104d.jpg)

![IMG_20230329_145136](https://user-images.githubusercontent.com/67259802/228597604-eb4ee8c8-17fa-4c23-9e03-52d08cb9841a.jpg)


Unfortunately some of the newer and absolutely mandatory chips are not available as dip packages but our chinese friends offer great pick and place service for a reasonable price (I guess). The SOIC amplifier on the bottom right was out of stock so I had to resort to hand soldering SOIC which wasnt as horrible as I was expecting.

![IMG_20230329_144846](https://user-images.githubusercontent.com/67259802/228597365-b66f541c-f4ae-4bfa-9b90-227474ab846e.jpg)

![IMG_20230329_151100](https://user-images.githubusercontent.com/67259802/228597702-fd41f794-7d1f-49eb-ae54-5d1814fbaaf8.jpg)

After some recreational soldering I got a finished JHACKULATOR board - now comes the hard part...

## Software

The JTAGULATOR software for the Propeller chip is available at https://github.com/grandideastudio/jtagulator/tags ! Make sure to use the latest version - the .eeprom file is inside the zip!
Unfortunately the PropellerTool you need to burn the EEPROM is super old and only works on Windows so I need a VM. Microsoft has some handy "developer VMs" on their website! After I had installed the PropellerTool and CH341 drivers on my Windows 11 VM I can identify the Propeller through PropellerTool!

![image](https://user-images.githubusercontent.com/67259802/228582217-4f0e9f21-9676-42a7-a6c2-85c3141d1738.png)

It only works once though and I have no idea why. After some digging on the internet I found that the identify command is trying to reboot the Propeller so I think something is wrong with my reset circuitry - this will become important later!

burning the EEPROM!
![image](https://user-images.githubusercontent.com/67259802/228582808-9dfd0662-77fd-4f40-8952-0b3597b5688c.png)

![image](https://user-images.githubusercontent.com/67259802/228582978-58eef3c0-f042-4c18-a18c-8013d602db46.png)

After several tries of burning the EEPROM and getting the same error all the time I found out that the burn process worked and the error is actually irrelevant to the write part. Lucky!

## First test

I connect via screen and TADA!!


![image](https://user-images.githubusercontent.com/67259802/228581604-1917a8f6-f964-4434-a611-289c50b1971b.png)

Now I can sit with the cool kids and get JHACKULATING!! omg! so leet! wow!

## Lessons learned

This was my first project without building a prototype on perf board first so it was pretty exciting and I felt like I was in danger the whole time! In the end it worked out pretty well and the hardest part was actually finding the correct parts on Mouser and getting the PropellerTool to work xD

Also my first time I hand soldered anything smaller than THT. First time using pick and place services and first time buying from Mouser since the Propeller MCU is hard and/or expensive to get outside The US of A. It all went pretty well!

One of the electrolytic condensators has the wrong polarity!! Make sure to "beep" through the important pads before soldering!!

Reset circuitry might or might not be borked!!

I should buy some more cheap electronics to JHACKULATE!!
