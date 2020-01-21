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

To carry out this tutorial, you need the following:

- A Debian-based Linux PC (e.g., Ubuntu), with an internet connection.

## Install and Run the Server App

1. On the Linux PC, open a terminal.

2. Download source and set up the IoTivity-Lite environment by running this command:

   ```
   curl https://openconnectivity.github.io/IOTivity-Lite-setup/install.sh | bash 
   ```

   Alternatively, you can download the install.sh script, review it, and run it from anywhere. 

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

The server app is now waiting for commands from the client app, which you’ll install next.

## Install and Run the Client App

The sample client application is called OTGC (Onboarding Tool and Generic Client). It’s prebuilt, so you’ll just install the binary with a script.

1. Open another terminal.

2. Download and install the Linux OTGC client by running this command:

   ```
   curl https://openconnectivityfoundation.github.io/development-support/otgc/linux/install.sh | bash
   ```

3. Launch the Linux OTGC client by running this command:

   ```
   /usr/bin/otgc.sh
   ```

   The client application loads, and your server device (which, in this simulation, is simply another process on your PC) appears in the list.

   ![client application loads](/Images/client-application-loads.png)

4. Click the server device in the list and click the Onboard button.

   ![onboard button](/Images/onboard-button.png)

5. Change the device name, if you wish, and click OK.

6. In the Generic Client tab, toggle the Value switch on and off. 

   ![value switch](/Images/toggle-switch.png)

   Notice that the console output in the server terminal responds to the actions in the client. This simulates controlling your smart home device with, for example, a mobile phone client.

7. Quit the client app and press Ctrl-C in the server terminal to exit the process.

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

6.	As before, select the discovered device. Notice the changed capabilities.
***
**[Todo Concrete: after OCF provides detail in step 3 above: insert screenshot of relevant section in OTGC with callout to changes]**
***

## Run on Separate Devices

Now that you’ve run a quick simulation on your own development PC to experience the basic flow, you can get a better picture of IoTivity capabilities by running it on a Raspberry Pi board, where you can control and read its status from an Linux application. 

A workshop kit includes a Pimoroni input/output board that most clearly shows the capabilities of IoTivity. If you already have a Raspberry Pi board and don’t want to order the full kit, you can run a simpler demonstration.

### [Tutorial for Raspberry Pi kit with input/output](gsg-kit.md)

Sample project code and instructions for kit including Raspberry Pi and Pimoroni Explorer HAT input/output board.

### Tutorial for plain Raspberry Pi with output only
***
   **[Todo OCF: If we want to support a bare Raspberry Pi board, we need this tutorial information]**
***
Sample project code and instructions for bare Raspberry Pi board.

## Next Steps for Development

To learn more about developing IoT devices with IoTivity, read the following:

### [Development workflow tutorial](https://github.com/openconnectivity/IOTivity-Lite-setup/blob/master/Readme.md)
***
   **[Todo OCF: Provide a suitable destination for this "Development workflow tutorial" link. The tutorial would go beyond the simple Customize the Code exercise above. It will walk the developer through creating a new project from scratch. Is this the PowerPoint translated by OCF into a PDF or markdown?]**
***

Create a whole separate test project (create configuration file, generate device server code, build and use). 

### [Development workflow reference](https://github.com/openconnectivity/IOTivity-Lite-setup/blob/master/Readme.md)

Folder structure, recommended development flow and description of core scripts.

### [Detailed programming guide](https://wiki.iotivity.org/)

From initializing the stack through managing scenes and details in between.

