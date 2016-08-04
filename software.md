# Software installation

You'll need to make sure you have the following packages installed to proceed with the worksheet:

- libav-tools

You'll need to be online to install packages.

First update and upgrade your system. Enter the following commands in to the terminal:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Now install the package you'll need:

```bash
sudo apt-get install libav-tools
```

Test you have `avconv` installed correctly by running it on the command line:

```bash
avconv
```

This should show some information about the version of `avconv` you have installed and bring you back to the command prompt. If you get an error saying `The program 'avconv' is currently not installed` then check you entered the commands above correctly.
