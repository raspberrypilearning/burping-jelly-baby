# Make a Jelly Baby Scream!

**Introduction**
You will learn how to turn a Jelly Baby into an input device for your Raspberry Pi. You will then create a program to make it scream when it is pressed. 

## Step 1: Wire up a Jelly Baby

To begin you will need to turn a simple jelly baby into a switch by attaching cables to it and then connecting them to the GPIO pins on a Raspberry Pi.

**You will need:**

![alt text](image.png "Components")

**Activity Checklist:**

1. Take the metal paper clips and unfold them to make a straight wire.

2. Take a female to female jumper cable and push the paper clip wire into one of the ends. 

3. Do the same to the other wire so that you have two identical jumper cables with 

4. Insert the paper clips into a jelly baby so that they are close to each other but not touching. 

    Raspberry Pi GPIO header pins. The diagram above the pins shows the pin numbers. You will be using pin 3 and pin 25.

5. Take the other end of one of the jumper leads and push onto pin 3 of the General Purpose Input-Output (GPIO) header which is connected to one of the GPIO channels.

6. Take the end of the other jumper lead and push onto pin 25 of the GPIO header which is connected to ground.

    **Warning!** You can damage your Raspberry Pi if you do not use the GPIO pins correctly!

7. Set up the rest of your Raspberry Pi with an SD card with the latest Raspbian image installed via NOOBS, a keyboard, mouse, a HDMI cable to a monitor or TV, a connection to the internet, and a speaker so that you can hear your Jelly Baby screaming. [See the Raspberry Pi Quick Start Guide here](http://www.raspberrypi.org/quick-start-guide)    

8. Finally plug in a Micro USB power supply to start your Pi and log in. The default login for Raspberry Pi is: login `pi` and password `raspberry` 
    
## Step 2: Downloading and playing screams!

So far you have created your input device and got your Raspberry Pi setup and running. You now need to download a scream sound file and install some software to be able to play it. This task can be achieved from the command line.

**Activity Checklist:**

1.  After logging into your Raspberry Pi you will see the following text:
    
    ```
    pi@raspberry ~ $
    ```
    The Raspberry Pi is waiting for you to type in a command to do something. This is referred to as the command line. 

2.  Type the following command and press **enter** to install a program that can play mp3 files:

    ```
    sudo apt-get install vlc
    ```
    
3.  Download an mp3 sound effect to play when the Jelly Baby is pressed - all of this instruction should be typed on one line with the same uppercase and lowercase characters.

    ```
    wget http://goo.gl/oejqP5 
    ```
4.  Now test that you can play the sound file using mplayer by typing:

    ```
    clvc /home/pi/la.mp3
    ```
    
    vlc will play the downloaded sound file and you should hear it from the speaker or headphones connected to your Pi. If     you can not hear anything, make sure that your headphones or speaker are connected correctly.  
    
## Step 3: Write a program in Python

The final step to make your Jelly Baby scream is to write a program in Python that detects when you press the Jelly Baby input device and outputs the scream sound.

**Activity Checklist:**

1. To write your Python program you will need to open a text editor window from the command-line. To do this type:

    ```
    nano scream.py
    ```

2. Begin your program by importing the modules and libraries needed to make it work. Type the following:

    ```python
    import time
    import RPi.GPIO as GPIO
    import os
    ```
    
    The time library will be used to make the program pause for a fixed amount of time. The Raspberry Pi GPIO libraries       will be used to connect the Raspberry Pi to other physical devices via the General Purpose Input-Output (GPIO) pins,      in this case your Jelly Baby input device! The os library will be used to allow our program to call other programs        that run on the Raspberry Pi like vlc.
    
3. Now you will need to set-up the General Purpose Input-Ouput (GPIO) pins. Leave a line empty by pressing enter on your keyboard and the type the following:

    ```python
    GPIO.cleanup()
    ```
    
    This line of code will clear the current set-up so that you can begin a fresh. 
    
4. Setup the GPIO library to use GPIO board pin numbers by typing: 

    ```python
    GPIO.setmode(GPIO.BOARD)
    ```
    
5. Set pin 3 on the GPIO header to be an input

    ```python
    GPIO.setup(3,GPIO.IN)    
    ```
6. Create a loop runs forever and plays the screaming sound file when the two wires inside the Jelly Baby are touching by typing:

    ```python
    while True:
        if GPIO.input(3) == False:
        os.system('cvlc la.mp3 &')
        time.sleep(1);
    ```

7. Save the file by pressing `CTRL+X`, then `Y` for yes, followed by `Enter`.

8. Fianlly, run the program by typing:

    ```
    sudo python SingingJellyBaby.py 
    ```
    
**Congratulations!** Now when you press the Jelly Baby, the wires will touch and the mp3 file will play
    
