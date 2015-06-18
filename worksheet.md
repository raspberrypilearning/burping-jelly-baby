# Burping Jelly Baby

Make a jelly baby burp by pressing it!

## Wire up a jelly baby

To turn a simple jelly baby into a switch, you will attach cables to it and then connect them to the GPIO pins on a Raspberry Pi.

1. Looking at the following GPIO diagram, comapre it to your Raspberry Pi. 

   GPIO stands for **General Purpose Input Output**. It is a way in which the Raspberry Pi can control and monitor the outside world by being connected to electronic circuits.  The Pi is able to control LEDs, or motors, or many other things.  It is also able to detect whether or not a switch has been pressed.

   You'll be using a single ground pin (marked `GND`) and a GPIO pin (marked `GPIO`):

|            |            |
|-----------:|:-----------|
|    3V3     | 5V         |
|  **GPIO2** | 5V         |
|  **GPIO3** | GND        |
|  **GPIO4** | **GPIO14** |
|        GND | **GPIO15** |
| **GPIO17** | **GPIO18** |
| **GPIO27** | GND        |
| **GPIO22** | **GPIO23** |
|        3V3 | **GPIO24** |
| **GPIO10** | GND        |
|  **GPIO9** | **GPIO25** |
| **GPIO11** | **GPIO8**  |
|        GND | **GPIO7**  |
|        DNC | DNC        |
|  **GPIO5** | GND        |
|  **GPIO6** | **GPIO12** |
| **GPIO13** | GND        |
| **GPIO19** | **GPIO16** |
| **GPIO26** | **GPIO20** |
|        GND | **GPIO21** |

Note that if you have an older Raspberry Pi model you'll only have 26 pins but they have the same layout, starting at the top row (`3V3` and `5V` and ending at `GND` and `GPIO7`).

1. Take the metal paper clips (or pins if you are using them) and unfold them to make a straight wire.

2. Take a female to female jumper cable and push the paper clip wire into one of the ends.

3. Do the same to the other wire so that you have two identical jumper cables with paper clip wires in one end.

4. Insert the paper clips into a jelly baby so that they are close to each other but not touching.

   The picture above shows the Raspberry Pi GPIO header pins; the diagram above the pins shows the pin numbers. You will be using `GPIO 3` and any `GND` pin. 
    
   Note that you will be only able to have one burping jelly baby button. Only use GPIO 3 and GND for this tutorial.

5. Take the other end of one of the jumper leads and push it onto `GPIO 3` of the General Purpose Input-Output (GPIO) header which is connected to one of the GPIO channels.

6. Take the end of the other jumper lead and push it onto the pin next to `GPIO 3` labelled `GND`.

   **Warning:** You can damage your Raspberry Pi if you do not use the GPIO pins correctly! 

7. Make sure your Raspberry Pi has speakers or headphones so that you can hear your jelly baby burping. If you are using headphones or a speaker on the Raspberry Pi, you will need to type the following command to redirect sound to the headphone socket in the **Terminal** which can be opened by clicking on **Menu** and then **Accessories**:

    `amixer cset numid=3 1`

## Sound of a burp!

So far you have created your input device and have your Raspberry Pi set up and running. You now need to find a burping sound file and move it into a new folder. This can all be achieved in a **Terminal** window:

1. Create a new folder called `jellybaby` with the following command:

    ```bash
    mkdir jellybaby
    ```

1. Enter the folder with `cd jellybaby`

    We're going to need a burping sample sound file for this project so we'll use one from Sonic Pi.

1. Make a copy of Sonic Pi's sound of a burp with the following command:

    ```bash
    cp /opt/sonic-pi/etc/samples/misc_burp.wav burp.wav
    ```

    This will copy the misc_burp sound file from the sonic-pi folder into the jellybaby folder and rename it to burp.wav

3.  Now test that you can play the sound file using `omxplayer` by typing:

    ```
    omxplayer burp.wav
    ```

    `omxplayer` will play the sound file and you should hear it from the speakers or headphones connected to your Pi.

    If you cannot hear anything, make sure that your headphones or speakers are connected correctly.  If the jack/plug looks like the picture below (notice the three black bands) you may find that it will only work if you pull the plug out by a few millimetres.

    ![](images/3-5mmjack.jpg)

## Write a program in Python

The final step to make your jelly baby burp is to write a program in Python; it will detect when you press the jelly baby input device and output the burp sound.


1. To write your Python program you will need to open the python programming environment **IDLE3** from the command line. To do this type the following command:

    ```
    sudo idle3 &
    ```

1. Once IDLE3 has opened, click on **File** and **New Window**. This will open a blank file. Click on **File** and **Save As** and name the file `burp.py`

1. Begin your program by importing the modules and libraries needed to make it work. Type the following:

    ```python
    import time
    import RPi.GPIO as GPIO
    import os
    ```

 The time library will be used to make the program pause for a fixed amount of time. The Raspberry Pi GPIO libraries will be used to connect the Raspberry Pi to other physical devices via the General Purpose Input-Output (GPIO) pins, in this case your jelly baby input device! The `os` library will allow you to play the burp sound in `omxplayer` but this time from within your code.

1. Now you will need to set up the GPIO pins to use GPIO board pin numbers. Leave a line empty by pressing Enter on your keyboard, then type:

    ```python
    GPIO.setmode(GPIO.BCM)
    ```
    
1. To switch off the "Ports already in use" warnings, press Enter to give you a new line and type:

    ```python
    GPIO.setwarnings(False)
    ```
    
1. Set `GPIO 3` on the GPIO header to be an input with the following command:

    ```python
    GPIO.setup(3,GPIO.IN)
    ```

1. Create a loop that runs forever and plays the burping sound file when the two wires inside the jelly baby are touching by typing the following:

    ```python
    while True:
        if GPIO.input(3) == False:
            os.system("omxplayer burp.wav")
            time.sleep(1)
    ```

1. Save the file by clicking on **File** and **Save**.

1. Finally, run the program by clicking on **Run** and **Run Module**

    **Congratulations!** Now when you press the jelly baby, the wires will touch and the burp sound file will play.


## What's next?

- Using a real button or switch connected to a breadboard
- Changing the sound that plays when the device is pressed
- Why not create a whole music box with our [GPIO Music Box tutorial](http://www.raspberrypi.org/learning/gpio-music-box/). 

