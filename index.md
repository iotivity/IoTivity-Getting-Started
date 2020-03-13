![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**IoTivity.org**](https://iotivity.org)

# Introduction

IoTivity is an open source framework that implements the [OCF](https://openconnectivity.org) (Open Connectivity Foundation) protocol for easy, secure device-to-device communication for IoT devices. IoTivity includes the following:

- A reference implementation of **client software** -- for example, the OTGC (Onboarding Tool and Generic Client) app for controlling a smart home or other IoT device (available on Linux or Android)
- A reference implementation of **server software** that runs on the actual IoT device
- **Tools that generate code** for the server, based on a JSON file that you will create to describe your device’s capabilities

# Learning to Use IoTivity

These 15-30 minute tutorials walk through installing, building, and using client and server software applications that rely on IoTivity capabilities. Then, the Digging Deeper section provides the how-to and reference information needed to implement IoTivity on your own device.

[**Getting Started with IoTivity (Device Simulation)**](gsg-sw.md)

- Quickly simulates smart device usage by running client and command-line server apps on the same Linux PC, using the OCF protocol to communicate over loopback.

[**Getting Started with IoTivity (Graphical Device Simulation)**](gsg-gtk.md)

- In this example you build a server with a graphical user interface (GUI). The GUI also has a switch and a slider, so you can make changes on the server and observe them in the client. We are still running both the client and the server on the same machine in loopback mode.

[**Getting Started with IoTivity (Raspberry Pi kit)**](gsg-kit.md)

- Experience realistic smart device usage with a Raspberry Pi kit ([purchase here](https://openconnectivity.org/developer/developer-kit), under <u>Development Resources and Solutions</u>). The kit provides for a more immersive experience. With the kit and a Linux or Android client app, you can control a Raspberry Pi equipped with colored LEDs and capacitive touch buttons on an add-on board.

[**Digging Deeper: Next Steps for Development**](digging-deeper.md)
