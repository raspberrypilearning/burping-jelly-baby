## Sound of a burp!

So far, you've created your input device and have your Raspberry Pi set up and running. You now need to find a burping sound file and move it into a new folder. This can all be achieved in a terminal window, which can be opened by pressing `Ctrl` + `Alt` + `T`.

- Create a new folder called `jellybaby` with the following command:

    ```bash
    mkdir jellybaby
    ```

- Enter the folder with `cd jellybaby`.

    We're going to need a *burping* sample sound file for this project. You could find your own one online, or use the one provided in the next step.

- Download a copy of a burp sound effect with the following command:

    ```bash
    wget http://rpf.io/burp -O burp.wav
    ```
    
-  Now test that you can play the sound file using `aplay` by typing:

    ```
    aplay burp.wav
    ```

    `aplay` will play the sound file and you should hear it from the speakers or headphones connected to your Pi.


