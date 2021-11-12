# Designing For Software Security Engineering

## Threat Modeling
Our full reports can be viewed at https://github.com/chadknowlton/PrivateOpenPilotRepo/tree/main/Reports


## Observations
### Enviromental DFD
When the OpenPilot software is running during a commute and experiences a fault from failure of external sensors, or from improper communications between the vehicle and OpenPilot, the software will initiate a shutdown and notify the driver with an audible chime. The shutdown process ensures that a damaged or modified external variable is dealt with properly and eleviates the risk of OpenPilot running false commands to put the driver in danger. Ultimately, the job of the driver is to remain aware of the physical enviroment, and given a failure from OpenPilot will result in control of the vehicle being given back to the driver. 

Another attack agaisnt the driver could come through the use of executable code being injected to the input recieved or sent from OpenPilot software. These attacks are mitigated through the use of the Panda Safety package. The flow of data is sanitized and checksums are made to ensure that all avenues of flow or within logic, and the automatic shutdown will be granted in the instance of an attack. 

CSRF attacks contributed to some of the DFD's 'Not Applicable' portions. In the case of the CSRF attacks, the data flow within the Enviromental processes is local and does not pertain to any web-based attacks.  

Elevation of Privilege attacks with and without the use of remote code execution are also mitigated throughout the DFD. This is due to the Panda Safety Package santizing data for code execution. The attacker would also need some form of proprietary vehicle software to begin the process of gaining elavation within the vehicle itself. 

### GitHub Project Board
Link to Project Board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/3



### Teamwork Reflection
