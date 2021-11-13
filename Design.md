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

In conclusion, the primary design flaw noticed within the enviromental DFD was the fact that the Panda safety package appears to be the only way for locally transferred data to be sanitized and checked for executable code. We recommend an addition of write-blockers to mitigate malicious data from reaching the sensors in the case that Panda safety package is compromised.  

### Logging and External Processes DFD
The OpenPilot service and data flow pathways involved with the logging services appeared to resemble clear mitigations of risk. However, one common flaw our team noticed with was the fact that a good portion of mitigations were justified by the attacks requiring physical access to the device. While we find these attacks to be very unlikely and require extensive knowledge of not only the Comma device but the vehicle itself, it serves that physical access to the device leaves questionable risk to the OpenPilot software. Though the chance of a bad actor gaining access to the everyday user is unlikely, we do recommend that the Comma device includes some form of tamper notification to the device itself. This could include some sticker covering one of the screws on the device itself. While this technique may seem trivial, it gives the driver the ability to confidently check whether or not a bad actor has tampered with the device.

The use of the Panda device and safety package running in conjunction with OpenPilot also remained as a keynote to the analysis. While the filtering and sanitization of data does allow for the remediation of most forms of hostile code execution, privilege escalation, etc., it can be seen that the failure of the Panda safety package itself leaves the OpenPilot vulnerable to attack. As with the Environmental DFD, our team recommends that some form of write-blocker is used between the connections involving the device sending data to the vehicle.

Connection between the OpenPilot software and the Comma.ai servers for uploading saved driving logs happens via cellular connection over the internet, greatly extending the range for which someone could try to connect to the device. To prevent unauthorized connections, the Comma device has a unique token associated with it which authenticates it with Comma servers in both directions. In the event that Comma.ai servers are compromised, however, the mitigation of this authentication would be negated. Safety measures are required on the end of Comma.ai servers to prevent compromises, but that is outside the scope of the OpenPilot software which is focused only on the domain of the vehicle it is implemented in.

Denial of service attacks were our last attacks in which our team noticed an active level of risk. While the Panda safety package and emergency shutdown appears to mitigate the event of device failure, it can be seen that the failure of these processes to execute leaves the driver at risk. OpenPilot requires the driver to remain attentive of the vehicle at all times and implements numerous sensors to ensure compliance with their safety model. OpenPilot does also cut data flow to the vehicle if the driver depresses either of the vehicle’s pedals, withdraws their hands from the steering wheel, or loses sight view of the driver. This then puts the driver back in control of the vehicle. However, in the highly unlikely event that the driver loses consciousness during commute, OpenPilot has no way to return the vehicle properly and safely to a safe stop. We deemed this to be out of scope but recommend some form of process to be added to mitigate this risk.


## GitHub Project Board
Link to Project Board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/3

## Teamwork Reflection
For this Data Flow Diagram (DFD) project, our team completed the quiz early so that we could spend more time focusing on the content of submission. 

Our first step tp beginning this submission was to initally meet to review our assurance cases and create level 0 DFDs to represent each case. From there, we manged to uncover that assurance cases 1 & 3 contained similiar level 0 DFD's in that they both reviewed the local and enviromental processes involved within the OpenPilot software. Cases 2, 4, and 5 all had relation in which they logging and externally facing systems used by OpenPilot. We then split into groups based off our assurance cases to begin crafting out DFDs. Our goal was to have the DFDs finished and reveiewed by professor before our Wednesday meeting. 

#### Enviromental DFD - Jack Rafter and Chad Middleton
#### Logging and External Processes DFD - Kyle Phipps, Dip Kiran Pradhan Newar, Jose Hernandez

Once we recieved feedback on our DFDs, the full team began working on the analyses of our DFDs before Wednesday meeting. Once we recieved feedback from our DFDs and rough analyses of said DFDs from the Wednesday meeting with professor, we scheduled two meetings for Thursday to finish our analyses portion. Our Enviromental DFD was completed and submitted to professor for review, but we did end up spending more time on our Logging DFD. 

Our team has continued to work through each project with sufficient contributions from team members. Although scheduling conflicts with classes and work stil play a hurdle to full attendance in team meetings. As we finish this submission and move onto the next, our biggest priority will be to ensure that all team members are able to remain in attendance during meetings. 
