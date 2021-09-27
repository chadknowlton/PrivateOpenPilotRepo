# Requirements for Software Security Engineering
## Part 1: Misuse Case Assessment

### Use Case diagram pertaining to cereal internal logging 
![Cereal Use Case Diagram](https://user-images.githubusercontent.com/47230603/134964521-2ddb7db3-01d0-4d9f-aa0a-c110cfff33fe.png)
  
For this use diagram, we explore how a hacker would gain access to the internal cereal logs on the device. The Cereal logs contain all sorts of information but the diagram focuses more on GPS data because it could be used to learn more about the user of the comma 2 device and CAN data since it could be used to learn more about the inner workings of OpenPilot and could be used to learn more about how the device works and cause more malicious actions. 

The easiest way for a hacker to do this would be to gain physical access to the device; from there the hacker would just need to access the storage and find the logs. In order to mitigate this the comma 2 would have to encrypt its storage device to deter the hacker from prying further. 

the hacker could try to get the device to connect to a rogue access point that he controls in order to try and gain access to the logs remotely. The comma 2 device does not connect to unknown networks which helps prevent this from happening.

If the hacker is successful at getting the device to connect to his network or is on the same network as the device he could attempt to gain access to these logs by connecting to the comma 2 device via SSH, SSH can be disabled on the device which would prevent this from happening. However, if SSH is enabled the comma 2 uses SSH keys in order to validate who is connecting to it to prevent a hacker from connecting. If the SSH key becomes compromised, a limit of login failures can be implemented to ban the IP connecting to it, fail2ban.

### Use Case diagram on Steering/Braking (Addresses Vehicle Actuators) 
![Openpilot Misuse Case Diagram](https://user-images.githubusercontent.com/61159481/134963214-60c4d31a-d131-44d8-992f-9fc8f44667ff.png)

For the steering/braking use diagram, we explore the misuse case where a malicious hijacker is attempting to take control of the vehicle away from the openpilot software. To start off, the hijacker will need to be able access the connection between the openpilot software and the vehicle CAN network where actuators are controlled. Since the openpilot software only uses Wi-Fi to connect to the car, this helps to limit the range from which someone could attempt to connect. Unfortunately, this doesn’t help to prevent someone who is driving nearby and remaining within range. Therefore, another layer of protection via SSH IP filtering is implemented to make it harder for an unauthorized user to determine what the SSH key of the device running the openpilot software is.

Should the hijacker manage to get a working connection, however, there should be preemptive counters within the openpilot software to mitigate any further misuses. Due to the nature of openpilot being a critical system, having an environment which allows for code execution is not acceptable. As a result, much of the development effort has been put towards preventing this altogether rather than trying to sandbox everything. Even if a hijacker was able to execute code giving them remote control of the vehicle, the openpilot software has been developed to always allow for the driver to retake control immediately. The software also cannot alter the vehicle trajectory in a way which would be too quick for the driver to react safely in these cases.

### Use Case diagram on Car location and surroundings (Addresses GPS Satellite) 
![gpstracker](https://user-images.githubusercontent.com/25081252/134749470-7d142168-61f0-4c5f-ab68-7c00cd9c3e86.png)

OpenPilot uses a camera and GPS satellite to detect car location and its surroundings. We explore that hackers can decode the coordinate information and locate the driver's current location. This use-case starts with Comma 2 device, and the device has a camera and GPS tracker to detect the car's current location. The camera detects the surrounding objects and a GPS tracker to find the current point of the driver and helps the driver drive safely. 

The hacker will start the misuse if they can decode the current location of the driver. The hacker tries to connect to the local network of OpenPilot. The hacker can run a location decoder and try to connect to the local network of open pilots. We can use a hash function like SHA-256 to decode the current location of the driver. It will make it harder for the hacker to extract the information. The other feature that will be is detecting multiple users by the comma software. It will prevent malicious users from trying to connect to a local network and alert the users.
 
 The driver also can check other users in the network. It will also prevent malicious users get inside the network.


### Use Case diagram on Wifi update of software (Installer/Updater Bash Scripts) 
![InstallerBashUpdater_UseCase drawio (4)](https://user-images.githubusercontent.com/57100645/134732947-d177e379-c2af-4acc-b3b2-20819da68413.png)

In the event the comma two device loses the ability to maintain active awareness and connection for updates, we explore the misuse case where am electrical failure inhibits a vehicle stall. This use case starts with the comma two device. The device has the ability to scan for road hazards, monitor vehicle positioning, and has the ability to automatically shut off. The misuse case begins with an electrical failure that results in a vehicular stall. The stall threatens the devices abilities to monitor surroundings. However, the comma two device will detect this stall and automatically disable itself to prevent any conflicts with the vehicles built in emergency systems. The automatic shutoff will also maintain the cache and memory. This will prevent device corruption in the event that stall occurs during an update.

The driver is the secondary actor in this scenario and has the ability to monitor the surroundings and assume control of the vehicle when a vehicular stall occurs. In this event the driver detects a stall has occurred and can resume monitoring surrounding and maintain control of the vehicle.

### Use Case diagram on External Environment Hazards (Self-Drive Safety Tests) 
![Malicious Driver drawio](https://user-images.githubusercontent.com/46686977/134965031-3d3cbb68-8e34-4c11-9355-9331e6a32ffd.png)
For the Self-Drive Safety Tests diagram, we explore the misuse case where one or more hazards on/near the roadway introduce potentially dangerous situations that hinder usage of the openpilot software. Since the software relies primarily on its usage of sensors for both the outside of the car (the roadway) and the inside of the car (the driver) we considered two situations that could cause issues for the software.

Should the environment interfere with one or more sensor (e.g. a leaf covering a sensor, an insect, etc.), it would threaten the sensor's ability to detect driver attentiveness or road lanes since the sensors are getting blocked visually or otherwise. To combat this, however, there are other types of sensors with the same purpose (i.e. an alerting system that notifies the driver that something is wrong and that they need to confirm presence). However, should all of these sensors malfunction there is still a failsafe in place which automatically shuts off the openpilot software (thus giving manual control back to the driver) should enough functionality malfunctions. When this control is given back to the operator of the vehicle the software will notify the user of the shifting of control so that even if all sensors monitoring driver attentiveness are malfunctioning, the driver will still be notified of this shift before it occurs. 

Meanwhile, should potentially dangerous roadway hazards appear (deer in road, thunderstorm, etc.), it threatens openpilot's ability to operate the vehicle safely. Therefore, the sensors that monitor driver attentiveness are present to ensure that, if a hazard does appear, the operator of the vehicle can manually regain control to better deal with the situation. Overall, external environmental factors threaten openpilot's ability to operate the vehicle safely, but if this occurs the software has many different sensors to mitigate the issues this may cause. Finally, if enough sensors are threatened and the environment is causing too many issues, it always has the ability to automatically re-give control back to the user (or the user can manually take back control) so that these situations can be dealt with better. The software is far from being perfectly secure from external factors, but it does the best it can by releasing control back to the user in a timely manner should something bad occur.

## Part 2: OSS Project Documentation Review

### Security-Related configuration and installation issues

Openpilot software is a powerful tool that has many failsafes in place in order to prevent sudden failure of systems. For example, there are driver awareness sensors to ensure that the driver is actively paying attention and ready to regain control at all times, there is a fast and easy way to retake control over the vehicle, and there is an automatic shut-down feature for the self-driving software in case the sensors fail, or a major component of the software is performing unexpectedly. Below is a diagram illustrating all of the fail-safe features:
![image](https://user-images.githubusercontent.com/46686977/134415266-ddd14e74-1453-421f-a65e-b932e4c6364c.png)

A major issue involving the security of this software is that it is operating "under good faith." Therefore, there are very few (if any) features dedicated to preventing malicious use of the software. If the software is hacked into or otherwise tampered with there is not much stopping the user since the software is made "under good faith." 

However, the software does do a fantastic job of quickly and safely controlling the vehicle and ensuring that the vehicle can safely pass control back to the operator of the vehicle. According to their website located at: https://comma-ai.medium.com/understanding-the-openpilot-safety-model-fe9797e306bf their safety model is based on three principles:

1. Driver must be actively paying attention
2. Driver must be capable of immediately retaking control
3. Vehicle must not alter too quickly for the driver to safely react

### OSS Project Documentation Related to Security and Installation Issues
  1. [Software Vehicle Recognition Issue](https://github.com/commaai/openpilot/issues/22356)  
A recent Openpilot user unocvered an issue related to the software not properly identifying a dmamaged Kia Soul in front of them. The occurance was documented three different times, and further infomration pertaining to the Kia Soul indicates that the vehicle did have some rear-end damage. The user expeirenced these occurences around dawn and describes the need for the driver to intervene or else the Openpilot software would have allowed the vehicle to accelerate through the car is if it was not there. The driver utilizing the OpenPilot software was driving a 2020 Toyota Corolla and the issue appears to be either related to the software's ability to decipher darker colored vehicles in low lit areas, or the inability to properly calculate a moving vehicle if it has sustained damaged. 

  2. [Steering Fault Issue](https://github.com/commaai/openpilot/issues/21557)  
Currently, the Panda device which facilitates communication between the OpenPilot software and a vehicle’s controller area network has a bug which inhibits steering capability. Panda will randomly drop lane keeping assist messages, allowing for gaps in the rolling counter message stream. While many controller area networks allow for gaps in the counter, some do not tolerate it such as those in GM cars. As a result, “Steering Temporarily Unavailable” and “Cruise Fault” errors may appear and prevent OpenPilot from continuing to engage with the vehicle. Correcting these errors involves restarting both the OpenPilot software device and the vehicle.

  3. [Communication Issue](https://github.com/commaai/openpilot/issues/22340)  
A user of openpilot has reported an issue stating that when he attempts to use his comma 3 device displays an “openpilot unavailable” message. The user also states that the vehicle he is attempting to use the device on is a 2017 Honda Pilot verified all the hardware was installed correctly; an important thing to note however is that only the Honda Pilot with the built-in camera is fully supported by OpenPilot out of the box. Another thing of note is that the comma 3 was just released in august. What the user is experiencing could be due to his vehicle not being supported or OpenPilot still having issues with the newly released hardware.

  4. [Braking Issue](https://github.com/commaai/openpilot/issues/2624)  

  5. [Vehicle Speed Issue](https://github.com/commaai/openpilot/issues/19801)  

### Team Reflection 



Contributions:\
**Chad** - Initial part 2 security configuration summary, Use Case Diagram on malicious drivers/hijackers\
**Dip** - Use case diagram on Car location and surroundings, Overall Use/Misuse case discussion\
**Jack** - Use case diagram on Wifi update of software, Organization of assignments/meetings\
**Jose** - Use case diagram pertaining to cereal internal logging, Review & Research for diagrams\
**Kyle** - Use case diagram on steering/braking, Overall Use/Misuse case discussion

