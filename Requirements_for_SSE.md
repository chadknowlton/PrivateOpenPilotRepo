# Requirements for Software Security Engineering
## Part 1: Misuse Case Assessment

### Use Case diagram on Alerting Distracted Driver (Self-Drive Safety Tests) --> Jose
### Use Case diagram pertaining to cereal internal logging --> Jose
![image](https://user-images.githubusercontent.com/47230603/134416325-1b97d5dc-0662-4dd8-8b90-afb4bf065f22.png)

### Use Case diagram on Steering/Braking (Addresses Vehicle Actuators) --> Kyle:
![Openpilot Misuse Case Diagram](https://user-images.githubusercontent.com/61159481/134554526-469adf26-1403-4455-8105-70ef1a5ff07f.png)
For the steering/braking use diagram, we explore the misuse case where a malicious hijacker is attempting to take control of the vehicle away from the openpilot software. To start off, the hijacker will need to be able access the connection between the openpilot software and the vehicle CAN network where actuators are controlled. Since the openpilot software only uses Wi-Fi to connect to the car, this helps to limit the range from which someone could attempt to connect. Unfortunately, this doesn’t help to prevent someone who is driving nearby and remaining within range. Therefore, another layer of protection via SSH IP filtering is implemented to make it harder for an unauthorized user to determine what the SSH key of the device running the openpilot software is.

Should the hijacker manage to get a working connection, however, there should be preemptive counters within the openpilot software to mitigate any further misuses. Due to the nature of openpilot being a critical system, having an environment which allows for code execution is not acceptable. As a result, much of the development effort has been put towards preventing this altogether rather than trying to sandbox everything. Even if a hijacker was able to execute code giving them remote control of the vehicle, the openpilot software has been developed to always allow for the driver to retake control immediately. The software also cannot alter the vehicle trajectory in a way which would be too quick for the driver to react safely in these cases.

### Use Case diagram on Car location and surroundings (Addresses GPS Satellite) --> Dip:
![location](https://user-images.githubusercontent.com/25081252/134412296-243eb8c4-ed5c-41e5-98c1-89b0988839b6.png)


### Use Case diagram on Wifi update of software (Installer/Updater Bash Scripts) --> Jack:
![InstallerBashUpdater_UseCase drawio (4)](https://user-images.githubusercontent.com/57100645/134732947-d177e379-c2af-4acc-b3b2-20819da68413.png)

In the event the comma two device loses the ability to maintain active awareness and connection for updates, we explore the misuse case where am electrical failure inhibits a vehicle stall. This use case starts with the comma two device. The device has the ability to scan for road hazards, monitor vehicle positioning, and has the ability to automatically shut off. The misuse case begins with an electrical failure that results in a vehicular stall. The stall threatens the devices abilities to monitor surroundings. However, the comma two device will detect this stall and automatically disable itself to prevent any conflicts with the vehicles built in emergency systems. The automatic shutoff will also maintain the cache and memory. This will prevent device corruption in the event that stall occurs during an update.

The driver is the secondary actor in this scenario and has the ability to monitor the surroundings and assume control of the vehicle when a vehicular stall occurs. In this event the driver detects a stall has occurred and can resume monitoring surrounding and maintain control of the vehicle.

### Use Case diagram on External Environment Hazards (Self-Drive Safety Tests) --> Chad:
![Malicious Driver drawio](https://user-images.githubusercontent.com/46686977/134443091-e6d81aff-c4f1-4205-bf97-a237a7dbf1e7.png)
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

### Planning and Reflection --> Overall team planning and Individual Contribution  --> All

Contributions:\
**Chad** - Initial part 2 security configuration summary, Use Case Diagram on malicious drivers/hijackers\
**Dip** - Use case diagram on Car location and surroundings, Overall Use/Misuse case discussion\
**Jack** - Use case diagram on Wifi update of software, Organization of assignments/meetings\
**Jose** - Use case diagram pertaining to cereal internal logging, Review & Research for diagrams\
**Kyle** - Use case diagram on steering/braking, Overall Use/Misuse case discussion

