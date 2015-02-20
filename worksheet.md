## Step 1: Wire up a jelly baby

To begin to turn a simple jelly baby into a switch, you will attach cables to it and then connect them to the GPIO pins on a Raspberry Pi.

1. Looking at the following GPIO diagram, comapre it to your Raspberry Pi. 

    *GPIO stands for **General Purpose Input Output**. It is a way in which the Raspberry Pi can control and monitor the outside world by being connected to electronic circuits.  The Pi is able to control LEDs, turning them on or off, or motors, or many other things.  It is also able to detect whether a switch has been pressed, or temperature, or light.*

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

1. Take the metal paper clips and unfold them to make a straight wire.

2. Take a female to female jumper cable and push the paper clip wire into one of the ends.

3. Do the same to the other wire so that you have two identical jumper cables with paper clip wires in one end.

4. Insert the paper clips into a jelly baby so that they are close to each other but not touching.

    The picture above shows the Raspberry Pi GPIO header pins; the diagram above the pins shows the pin numbers. You will be using `GPIO 4` and any `GND` pin.

5. Take the other end of one of the jumper leads and push it onto pin 3 of the General Purpose Input-Output (GPIO) header which is connected to one of the GPIO channels.

6. Take the end of the other jumper lead and push it onto pin 25 of the GPIO header which is connected to ground.

    **Warning:** You can damage your Raspberry Pi if you do not use the GPIO pins correctly!

7. Make sure your Raspberry Pi has an internet connection, and speakers or headphones so that you can hear your jelly baby screaming. If you are using headphones or a speaker on the Raspberry Pi, you will need to type the following command to redirect sound to the headphone socket in the **Terminal**:

    `amixer cset numid=3 1`

## Step 2: Downloading and playing screams!

So far you have created your input device and have your Raspberry Pi set up and running. You now need to download a scream sound file and install some software to be able to play it. This task can be achieved from the command line.

1.  After logging into your Raspberry Pi you will see the following text:

    ```
    pi@raspberry ~ $
    ```
    The Raspberry Pi is waiting for you to type in a command to do something. This is referred to as the command line.

2.  Download an mp3 sound effect to play when the jelly baby is pressed. Enter the following command; it should be typed on one line with the same uppercase and lowercase characters:

    ```
    wget http://goo.gl/MOXGX3 -O la.mp3 --no-check-certificate
    ```

3.  Now test that you can play the sound file using `omxplayer` by typing:

    ```
    omxplayer la.mp3
    ```

    `omxplayer` will play the downloaded sound file and you should hear it from the speakers or headphones connected to your Pi.

    If you cannot hear anything, make sure that your headphones or speakers are connected correctly.  If the jack/plug looks like the picture below (notice the three black bands) you may find that it will only work if you pull the plug out by a few millimetres.

    ![](./images/3-5mmjack.jpg)

## Step 3: Write a program in Python

The final step to make your jelly baby scream is to write a program in Python; it will detect when you press the jelly baby input device and output the scream sound.


1. To write your Python program you will need to open a text editor window from the command line. To do this type the following command:

    ```
    nano scream.py
    ```

2. Begin your program by importing the modules and libraries needed to make it work. Type the following command:

    ```python
    import time
    import RPi.GPIO as GPIO
    import os
    ```

    The time library will be used to make the program pause for a fixed amount of time. The Raspberry Pi GPIO libraries will be used to connect the Raspberry Pi to other physical devices via the General Purpose Input-Output (GPIO) pins, in this case your jelly baby input device! The `os` library will be used to allow our program to call other programs that run on the Raspberry Pi like `omxplayer`.

3. Now you will need to set up the GPIO pins to use GPIO board pin numbers. Leave a line empty by pressing Enter on your keyboard, then type:

    ```python
    GPIO.setmode(GPIO.BCM)
    ```
    
4. To switch off the "Ports already in use" warnings, press Enter to give you a new line and type:

    ```python
    GPIO.setwarnings(False)
    ```
    
5. Set pin 3 on the GPIO header to be an input with the following command:

    ```python
    GPIO.setup(4,GPIO.IN)
    ```
    
6. Create a loop that runs forever and plays the screaming sound file when the two wires inside the jelly baby are touching by typing the following:

    ```python
    while True:
        if GPIO.input(4) == False:
            os.system('omxplayer la.mp3')
            time.sleep(1);
    ```

7. Save the file by pressing `CTRL+X`, then `Y` for yes, followed by `Enter`.

8. Finally, run the program by typing:

    ```
    sudo python scream.py
    ```

    **Congratulations!** Now when you press the jelly baby, the wires will touch and the mp3 file will play.

9. Exit the program when you are finished by pressing `CTRL+C`.

## What's next?

- Using a real button or switch connected to a breadboard
- Changing the sound that plays when the device is pressed
- Can you think of a way to use more inputs?

