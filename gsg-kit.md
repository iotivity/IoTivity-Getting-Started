![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**IoTivity.org**](https://iotivity.org)

# Getting Started with IoTivity (Raspberry Pi Kit)

## Introduction

This Getting Started guide will show you how to quickly download, build, and run IoTivity apps, featuring two-way communication between a Linux device and a Raspberry Pi with an add-in Pimoroni board. This simple platform enables you to quickly prototype the capabilities of your planned smart device:

- The *server*, a command-line app, runs on a smart home device, such as a smart thermostat, represented by the Raspberry Pi board.
- The *client*, a GUI app, controls the smart device from a Linux computer or tablet.

The two apps talk to each other over Wi-Fi, using the OCF protocol. 

![OCF protocol](/Images/communication-over-ocf-protocol.png)

## Requirements

To carry out this tutorial, you will need the following:

- Raspberry Pi board with microSD card with Raspbian OS
- Pimoroni Explorer HAT board
- Optional: HDMI monitor and cable for the Pi
- Optional: USB mouse for the Pi
- Ethernet connection between a DHCP-enabled network and the Pi
- Linux computer or tablet on the same network as the Pi

The first two listed items are sold together as a kit [here](https://openconnectivity.org/developer/developer-kit) (scroll down, below "Development Resources and Solutions").

## Set up the Raspberry Pi

1. *Before* connecting power, attach the Explorer HAT board to the GPIO header on the Raspberry Pi. Be careful not to bend the pins, as the connector fits very tightly. (At this point, you don’t need the blue breadboard, which may be attached later.)

   ![OCF protocol](/Images/attach-HAT-plus-blue-board.png)

2.	Insert the micro SD card into its slot, located under the Pi board.
3.	Connect an Ethernet cable between the Pi board and network.
4.	Attach the power cable to the Pi board, and plug it in.

   The board will boot.

## Connect to the Raspberry Pi

As an alternative to using SSH (per steps provided in this section), attach a monitor and USB keyboard to the Raspberry Pi. 

1. Open a terminal on your development PC.

2. Learn the Raspberry Pi board’s IP address by giving this command, then pressing ctrl-C. Use the host name of the Pi (or replace with the current hostname, if Pi name had been changed):

   ```
   ping raspberrypi.local
   ```

   ![ping Pi](/Images/ping-pi-local.png)

   In the screen above, the IP address is 192.168.0.30.
   
   Sometimes the ping command doesn't reach raspberrypi.local due to DNS issues. An alternative is to connect a keyboard and monitor to the Pi and run the ifconfig command in the terminal.

4. Connect to the Pi via SSH, using either of these commands:

   For Linux or macOS, use either of these commands:

   ```
   ssh pi@raspberrypi.local #replace with current hostname if changed, OR...
   ```

   ​		OR

   ```
   ssh pi@ipaddress #use IP address from previous step
   ```

5. Supply the password when prompted. Default login: 
   *username* **pi**
   *password* **raspberry**

   ![ssh prompt](/Images/ssh-prompt.png)

You’re now ready to install IoTivity code and samples.

## Install IoTivity and Pi Samples

1. Continuing on your development PC, from the SSH prompt, go to the home directory and install the server app, which takes several minutes to complete:

   ```
   cd ~
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash
   ```
   Alternatively, you can download the install.sh script, review and run it from anywhere.

2. Install manufacturer certificates:

   ```
   cd ~/iot-lite; ./manufacturer_pki.sh; cd ~
   ```

   ![install certificates](/Images/install-certificates.png)

3. Install the project scripts:

   ```
   curl https://openconnectivity.github.io/Project-Scripts/install.sh | bash
   ```

   Rerun this script, if an error occurs.

4. Install the repository containing sample code, which takes several minutes to run. Answer “y” when prompted:

   ```
   curl https://openconnectivity.github.io/Emulator-Code/emulator/install.sh | bash
   ```

5. Build the sample project in a new directory:

   ```
   create_project.sh myproject
   cd myproject
   cp ~/Emulator-Code/IoTivity-lite/dimming/setup.sh ./
   ./setup.sh
   gen.sh
   build.sh
   reset.sh
   run.sh
   ```
   
   A GUI light bulb with a switch and slider will appear in the Linux application window.

### Set up the Project Environment

1. Before you begin, be sure that the Raspberry Pi is set to use your preferred keyboard. UK English is the Pi’s preset keyboard layout. To choose another keyboard layout:

   ```
   sudo raspi-config #enter the Pi account password, if prompted.
   ```
   
2. In the Raspberry Pi Software Configuration Tool (raspi-config) menu, choose:

   * **Localisation Options** or **Internalization Options**
   * **Change Keyboard Layout**

   Select your keyboard and preferred keyboard layout. For example, for American English, after you select your connected keyboard, choose **English (US)**. Navigate through the menus to **save** and **exit** raspi-config.

   Then sudo reboot:

   ```
   sudo reboot
   ```

3. On the Pi, create a project directory:

   ```
   cd ~
   mkdir workspace
   cd workspace
   ```

4. Create the IoTivity project:

   ```
   /home/pi/workspace/create_project.sh myexample
   cd myexample
   ```

5. Copy the sample project to the current directory and set it up:

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

Leave this terminal window open. The server app is now waiting for commands from the client app, which you’ll install next.

## Install and Run the Client App

The sample client application is called OTGC (Onboarding Tool and Generic Client). It's prebuilt, so you'll just install the binary with a script:

1. Open a terminal window on your development PC.

2. Download and install the Linux OTGC client by running this command, which takes several minutes to complete:

   ```
   curl https://openconnectivity.github.io/otgc-linux/setup.sh | bash
   ```

   **Troubleshooting:** If an error occurs, manually run the dpkg command from the setup.sh script.

   ```
   sudo dpkg -i ./otgc-linux/build/debian/out/otgc-2.7.0.deb #run only in the event of an error
   ```

3. Launch the Linux OTGC client by running this command:

   ```
   /usr/bin/otgc.sh
   ```

4. Click to OK the End User License Agreement.

   OTGC starts and automatically scans all visible OCF (Open Connectivity Foundation) devices, listing them in the app's left-hand pane.

5. Locate and align both the terminal window that is awaiting incoming connections, plus the app window, so that both are visible. 

   As you proceed with the remaining steps in this section, notice that each action taken in the client app generates console output in the terminal window that had been awaiting incoming connections. This simulates controlling your smart home device with, for example, a mobile phone client:

   - Click to select the device listed in the left-hand pane, and click the Onboard button.

     The Select OTM (Ownership Transfer Method) dialog box pops up.

   - OK the Select OTM dialog box.

     As device ownership is transferred, the Select OTM dialog box closes and is replaced by the Set Device Name dialog box.

   - Change the device name, if you wish. Click OK to close the dialog box.

   - Click to reselect the device in the left-hand pane. In the Generic Client tab, toggle the Value switch on and off. 

6. **[Todo OCF: We could not successfully execute the remaining steps.]** Quit the client app and then press Ctrl-C in the server terminal to exit the process.

7.	Onboard (pair) the discovered server by clicking the + icon next to the device. **[Todo OCF: insert screenshot of Linux client screen, callout to + button]** 
   
   If the item has a gear icon instead of a + icon, it has already been onboarded. You can select the server and click Offboard to prepare to see the onboarding process.

8.	Once the + icon has changed to a gear, click the gear icon. **[Todo OCF: insert screenshot with callout to gear]** 

9.	Find the /LED1, /LED2, and /LED3 sections and in each, click the switch button on the left. **[Todo OCF: insert screenshot /LED section with callout to value button]** 
   
   The colored LEDs on the Explorer HAT board turn on or off, controlled by the client app over the OCF protocol. Notice that the console output in the server terminal on the Pi responds to your actions in the client.

10.	Now “observe” (monitor) the touch buttons on the Explorer HAT board in the OTGC app by clicking the switch buttons on the right of the /touch1, /touch2, and /touch3 sections. Physically touch the buttons on the board numbered 1, 2, and 3. **[Todo OCF: insert screenshot]** 

   Notice that the output in the OTGC app detects the touches.

11. Press Ctrl-C in the server terminal on the Pi to exit the server app.

## Customize the Code

***
**[Todo OCF: This section needs verification and some detail where noted]**
**[It should not be the same example as in the SW Simulation tutorial. It should be device-relevant.]
***

IoTivity provides a tool for automatically generating server code as a significant head start for your software development. The code generation tool works from a JSON file created by you that describes the capabilities of your device. The server code you compiled and ran in this tutorial began from example.json file, found in the ~/iot-lite/ directory on your development PC.

The steps below will show you how to make a simple change to the JSON file, recompile, and run the server and client. You can then see how the changes you made to the server’s capabilities in the JSON file are reflected in the client app. 

1. On your development PC, back up the example.json file:

   ```
   cd ~/iot-lite/
   cp example.json example.json.bak
   ```

2. Open the example.json file in your preferred editor. 

3. **[Todo OCF: Insert here the editing changes that user will make]**

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
***
**[Todo OCF: Based on the detail in step 3 above, insert screenshot of relevant section in OTGC with callout to changes]**
***

## Digging deeper: Next steps for development

Now that you've created a device simulation based on IoTivity, you're read to dig deeper to explore other platforms and learn how to apply IoTivity to your own platform and devices.

[**Digging Deeper**](digging-deeper.md)


