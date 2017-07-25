## Write a program in Python

The final step to make your jelly baby burp is to write a program in Python. The program will detect when you press the jelly baby input device, and will output the burp sound.

- Go to `Menu` > `Programming` > `Python 3 (IDLE)`.

- Once IDLE 3 has opened, click on **File** and **New File**. This will open a blank file. Click on **File** and **Save As** and name the file `burp.py`.

- Begin your program by importing the modules and libraries needed to make it work. Type the following:

    ```python
    from gpiozero import Button
    import pygame
    from time import sleep
    ```

    This allows you to find out when the button has been pushed using `gpiozero`, and allows you to use `pygame` to play a sound. The `time` library is used to pause the program for a while.
    
- Next, you need to tell your program which GPIO pin the jelly baby is attached to:

    ``` python
    jelly_baby = Button(3)
    ```

- You also need to initialise `pygame` and import the sound into your program:

    ``` python
    pygame.init()
    pygame.mixer.init()

    burp = pygame.mixer.Sound("burp.wav")
    ```
- Lastly, you can use an infinite loop to wait for the jelly baby to be pushed and then play the sound:
    ``` python
    while True:
        jelly_baby.wait_for_press()
        burp.play()
        sleep(2)
        burp.stop()
    ```

- Save the file by clicking on **File** and **Save**.

- Finally, run the program by clicking on **Run** and **Run Module**.

    **Congratulations!** Now when you press the jelly baby, the wires will touch and the burp sound file will play.


