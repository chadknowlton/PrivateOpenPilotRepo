# Designing For Software Security Engineering

## Threat Modeling
Our full reports can be viewed at:
##### https://htmlpreview.github.io/?https://github.com/chadknowlton/PrivateOpenPilotRepo/blob/main/Reports/EnviromentalReport.htm

##### https://htmlpreview.github.io/?https://github.com/chadknowlton/PrivateOpenPilotRepo/blob/main/Reports/DFD_Logging.htm

## Observations
### Enviromental DFD
When the OpenPilot software is running during a commute and experiences a fault from failure of external sensors, or from improper communications between the vehicle and OpenPilot, the software will initiate a shutdown and notify the driver with an audible chime. The shutdown process ensures that a damaged or modified external variable is dealt with properly and eleviates the risk of OpenPilot running false commands to put the driver in danger. Ultimately, the job of the driver is to remain aware of the physical enviroment, and given a failure from OpenPilot will result in control of the vehicle being given back to the driver. 

Another attack agaisnt the driver could come through the use of executable code being injected to the input recieved or sent from OpenPilot software. These attacks are mitigated through the use of the Panda Safety package. The flow of data is sanitized and checksums are made to ensure that all avenues of flow or within logic, and the automatic shutdown will be granted in the instance of an attack. 

CSRF attacks contributed to some of the DFD's 'Not Applicable' portions. In the case of the CSRF attacks, the data flow within the Enviromental processes is local and does not pertain to any web-based attacks.  

Elevation of Privilege attacks with and without the use of remote code execution are also mitigated throughout the DFD. This is due to the Panda Safety Package santizing data for code execution. The attacker would also need some form of proprietary vehicle software to begin the process of gaining elavation within the vehicle itself. 

The primary design flaw noticed within the enviromental DFD was the fact that the Panda safety package appears to be the only way for locally transferred data to be sanitized and checked for executable code. We recommend an addition of write-blockers to mitigate malicious data from reaching the sensors in the case that Panda safety package is compromised.  

### Logging and External Processes DFD

## GitHub Project Board
Link to Project Board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/3

## Teamwork Reflection
For this Data Flow Diagram (DFD) project, our team completed the quiz early so that we could spend more time focusing on the content of submission. 

Our first step tp beginning this submission was to initally meet to review our assurance cases and create level 0 DFDs to represent each case. From there, we manged to uncover that assurance cases 1 & 3 contained similiar level 0 DFD's in that they both reviewed the local and enviromental processes involved within the OpenPilot software. Cases 2, 4, and 5 all had relation in which they logging and externally facing systems used by OpenPilot. We then split into groups based off our assurance cases to begin crafting out DFDs. Our goal was to have the DFDs finished and reveiewed by professor before our Wednesday meeting. 

#### Enviromental DFD - Jack Rafter and Chad Middleton
#### Logging and External Processes DFD - Kyle Phipps, Dip Kiran Pradhan Newar, Jose Hernandez

Once we recieved feedback on our DFDs, the full team began working on the analyses of our DFDs before Wednesday meeting. Once we recieved feedback from our DFDs and rough analyses of said DFDs from the Wednesday meeting with professor, we scheduled two meetings for Thursday to finish our analyses portion. Our Enviromental DFD was completed and submitted to professor for review, but we did end up spending more time on our Logging DFD. 

Our team has continued to work through each project with sufficient contributions from team members. Although scheduling conflicts with classes and work stil play a hurdle to full attendance in team meetings. As we finish this submission and move onto the next, our biggest priority will be to ensure that all team members are able to remain in attendance during meetings. 
