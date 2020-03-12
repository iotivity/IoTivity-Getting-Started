![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**IoTivity.org**](https://iotivity.org)

This guide will show you how to download, build, and run two simulated devices on the same Linux PC:

- The *server*, a GUI app in this case, simulates a smart home dimmable light. The switch and dimmer can be adjusted from the server GUI. This simulates a physical dimming light switch.
- The *client*, a GUI app, controls the smart device. The client typically runs on a smart phone.

The two apps talk to each other over a loopback connection, using the OCF protocol.

![OCF protocol over loopback connection](/Images/ocfprotocol-loopback-connection.png)

**To use Windows:** To download, build, and run on a Windows PC instead, check the Iotivity [FAQ](https://wiki.iotivity.org/getting_started_troubleshooting_and_faq).

## Requirements

To carry out this tutorial, you will need the following:

- A Debian-based Linux PC (e.g., Ubuntu), with an internet connection.

## Install IoTivity and Emulator Sample

1. On the development PC, open a terminal.

2. Download source and set up the IoTivity-Lite environment by running this command, which takes several minutes to complete:

   ```
   cd ~
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash
   ```

   Alternatively, you can download the install.sh script, review and run it from anywhere.


3. Install the project scripts:


   ```
   curl https://openconnectivity.github.io/Project-Scripts/install.sh | bash
   ```

   Rerun this script if an error occurs.


4. Install the repository containing emulator sample code. Answer “y” if prompted:


   ```
   curl https://openconnectivity.github.io/Emulator-Code/emulator/install.sh | bash
   ```

   You may need to run source ~/.bashrc or reboot the computer at this point to ensure that your environment variables are set.

  ```
  source ~/.bashrc

  or

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


   This script starts from a default JSON configuration file that can be edited to specify the capabilities of your actual device. The script calls the DeviceBuilder app to generate source code for the server app you’ll run on your smart device (in this case, the dimmable light Emulator app).

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

NOTE: Alternatively, you can run the Android version of OTGC on your smart phone or tablet. Get the installation package here: (https://github.com/openconnectivity/otgc-android). You can then just run it and skip the Linux OTGC installation in the steps below. The circle icon will start the discovery process and should find the Emulator server.

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


   - Click to reselect the device in the left-hand pane.


6.	Onboard (pair) the discovered server by clicking the + icon next to the device. If the item has a gear icon instead of a + icon, it has already been onboarded. You can select the server and click Offboard to prepare to see the onboarding process.


8.	Once the + icon has changed to a gear, click the gear icon.


9.	In OTGC, find the /binaryswitch and /dimming sections and click the switch value button on the left. The light bulb animation will turn on or off, controlled by the client app over the OCF protocol. Also, the dimming slider will move from 0 to 100. If you change the dimming value (type <Tab> to get the value accepted), the dimmer slider in the GUI should reflect what you type and the light animation should change. If you type 100, the light should turn on fully and the binary switch should turn on. Notice that the console output in the server terminal also responds to your actions in the client.


10.	Now “observe” (monitor) the touch buttons on the emulator window in the OTGC app by turning on the "observe" button on the /binaryswitch and /dimmer sections of OTGC, then clicking the switch button or dimming slider on the emulator application. Notice that the output in the OTGC app detects the changes in the emulator application.


11. Press Ctrl-C in the server terminal or click the "X" in the emulator window to exit the server app.


## Digging deeper: Next steps for development


Now that you've created a device simulation based on IoTivity, you're read to dig deeper to explore other platforms and learn how to apply IoTivity to your own platform and devices.


[**Digging Deeper**](digging-deeper.md)
