![Image of the licence](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)

# Somfy Remote
   This sketch allows you to emulate a Somfy RTS or Simu HZ remote.

   This is a fork of MakerMeik's project, to add functionality to control multiple (up to 20) blinds. 
   (https://github.com/MakerMeik/Somfy_Remote)
   
   MakerMeik's code was forked from the original sketch written by Nickduino (https://github.com/Nickduino)
    
   If you want to learn more about the Somfy RTS protocol, check out https://pushstack.wordpress.com/somfy-rts-protocol/
   
   The rolling code will be stored in EEPROM, so that you can power the D1 Mini.
   
   Easiest way to make it work for you:
    - Choose a remote number
    - Choose a starting point for the rolling code. Any unsigned int works, 1 is a good start
    - Upload the sketch
    - Long-press the program button of YOUR ACTUAL REMOTE until your blind goes up and down slightly
    - send 'p' via 'MQTT'
   To make a group command, just repeat the last two steps with another blind (one by one)

   Send a message to the channel number corresponding to the blind you want to program / control. 

   e.g. "Somfy-1"

   From the command line, this is:
   mosquitto_pub -h <mqtt server IP address> -m "u" -t "Somfy-1"
   
   Then:
    - u will make it to go up
    - s make it stop
    - d will make it to go down
    - p sets the program mode
    - you can also send a HEX number directly for any weird command you (0x9 for the sun and wind detector for instance)

If you want to learn more about the Somfy RTS protocol, check out [Pushtack](https://pushstack.wordpress.com/somfy-rts-protocol/).



**How the hardware works:**
Connect a *433.42 Mhz* RF transmitter to Arduino Pin 5 (or change the pin in the sketch). I couldn't find a 433.*42* MHz transmitter so I hacked a remote to send my signals. I then ordered 433.42 MHz crystals to change the regular 433.92 MHz ones I have on my transmitters: that's the cheapest way to do it. Other option would be to use a tunable transmitter like the CC1101 (but that hardly looks like the easy way and I'm not a ham radio, so...).


**How the software works:**
What you really want to keep here are the BuildFrame() and SendCommand() procedures. Input the *remote address* and the *rolling code* value and you have a remote. With the sketch, you can send the command through serial line but that would be easily modified to button press or whatever (I plan on running it on an internet-connected ESP8266 to shut the blinds at sunset every day).


The rolling code value is stored in the EEPROM, so that you don't loose count of your rolling code after a reset.

<br/>
<br/>
<br/>

**If you want more functionality**, check out the [Python version](https://github.com/Nickduino/Pi-Somfy)
