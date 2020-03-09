![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**IoTivity.org**](https://iotivity.org)

# Getting Started with IoTivity (the Linux graphical user interface (GUI) using GTK)

## Introduction

This Getting Started guide will show you how to quickly download, build, and run IoTivity apps, featuring two-way communication between a Linux or Android device and a Linux dimmable light emulator server with a GUI and controls on the server. This simple platform enables you to quickly prototype the capabilities of your planned smart device:

- The *server*, a command-line app, runs here as a GUI emulator of a smart home device, such as a smart switch or smart thermostat. In this case, this is represented by emulator code on the Linux machine of a dimmable light.

- The *client*, a GUI app, controls the smart device from a Linux computer or Android tablet.

The two apps talk to each other via a loopback connection on the same machine, using the OCF (Open Connectivity Foundation) protocol. This also works for the code running on a different Linux machine if that machine is on the same local area network.


![OCF protocol](/Images/communication-over-ocf-protocol.png)


## Requirements

To carry out this tutorial, you will need the following:

- Linux computer


## Install IoTivity and Emulator Sample

1. Continuing on your development PC, from the terminal prompt, go to the home directory and install the IoTivity-lite development system, which takes a few minutes to complete:


   ```
   cd ~
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash
   ```

   Alternatively, you can download the install.sh script, review and run it from anywhere.


2. Install the project scripts:


   ```
   curl https://openconnectivity.github.io/Project-Scripts/install.sh | bash
   ```

   Rerun this script if an error occurs.


4. Install the repository containing emulator sample code, which takes several minutes to run. Answer “y” if prompted:


   ```
   curl https://openconnectivity.github.io/Emulator-Code/emulator/install.sh | bash
   ```

   You may need to reboot the Raspberry Pi at this point to ensure that your environment variables are set.

  ```
  sudo reboot -h now
  ```

5. Create a project directory:

   ```
   cd ~
   mkdir workspace
   cd workspace
   ```

6. Create the IoTivity project (we'll call it myexample):

    ```
    create_project.sh myexample
    cd myexample
    ```

5. Copy the sample project to the current directory and set it up:

   ```
   cp ~/Emulator-Code/IoTivity-lite/emulator/setup.sh ./
   ./setup.sh
   ```

The sample project now has all dependencies installed and is ready for code generation and building.


## Build and Run the Server App


1. Generate code for the server app by running these commands:

   ```
   cd ~/workspace/myexample (if not already there)
   gen.sh
   ```


   This script starts from a default JSON configuration file that can be edited to specify the capabilities of your actual device. The script calls the DeviceBuilder app to generate source code for the server app you’ll run on your smart device (in this case, the Pi).

2. Build the server app with this command:


   ```
   build.sh
   ```


3. Reset and run the server app by running these commands:


   ```
   reset.sh
   run.sh
   ```

A small window should open with a graphical image of a light bulb, an on/off switch and slider dimming switch.

Leave the terminal window open. The server app is now waiting for commands from the client app, which you’ll install next.



## Build and Run the Client App (If you've already installed OTGC once, you can skip the installation here and jump to step 3.)

NOTE: Alternatively, you can run the Android version of OTGC on your smart phone or tablet. Get the installation package here: (http://dfslfjsdf). You can then just run it and skip the Linux OTGC installation in the steps below. The circle icon will start the discovery process and should find the Raspberry Pi server (make sure you're on the same LAN).

The sample client application is called OTGC (Onboarding Tool and Generic Client). You'll download and build the binary with a script:

1. On the development PC, open another terminal window.

2. Download and build the Linux OTGC client by running this command, which takes several minutes to complete:

   ```
   curl https://openconnectivity.github.io/otgc-linux/setup.sh | bash
   ```

   **Troubleshooting:** If the build process finishes but an error occurs, manually run the dpkg command from the setup.sh script.

   ```
   sudo dpkg -i ./otgc-linux/build/debian/out/otgc-2.9.0.deb
   #run only in the event of an error and substitute the version of otgc
   #that is available at this location (for example, the version number will
   #increment as new versions are created (e.g. otgc-2.10.0.deb))
   ```

3. Launch the Linux OTGC client by running this command:


   ```
   /usr/bin/otgc.sh
   ```


4. Click to OK the End User License Agreement.


   OTGC starts and automatically scans all visible OCF devices, listing them in the app's left-hand pane.


5. Locate and align both the terminal window that is awaiting incoming connections, plus the app window, so that both are visible.


   As you proceed with the remaining steps in this section, notice that each action taken in the client app generates console output in the terminal window that had been awaiting incoming connections. This simulates controlling your smart home device with, for example, a mobile phone client:


   - Click to select the device listed in the left-hand pane, then click the Onboard button.



     The Select OTM (Ownership Transfer Method) dialog box pops up.



   - Click OK in the Select OTM dialog box.



     As device ownership is transferred, the Select OTM dialog box closes and is replaced by the Set Device Name dialog box.


   - Change the device name, if you wish. Click OK to close the dialog box.


   - Click to reselect the device in the left-hand pane. In the Generic Client tab, toggle the Value switch on and off.



6. **[Todo OCF: We could not successfully execute the remaining steps.]** Quit the client app and then press Ctrl-C in the server terminal to exit the process.


7.	Onboard (pair) the discovered server by clicking the + icon next to the device. **[Todo OCF: insert screenshot of Linux client screen, callout to + button]** If the item has a gear icon instead of a + icon, it has already been onboarded. You can select the server and click Offboard to prepare to see the onboarding process.


8.	Once the + icon has changed to a gear, click the gear icon. **[Todo OCF: insert screenshot with callout to gear]**


9.	Find the /light sections and click the switch button on the left. **[Todo OCF: insert screenshot /LED section with callout to value button]** The light bulb animation will turn on or off, controlled by the client app over the OCF protocol. Notice that the console output in the server terminal on the Pi responds to your actions in the client.


10.	Now “observe” (monitor) the touch buttons on the emulator window in the OTGC app by turning on the "observe" button on the switch and dimmer sections of OTGC, then clicking the switch button or dimming slider on emulator application. **[Todo OCF: insert screenshot]** Notice that the output in the OTGC app detects the changes in the emulator application. (This step does not apply if you do not have the Explorer HAT board.)


11. Press Ctrl-C in the server terminal or click the "X" in the emulator window to exit the server app.


## Digging deeper: Next steps for development


Now that you've created a device simulation based on IoTivity, you're read to dig deeper to explore other platforms and learn how to apply IoTivity to your own platform and devices.


[**Digging Deeper**](digging-deeper.md)
