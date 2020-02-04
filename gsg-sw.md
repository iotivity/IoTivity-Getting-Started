![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**Wiki**](https://wiki.iotivity.org/start)   |   [**IoTivity.org**](https://iotivity.org)

# Getting Started with IoTivity (Device Simulation)

## Introduction

This guide will show you how to download, build, and run two simulated devices on the same Linux PC:

- The *server*, a command-line app, simulates a smart home device such as a smart thermostat.
- The *client*, a GUI app, controls the smart device. The client typically runs on a smart phone.

The two apps talk to each other over a loopback connection, using the OCF protocol. 

![OCF protocol over loopback connection](/Images/ocfprotocol-loopback-connection.png)

**To use Windows:** To download, build, and run on a Windows PC instead, check the Iotivity [FAQ](https://wiki.iotivity.org/getting_started_troubleshooting_and_faq).

## Requirements

To carry out this tutorial, you will need the following:

- A Debian-based Linux PC (e.g., Ubuntu), with an internet connection.

## Install and Run the Server App

1. On the development PC, open a terminal.

2. Download source and set up the IoTivity-Lite environment by running this command, which takes several minutes to complete:

   ```
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash 
   ```

   Alternatively, you can download the install.sh script, review and run it from any location. 

3. Generate code for the server app by running these commands:

   ```
   cd ~/iot-lite/
   ./gen.sh
   ```

   This script runs the DeviceBuilder app with a default JSON configuration file that can be edited to specify the capabilities of your actual device.

4. Build and run the server app by running these commands:

   ```
   ./build.sh
   ./run.sh
   ```

Leave this terminal window open. The server app is now waiting for commands from the client app, which you’ll install next.

## Install and Run the Client App

The sample client application is called OTGC (Onboarding Tool and Generic Client). It's prebuilt, so you'll just install the binary with a script:

1. On the development PC, open another terminal window.

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

   ![/usr/bin/otgc.sh](/Images/usr-bin-otgc.sh.png)

4. Click to OK the End User License Agreement.

   ![client application loads](/Images/client-application-loads.png)

   OTGC starts and automatically scans all visible OCF (Open Connectivity Foundation) devices, listing them in the app's left-hand pane. In the screen above, the device found is called server_lite_3173.

5. Locate and align both the terminal window that is awaiting incoming connections, plus the app window, so that both are visible. 

   As you proceed with the remaining steps in this section, notice that each action taken in the client app generates console output in the terminal window that had been awaiting incoming connections. This simulates controlling your smart home device with, for example, a mobile phone client:

   - Click to select the device listed in the left-hand pane, and click the Onboard button.

     ![select device and onboard](/Images/onboard-button.png)

     The Select OTM (Ownership Transfer Method) dialog box pops up.

   - OK the Select OTM dialog box.

     ![select OTM](/Images/set-device-name.png)

     As device ownership is transferred, the Select OTM dialog box closes and is replaced by the Set Device Name dialog box.

   - Change the device name, if you wish. Click OK to close the dialog box.

     In this example, the device name will be changed to server_lite_####.

   - Click to reselect the device in the left-hand pane. In the Generic Client tab, toggle the Value switch on and off. 

     ![toggle value switch](/Images/toggle-switch.png)

9. Quit the client app and then press Ctrl-C in the server terminal to exit the process.

## Customize the Code

***
**[Todo OCF: This section needs verification and some detail where noted]**

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

6. As you observed in Step 5 of the **Install and Run the Client App** section above, notice how the console output in the server terminal responds to actions taken in the client app:

   * Click to select the device and click the Onboard button.
   * OK the Select OTM dialog box.
   * Change the device name, if you wish, and click OK to close the Set Device Name dialog box.
   * Click to reselect the device. In the Generic Client tab, toggle the Value switch on and off.

7. Quit the client app and then press Ctrl-C in the server terminal to exit the process.
***
**[Todo Concrete: after OCF provides detail in step 3 above: insert screenshot of relevant section in OTGC with callout to changes]**

***

## Run on Separate Devices

Now that you’ve run a quick simulation on your own development PC and experienced the basic flow, you can get a better picture of IoTivity capabilities by running it on a Raspberry Pi board, where you can control and read its status from a Linux application. 

A workshop kit includes a Pimoroni input/output board that is used to demonstrate the capabilities of IoTivity. If you already have a Raspberry Pi board and don’t want to order the full kit, you can run a simpler demonstration.

### [Tutorial for Raspberry Pi kit with input/output](gsg-kit.md)

Sample project code and instructions for kit including Raspberry Pi and Pimoroni Explorer HAT input/output board.

### Tutorial for plain Raspberry Pi with output only
***
   **[Todo OCF: If we want to support a bare Raspberry Pi board, we need this tutorial information]**
***
Sample project code and instructions for bare Raspberry Pi board.

## Digging deeper: Next steps for development

Now that you've created a device simulation based on IoTivity, you're read to dig deeper to explore other platforms and learn how to apply IoTivity to your own platform and devices.

[**Digging Deeper**](digging-deeper.md)