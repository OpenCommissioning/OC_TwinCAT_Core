# Open Commissioning: TwinCAT Core Library

The TwinCAT Core Library is used in the TwinCAT PLC project and provides the behaviour models for industrial devices as function blocks.

## Project setup
+ Create PLC Project
+ Install and add the `OC_Core` library
+ Install the dependencies:
    * TcUnit
    * Tc2_Utilities
    * Tc2_Math
    * Tc3_Module
+ Declare and call `FB_System` in your main program

## Overview
In Unity project each device has a link class, which defines the interface for communication with TwinCAT.
At startup, Unity Client tries to find a TwinCAT function block for each device.
The search is done by name and type. The mapping is done when all the interface variables have found the opposite side in twincat, otherwise connection for this module becomes invalid.

![Twincat_Overview](./Documentation/Images/TwinCAT_Overview_dark.png#gh-dark-mode-only)
![Twincat_Overview](./Documentation/Images/TwinCAT_Overview_light.png#gh-light-mode-only)

## Components
### System
The main component in Open Commissioning is `FB_System`.
This function block contains the system parameters and the global system variables such as `fDeltatime`, which can be accessed by other FBs in the project through the static `GVL_Core.fbSystem`.
`FB_System` should be defined and called up once in the project so that the GVL reference is correctly assigned.
If `FB_System` is not defined or there are several instances, the TwinCAT PLC project is forced into config mode with corresponding messages in the console.

### Links
The links are the basic communication blocks in open commissioning that realise the interface for data exchange.

The basic interface consists of a `Control` _(From TwinCAT to Unity)_ and `Status` _(From Unity to TwinCAT)_ byte.
The basic link is used for additional data exchange and extended with corresponding data types. The current library contains the following links:
* `FB_LinkDevice`
* `FB_LinkDataByte`
* `FB_LinkDataWord`
* `FB_LinkDataDWord`
* `FB_LinkDataLWord`
* `FB_LinkDataReal`

### Devices
Device in Open Commissioning is a function block that represents the behaviour of the device at PLC level.
If device is inherited from an FB_Link, the corresponding interface is also prepared for Unity.
Devices also have the interface to the PLC side.
This can be as single variables or complex structures, such as control and status words in drive systems.

An example of the abstracted `FB_Drive` is shown in the following images.
![Device_Example1](./Documentation/Images/Device_Example1_dark.png#gh-dark-mode-only)
![Device_Example1](./Documentation/Images/Device_Example1_light.png#gh-light-mode-only)

#### Basic
The basic Function Blocks for the most frequently used devices are listed under Basic folder in Library.
* `FB_Button`
* `FB_Cylinder`
* `FB_SensorBinary`
* `...`

#### Drives
The Drive Folder collects the function blocks for various drives, such as simulation blocks for `DS402`, `SoE`, etc drives.

#### Others
The community-developed FBs will be added to the core library in the next incremental releases.

## Contributing
We welcome contributions from everyone and appreciate your effort to improve this project.
We have some basic rules and guidelines that make the contributing process easier for everyone involved.

### Submitting Pull Requests
1. For non-trivial changes, please open an issue first to discuss your proposed changes.
2. Fork the repo and create your feature branch.
3. Follow the code style conventions and guidelines throughout working on your contribution.
4. Create a pull request with a clear title and description.

> [!NOTE]
> All contributions will be licensed under the project's license

### Code Style Convention
Please follow [Beckhoff Programming Conventions](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/12049233675.html&id=6398798947359024199) in your code.

### Guidelines for Contributions
- **Keep changes focused:** Submit one pull request per bug fix or feature. This makes it easier to review and merge your contributions.
- **Discuss major changes:** For large or complex changes, please open an issue to discuss with maintainers before starting work.
- **Commit message format**: Use the [semantic-release](https://semantic-release.gitbook.io/semantic-release#commit-message-format) commit message format.
- **Write clear code:** Prioritize readability and maintainability.
- **Be consistent:** Follow existing coding styles and patterns in the project.
- **Include tests:** It is recommended to add or update tests to cover your changes.
- **Document your work:** Update relevant documentation, including code comments and user guides.

## Credits for third-party software components and developers:
* [TcUnit](https://github.com/tcunit/TcUnit) - TwinCAT unit testing framework
* [Beckhoff ADS](https://www.nuget.org/packages/Beckhoff.TwinCAT.Ads) - Beckhoff protocol to communicate with TwinCAT devices