# Burping Jelly Baby

In this resource, you can make a jelly baby burp when ever you give it a squeeze.

To turn a simple jelly baby into a switch, you will attach cables to it and then connect them to the GPIO pins on a Raspberry Pi.

## Raspberry Pi GPIO pins

1. The image below shows a RasPiO pin label, that can help to identify what each pin on the Raspberry Pi is used for, but if you don't have one then you can use the image as a guide to the Raspberry Pi GPIO pins.

![gpio label](images/raspio-ports.jpg)

1. The pins labelled with `GP` before a number are the GPIO pins. So `GPIO 17`, for instance, is labelled `GP17`. GPIO pins can be used to output 3.3 volts, or they can be used to detect high or low voltages.

1. There are two pins labelled `3V3` both of which provide power at **3.3 volts**. There are also two pins labelled `5V` that provide power at **5 volts**.

1. There are also 8 pins labelled `GND` which stands for **ground**.

## Wiring up the Jelly Baby

1. Take two metal paper clips (or pins if you are using them) and unfold them to make a straight wire.

1. Take a female to female jumper lead and push the paper clip wire into one of the ends.

1. Do the same to the other wire so that you have two identical jumper cables with paper clip wires in one end.

1. Insert the paper clips into a jelly baby so that they are close to each other but not touching.

1. Now attach the free ends of the jumper leads into `GPIO 3` and any `GND` pin.

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
    cp /opt/sonic-pi/etc/samples/misc_burp.flac burp.flac
    ```
    
    This will copy the misc_burp sound file from the sonic-pi folder into the jellybaby folder and rename it to burp.flac

1. Now you need to convert it to a wav file. To do this you can use `avconv`. In the terminal type:

    ``` bash
    avconv -i burp.flac burp.wav
    ```

3.  Now test that you can play the sound file using `omxplayer` by typing:

    ```
    omxplayer burp.wav
    ```

`omxplayer` will play the sound file and you should hear it from the speakers or headphones connected to your Pi.

## Write a program in Python

The final step to make your jelly baby burp is to write a program in Python; it will detect when you press the jelly baby input device and output the burp sound.


1. Go to `Menu` > `Programming` > `Python 3 (IDLE)`

1. Once IDLE3 has opened, click on **File** and **New File**. This will open a blank file. Click on **File** and **Save As** and name the file `burp.py`

1. Begin your program by importing the modules and libraries needed to make it work. Type the following:

    ```python
    from gpiozero import Button
    import pygame
    from time import sleep
    ```

    This allows you to find out when the button has been pushed using `gpiozero` and allows you to use `pygame` to play a sound. The `time` library is used to pause the program for a while.
    
1. Next you need to tell your program which GPIO pin the Jelly Baby is attached to.

    ``` python
    jelly_baby = Button(3)
    ```

1. You also need to initialise `pygame` and import the sound into your program.

    ``` python
    pygame.init()
    pygame.mixer.init()

    burp = pygame.mixer.Sound("burp.wav")
    ```
1. Lastly you can use an infinite loop to wait for the jelly baby to be pushed and then play the sound.

``` python
while True:
    button.wait_for_press()
    burp.play()
    sleep(2)
    burp.stop()
```

1. Save the file by clicking on **File** and **Save**.

1. Finally, run the program by clicking on **Run** and **Run Module**

    **Congratulations!** Now when you press the jelly baby, the wires will touch and the burp sound file will play.


## What's next?

- Using a real button or switch connected to a breadboard
- Changing the sound that plays when the device is pressed
- Why not create a whole music box with our [GPIO Music Box tutorial](http://www.raspberrypi.org/learning/gpio-music-box/). 

