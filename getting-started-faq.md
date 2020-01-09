![IoTivity logo](/Images/IoTivity-logo.png)

[**Getting Started**](index.md)   |   [**Getting Started FAQ**](getting-started-faq.md)   |   [**Digging Deeper**](digging-deeper.md)   |   [**GitHub Repository**](https://github.com/iotivity/iotivity-lite)   |   [**Wiki**](https://wiki.iotivity.org/start)   |   [**IoTivity.org**](https://iotivity.org)

# Getting Started FAQ

If you're having issues getting started with IoTivity-Lite, these common questions and answers should help.

* **I'm having issues with curl:**
  * The IoTivity-Lite installer script can be found [here](https://github.com/openconnectivity/IOTivity-setup/blob/master/install.sh).
  * The OTGC installer script can be found [here](https://github.com/openconnectivityfoundation/development-support/blob/master/otgc/linux/install.sh).
  * Both scripts can be copied to a local .sh files and executed if the curl command is failing.
  * Ran all scripts as superuser.
* **I'm building on Windows:**
  * Check the "Building sample applications on Windows" section of the "README.rst" file, found in the "IoTivity-constrained" directory, under the IoTivity-Lite project directory.
* **I'm not building on Windows or Ubuntu Linux 18, and have generic toolchain issues:**
  * Try installing Ubuntu Linux 18 or creating an Ubuntu 18 VM using VMWare Workstation (free download for non-commercial use).
* **I need an OCF feature that is not present in Lite**
  * Take a look at IoTivity "main," which is the older open source reference implementation of OCF Specifications 2.0.0 and prior. Get started building "main using the [IoTivity build instructions](https://wiki.iotivity.org/build_for_your_system).
* **Is there an Android client?**
  * Yes! The Android version of the OTGC can be installed following [these](https://github.com/openconnectivityfoundation/development-support/blob/master/otgc/README.md#install-otgc-on-android-501-or-later) directions.
* **What is "IoTivity-constrained?"**
  * IoTivity-Constrained is the former name for IoTivity-Lite; they're the same thing. IoTivity-Lite is the newer and correct name, although the constrained term still hangs around on some URLs, etc. For more info on IoTivity-Lite, visit [About IoTivity-Lite](https://iotivity.org/about-iotivity-lite).
* **Still no luck?**
  * Ask your question on the **IoTivity-dev email reflector**.
