Part 1: Misuse case notion and quality

Use of proper misuse case notation (as discussed in class).
**Reasoning Quality: Misuse cases reflect reasoning that help derive security requirements --> Kyle & Dip**

Use Cases:



Use Case diagram on Alerting Distracted Driver (Self-Drive Safety Tests) --> Jose
**Use Case diagram pertaining to cereal internal logging --> Jose**
![image](https://user-images.githubusercontent.com/47230603/134416325-1b97d5dc-0662-4dd8-8b90-afb4bf065f22.png)

**Use Case diagram on Steering/Braking (Addresses Vehicle Actuators) --> Kyle:**
![Openpilot Misuse Case Diagram](https://user-images.githubusercontent.com/61159481/134416417-b0ee03ca-2880-436c-8640-f78c32f40a61.png)

**Use Case diagram on Car location and surroundings (Addresses GPS Satellite) --> Dip:**
![location](https://user-images.githubusercontent.com/25081252/134412296-243eb8c4-ed5c-41e5-98c1-89b0988839b6.png)


**Use Case diagram on Wifi update of software (Installer/Updater Bash Scripts) --> Jack:**
![InstallerBashUpdater_UseCase drawio (1)](https://user-images.githubusercontent.com/57100645/134416881-a434363f-a5cb-43ff-b408-e2d94b0fabdb.png)


**Use Case diagram on Malicious Drivers/Hijackers (Self-Drive Safety Tests) --> Chad:**
![Capture](https://user-images.githubusercontent.com/46686977/134443034-ffacac25-7c04-4989-b0a3-1c888fcaa172.JPG)


**Reflection --> Assess alignment of security requirements with advertised features. Review OSS project documentation and codebase to support your observations. --> All**

 -----------------------------------------------------------------------------------
Part 2: OSS project documentation review

**Review OSS project documentation for security-related configuration and installation issues. Summarize your observations. --> Chad**
Security-Related configuration and installation issues

Openpilot software is a powerful tool that has many failsafes in place in order to prevent sudden failure of systems. For example, there are driver awareness sensors to ensure that the driver is actively paying attention and ready to regain control at all times, there is a fast and easy way to retake control over the vehicle, and there is an automatic shut-down feature for the self-driving software in case the sensors fail, or a major component of the software is performing unexpectedly. Below is a diagram illustrating all of the fail-safe features:
![image](https://user-images.githubusercontent.com/46686977/134415266-ddd14e74-1453-421f-a65e-b932e4c6364c.png)

A major issue involving the security of this software is that it is operating "under good faith." Therefore, there are very few (if any) features dedicated to preventing malicious use of the software. If the software is hacked into or otherwise tampered with there is not much stopping the user since the software is made "under good faith." 

However, the software does do a fantastic job of quickly and safely controlling the vehicle and ensuring that the vehicle can safely pass control back to the operator of the vehicle. According to their website located at: https://comma-ai.medium.com/understanding-the-openpilot-safety-model-fe9797e306bf their safety model is based on three principles:

1. Driver must be actively paying attention
2. Driver must be capable of immediately retaking control
3. Vehicle must not alter too quickly for the driver to safely react

**Planning and Reflection --> Overall team planning and Individual Contribution  --> All**

Contributions:\
**Chad** - Initial part 2 security configuration summary, Use Case Diagram on malicious drivers/hijackers\
**Dip** - Use case diagram on Car location and surroundings, Overall Use/Misuse case discussion\
**Jack** - Use case diagram on Wifi update of software, Organization of assignments/meetings\
**Jose** - Use case diagram pertaining to cereal internal logging, Review & Research for diagrams\
**Kyle** - Use case diagram on steering/braking, Overall Use/Misuse case discussion\


