

# TXT C/++ local executables workspace (Download Examples)
## Contact

> Version for TXT firmware 4.6.6 4.7.0 pre-release
 
> If you have any questions, please contact us: fischertechnik-technik@fischer.de

>  [For older firmware versions ](https://github.com/fischertechnik/txt_demo_c_download/releases). 

<!---
## TXT Programming

The fischertechnik TXT controller has an (embedded) Linux system that allows communication via WLAN, Bluetooth or USB interface. 
The network protocol is used for control by means of interfaces and the TXT can thus be directly activated via IP addresses. 

In the previous Robo interface, it was important to know whether the interface was connected to the computer via the serial interface or the USB interface and the programming varied accordingly.
In TXT, this differentiation has been done away with using the network protocol. Every interface of the TXT (USB, BT, WLAN) has a separate IP address. This makes the different programs more convenient and only the desired IP address must be used.

The sensors and actuators of the fischertechnik TXT controller can be controlled in two ways:

- **Online programming**
Here, a computer can control a controller via the USB cable, WLAN or Bluetooth (BT). The documentation can be found in 
[txt_demo_c_online](https://github.com/fischertechnik/txt_demo_c_online).

- **Download programming**
Here, a program is created with a cross compiler and transferred to the TXT, and it can be started there via the menu system. This documentation shows how an Eclipse development environment can be used to create C download programs for the TXT. You can also use other IDE, e. g. Visual Studio or CodeLite.
-->

## Overview of the Demo Programs
There are several sample programs that explain the control of the TXT.

The basic C program in download mode looks as following: 
```c
#include "KeLibTxtDl.h"     // TXT Lib
#include "FtShmem.h"        // TXT Transfer Area

// Common debugging stuff for RoboProLib
unsigned int DebugFlags;
FILE *DebugFile;

int main(void) 
{
	FISH_X1_TRANSFER    *pTArea;
	if (StartTxtDownloadProg() == KELIB_ERROR_NONE)
	{
		pTArea = GetKeLibTransferAreaMainAddress();
		if (pTArea)
		{ 
      //...
		}
		StopTxtDownloadProg();
	}
	return 0;
}
```
## Overview of available examples

### TxtDeps
[See also the project Readme](./TxtDeps/README.md)
This project contains the libraries and includes belowing to the libraries and tools which are available on the TXT.<br/>
This is the same for the SLI's.

### TxtDemo00_HelloWorld
[See also the project Readme](./TxtDemo00_HelloWorld/README.md)

The demo program prints "TXT: Hello World!" to `cout`.

### TxtDemo01_Input1Print
The demo program prints analog value to `cout`.
> Master TXT:
> - Input I1: Voltage or color sensor

### TxtDemo02_EncM1
[See also the project Readme](./TxtDemo02_EncM1/README.md)

The demo program shows the distance operation of the encoder motor. It is recommended that you plug a rest gear wheel 137677 to the axle and highlight a wheel. The program switches the motor for 2 rotations, then waits for a second and carries out the same number of rotations in the opposite direction. Then the program ends.
> Master TXT:
> - Output M1	Encoder motor
> - Input C1	Counter signal of the encoder motor

### TxtDemo03_Input12ExtM12
[See also the project Readme](./TxtDemo03_Input12ExtM12/README.md)

The demo program shows the initialization of the universal inputs and then requests them for 10 seconds. If the key is pressed, the M1 motor is switched on. The measured distance value of the ultrasonic sensor controls the M2 motor in the 0..100 cm area with a proportional speed. The program automatically ends after 10 seconds.

> Master TXT:
> - Input I1	key
> - Input I2	Ultrasonic sensor (if present)
> - Output M1	Light or motor
> - Output M2	Light or motor

> Extension TXT (Connect Extension only if a second TXT is present.):
> - Input I1	key
> - Input I2	Ultrasonic sensor (if present)
> - Output M1	Light or motor
> - Output M2	Light or motor

### TxtDemo04_DbcCallback_I2C
[See also the project Readme](./TxtDemo04_DbcCallback_I2C/README.md)

This example shows the data output at the I2C bus.
The I2C unit must first be initialized, and the I2C function can then be used to write the desired number of bytes and then read in the response.

> Master TXT:
> - I1: Switch
> - I2C: PCF8574 with LED's on the Outputs

### TxtDemo05_DbcCallbackInput1M1
[See also the project Readme](./TxtDemo05_DbcCallbackInput1M1/README.md)

The demo program shows the use of CallBack routine. As long as this function is set up, it is called up during the data exchange with the hardware after the inputs are read in and the output information is output. 

The CallBack routine should not need a lot of time so that the timing is not affected. During the routine, the key - in order to show it as an example - is debounced and the motor is then switched depending on the input.

The program ends after the key is pressed 10 times at the I1 input.

> Master TXT:
> - Input I1	key
> - Output M1	Light or motor

### TxtDemo06_O1_Blink
[See also the project Readme](./TxtDemo06_O1_Blink/README.md)

### TxtDemo07_Sound
[See also the project Readme](./TxtDemo07_Sound/README.md)

###TxtDemo08_MoveRef
[See also the project Readme](./TxtDemo08_MoveRef/README.md)

### TxtDemo99_BNO055
[See also the project Readme](./TxtDemo99_BNO055/README.md)

## Setting up my developers tools  Installation
See []( )

<!---
### Eclipse IDE
Download and install:
- [Java JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
- [Eclipse CDT](http://www.eclipse.org/downloads/packages/release/photon/r/eclipse-ide-cc-developers)

### TXT Tool Chain (TXT firmware >= 4.4.3)
Download:
- [Linaro 2017.11](https://releases.linaro.org/components/toolchain/binaries/7.2-2017.11/arm-linux-gnueabihf/gcc-linaro-7.2.1-2017.11-i686-mingw32_arm-linux-gnueabihf.tar.xz)

## Setting up Eclipse IDE
1. Clone demo examples from GIT repository to a workspace folder.
2. Start Eclipse CDT and import the examples to your workspace
![eclipse_import1](docs/eclipse_import1.PNG)
![eclipse_import2](docs/eclipse_import2.PNG)
3. Change 'Current builder' to 'CDT Internal Builder' in Release and Debug configuration
![eclipse_toolchain](docs/eclipse_toolchain.PNG)
4. Change 'Prefix' and 'Path' to the tool chain location
![eclipse_tool_settings](docs/eclipse_tool_settings.PNG)
5. Change project properties in 'Paths and Symbols'
![eclipse_pathsandsymbols_includes](docs/eclipse_pathsandsymbols_includes.PNG)
![eclipse_pathsandsymbols_libpaths](docs/eclipse_pathsandsymbols_libpaths.PNG)
![eclipse_pathsandsymbols_libs](docs/eclipse_pathsandsymbols_libs.PNG)
-->

## How to upload programs to the TXT controller

<!---
Aanpassen aan de TXT webs erver.
Compiled programs can be downloaded to the TXT controller using [WinSCP](https://winscp.net/)

> Attention: At first activate SSH Daemon for TXT firmware >=4.4.4!

- Activate SSH Daemon on TXT controller

![ssh_daemon](docs/ssh_daemon.png)

- Login with ROBOPro user

![winscp_login](docs/winscp_login.PNG)

- Create the directory ```/opt/knobloch/DownloadFiles/```

![winscp_downloadfiles](docs/winscp_downloadfiles.PNG)

- Copy the program binary using WinSCP to the path ```/opt/knobloch/DownloadFiles/```. You can drag and drop files to the DownloadFiles directory

- Set access rights in Properties of the downloaded binary

![winscp_access](docs/winscp_access.PNG)

-->

# document history
- 2020-05-26 CvL 466.1.1 new<br/>
  Parts are copy from the original README.md