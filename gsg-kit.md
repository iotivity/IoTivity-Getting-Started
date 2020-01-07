![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](gsg-home.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**Wiki**](https://wiki.iotivity.org/start)   |   [**IoTivity.org**](https://iotivity.org)

# Getting Started with IoTivity (Raspberry Pi Kit)

## Introduction

This Getting Started guide will show you how to quickly download, build, and run IoTivity apps featuring two-way communication between an Android device and a Raspberry Pi with an add-in Pimoroni board. This simple platform enables you to quickly prototype the capabilities of your planned smart device:

- The *server*, a command-line app, runs on a smart home device, such as a smart thermostat, represented by the Raspberry Pi board.
- The *client*, a GUI app, controls the smart device from an Android phone or tablet.

The two apps talk to each other over Wi-Fi, using the OCF protocol. 

![OCF protocol](/Images/communication-over-ocf-protocol.png)

## Requirements

To carry out this tutorial, you will need the following:

- Raspberry Pi board with microSD card with Raspbian OS
- Pimoroni Explorer HAT board
- Ethernet connection to your network for the Pi
- Android phone or tablet on the same LAN as the Pi

The first two items are available together in a kit [here](https://openconnectivity.org/developer/developer-kit) (under Development Resources and Solutions).

## Set up the Raspberry Pi

1. *Before* connecting power, attach the Explorer HAT board to the GPIO header on the Raspberry Pi. Be careful not to bend the pins, as the connector fits very tightly. (At this point, you don’t need the blue breadboard, but you can attach it later, with adhesive, to add other inputs and outputs to your IoTivity test setup.) 
![OCF protocol](/Images/attach-HAT-plus-blue-board.png)
3. Insert the micro SD card into the slot under the Pi board.
4. Connect an Ethernet cable between the Pi board and your DHCP-enabled network.
5. Attach the power cable to the Pi board and plug it in.
   The board will boot.

If you don’t want to use SSH (steps provided in the next section), attach a monitor and USB keyboard. 

## Connect to the Raspberry Pi

1. Open a terminal on your development PC.

2. Get the Raspberry Pi board’s IP address by giving this command with the host name of the Pi (or replace it with the current hostname, if you’ve changed it):

   ```
   ping raspberrypi.local
   ```

   **[insert screenshot of ping command output]**
   In the screen above, the IP address is **[fill in from screenshot]**.

3. Use the IP address to connect to the Pi via SSH:

   - For Linux or macOS, use either of these commands:

   ```
   ssh pi@raspberrypi.local
   ```

   ​		Replace with current hostname, if changed.

   ​		OR...

   ```
   ssh pi@ipaddress
   ```

   ​		Use IP address from previous step.

   - 
     For a Windows PC, follow the documentation in Putty or a similar terminal program to make the SSH connection.

4. Supply the password when prompted. Default login: 
   *username* **pi**
   *password* **raspberry**
   **[insert screenshot of SSH prompt]**

You’re now ready to install IoTivity code and samples.

## Install IoTivity and Pi Samples

1. From the SSH prompt, go to the home directory and install IoTivity:

   ```
   cd ~
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash
   ```

2. Install the project scripts:

   ```
   [curl]() https://openconnectivity.github.io/Project-Scripts/install.sh | bash
   ```


   Rerun this script if an error occurs.

3. Install Pi example code, answering “y” to the many prompts:

   ```
   curl https://openconnectivity.github.io/Sample-Raspberry-Pi-Code/pi-boards/install.sh | bash
   ```


   This script takes several minutes to run.

4. Make sure changes to the PATH variable are active with this command:

   ```
   source ~/.bashrc
   ```

### Set up the Project Environment

1. On the Pi, create a project directory:

   ```
   cd ~
   mkdir workspace
   cd workspace
   ```

2. Create the IoTivity project:

   ```
   create_project.sh]() myexample
   cd myexample
   ```

3. Copy the sample project to the current directory and set it up:

   ```
   cp ~/Sample-Raspberry-Pi-Code/IoTivity-lite/explorer-hat-pro/setup.sh .
   ./setup.sh
   ```

The sample project now has Explorer HAT drivers installed and is ready for code generation and building.

## Build and Run the Server App

1. On the Pi, generate code for the server app by running these commands:

   ```
   cd ~/iot-lite/ #path where you installed IoTivity
   ./gen.sh
   ```

   This script starts from a default JSON configuration file that can be edited to specify the capabilities of your actual device. The script calls the DeviceBuilder app to generate source code for the server app you’ll run on your smart device (in this case, the Pi).

2. Build the server app with this command:

   ```
   ./build.sh
   ```

3. Reset and run the server app by running these commands:

   ```
   ./reset.sh
   ./run.sh
   ```

The server app is now waiting for commands from the client app, which you’ll install next.

## Install and Run the Client App

The sample client application is called OTGC (Onboarding Tool and Generic Client) and can run on Android. It’s prebuilt, so you’ll just side-load the APK file on your Android device.

1.	Find the OTGC APK file from the USB flash drive that came with your development kit.
You can also [download the file](https://github.com/openconnectivityfoundation/development-support/blob/master/otgc/android/otgc-debug.apk) from GitHub.
2. Install the APK file on your Android Device.

   Search the web for “how to sideload APK” to find [instructions](https://www.digitaltrends.com/mobile/how-to-sideload-an-apk/). Many sites explain the process.
3.	Launch the OTGC client on the Android device.
4.	Click the discover button to search for OCF devices on the same network.
**[insert screenshot of initial Android client screen, callout to discover button]**
5.	Onboard (pair) the discovered server by clicking the + icon next to the device.
**[insert screenshot of initial Android client screen, callout to + button]**
If the item has a gear icon instead of a + icon, it has already been onboarded. You can select the server and click Offboard to prepare to see the onboarding process.
6.	Once the + icon has changed to a gear, click the gear icon.
**[insert screenshot with callout to gear]**
7.	Find the /LED1, /LED2, and /LED3 sections and in each, click the switch button on the left.
**[insert screenshot /LED section with callout to value button]**
The colored LEDs on the Explorer HAT board turn on or off, controlled by the client app over the OCF protocol. Notice that the console output in the server terminal on the Pi responds to your actions in the client.
8.	Now “observe” (monitor) the touch buttons on the Explorer HAT board in the OTGC app by clicking the switch buttons on the right of the /touch1, /touch2, and /touch3 sections. Physically touch the buttons on the board numbered 1, 2, and 3.
**[insert screenshot]**
Notice that the output in the OTGC app detects the touches.
9.	Press Ctrl-C in the server terminal on the Pi to exit the server app.

## Customize the Code

**[Needs detail from OCF]**
IoTivity provides a tool for automatically generating server code as a significant head start for your software development. The code generation tool works from a JSON file created by you that describes the capabilities of your device. The server code you compiled and ran in this tutorial began from example.json file, found in the ~/iot-lite/ directory.

The steps below will show you how to make a simple change to the JSON file, recompile, and run the server and client. You can then see how the changes you made to the server’s capabilities in the JSON file are reflected in the client app. 

1. Back up the example.json file:

   ```
   cd ~/iot-lite/
   cp example.json example.json.bak
   ```

2. Open the example.json file in your preferred editor. 

3. **[Insert here the editing changes that user will make]**

4. While still in the ~/iot-lite/ directory, generate the server code, build, and run:

   ```
   ./gen.sh
   ./build.sh
   ./run.sh
   ```

5. Run the client app:

   ```
   /usr/bin/otgc.sh
   ```

6.	As before, select the discovered device. Notice the changed capabilities.
**[insert screenshot of relevant section in OTGC with callout to changes]**

## Next Steps for Development

To learn more about developing IoT devices with IoTivity, read the following:

### [Development workflow tutorial](https://github.com/openconnectivity/IOTivity-Lite-setup/blob/master/Readme.md)

Create a whole separate test project (create configuration file, generate device server code, build and use). **[To be developed by OCF. This tutorial will go beyond the simple Customize the Code exercise above. It will walk the developer through creating a new project from scratch.]**

### [Development workflow reference](https://github.com/openconnectivity/IOTivity-Lite-setup/blob/master/Readme.md)

Folder structure, recommended development flow and description of core scripts.

### [Detailed programming guide](https://wiki.iotivity.org/)

From initializing the stack through managing scenes and details in between.

