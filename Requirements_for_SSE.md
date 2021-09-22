Part 1: Misuse case notion and quality

Use of proper misuse case notation (as discussed in class).
**Reasoning Quality: Misuse cases reflect reasoning that help derive security requirements --> Kyle**

Use Cases:



Use Case diagram on Alerting Distracted Driver (Self-Drive Safety Tests) --> Jose
**Use Case diagram pertaining to cereal internal logging --> Jose**
![image](https://user-images.githubusercontent.com/47230603/134416325-1b97d5dc-0662-4dd8-8b90-afb4bf065f22.png)




**Use Case diagram on Steering/Braking (Addresses Vehicle Actuators) --> Kyle:**
![unknown](https://user-images.githubusercontent.com/57100645/134406242-c0b177ca-17c1-44e6-8fc7-49ec8c776d43.png)

**Use Case diagram on Car location and surroundings (Addresses GPS Satellite) --> Dip:**
![location](https://user-images.githubusercontent.com/25081252/134412296-243eb8c4-ed5c-41e5-98c1-89b0988839b6.png)


**Use Case diagram on Wifi update of software (Installer/Updater Bash Scripts) --> Jack:**
![InstallerBashUpdater_Usecase drawio](https://user-images.githubusercontent.com/57100645/134409737-4bc44f73-a636-44d8-ba64-b90549b73825.png)

**Use Case diagram on Malicious Drivers/Hijackers (Self-Drive Safety Tests) --> Chad:**
![image](https://user-images.githubusercontent.com/46686977/134414326-baad766d-6a09-48c2-a685-47ea3a3c5a15.png)


**Reflection --> Assess alignment of security requirements with advertised features. Review OSS project documentation and codebase to support your observations. --> All**

 -----------------------------------------------------------------------------------
Part 2: OSS project documentation review

Review OSS project documentation for security-related configuration and installation issues. **Summarize your observations. --> Chad**
Security-Related configuration and installation issues

Openpilot software is a powerful tool that has many failsafes in place in order to prevent sudden failure of systems. For example, there are driver awareness sensors to ensure that the driver is actively paying attention and ready to regain control at all times, there is a fast and easy way to retake control over the vehicle, and there is an automatic shut-down feature for the self-driving software in case the sensors fail, or a major component of the software is performing unexpectedly. Below is a diagram illustrating all of the fail-safe features:
![image](https://user-images.githubusercontent.com/46686977/134415266-ddd14e74-1453-421f-a65e-b932e4c6364c.png)

A major issue involving the security of this software is that it is operating "under good faith." Therefore, there are very few (if any) features dedicated to preventing malicious use of the software. If the software is hacked into or otherwise tampered with there is not much stopping the user since the software is made "under good faith." 

However, the software does do a fantastic job of quickly and safely controlling the vehicle and ensuring that the vehicle can safely pass control back to the operator of the vehicle. According to their website located at: https://comma-ai.medium.com/understanding-the-openpilot-safety-model-fe9797e306bf their safety model is based on three principles:

1. Driver must be actively paying attention
2. Driver must be capable of immediately retaking control
3. Vehicle must not alter too quickly for the driver to safely react

**Planning and Reflection --> Overall team planning and Individual Contribution  --> All**





Contributions:


