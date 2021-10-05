# Assurance Cases for Software Security Engineering

## Top Level Claims

### Claim 1: OpenPilot maintains vehicle safety during environmental hazards


### Claim 2


### Claim 3
![Assurancecase3](https://user-images.githubusercontent.com/57100645/136056210-a8c06b42-a773-40e3-af94-0c54c17f20b5.PNG)

### Claim 4


### Claim 5
![Phipps Assurance Case 5 WIP](https://user-images.githubusercontent.com/61159481/135945705-02f2d1e4-b131-410f-bb79-767e3349e25e.png)


## Alignment with OpenPilot
In our assurance cases, we present a number of pieces of supporting evidence. For each of these pieces, we will discuss whether it aligns with functionality provided by OpenPilot. If it does not align with OpenPilot, we will also discuss whether it might be a good candidate for inclusion in our framework with future work.

### Evidence in Claim 1


### Evidence in Claim 2


### Evidence in Claim 3
1. Device Capacitor - The comma three device features a capacitor that allows the device to maintain operation even when the vehicle loses power (less than 12 volts). The device will detect such a state and beep to notify the user. It will also allow for about five addition seconds of runtime before powering down. During this powerdown cycle, the current memory stored within the cache will stay maintained.
2. Persistent Memory Architecture -  The CPU of the comma device allows for the protection of data integrity with cache and memory protection in the event of a sudden powerdown cycle. This cycle is further assisted by capacitor in Claim 3 #1. 
3. Panda Safety Model - The safety model for OpenPilot outlines the main principles for the software to maintain compliance with safety. In the event of stall, the driver must be able to take control of the vehicle when the device shuts down.
4. Comma Connect - Cellular application that enables a bridge to the comma device. When the device is synced to the application, the application will be able to maintain device logs and data.

### Evidence in Claim 4


### Evidence in Claim 5

## Project Board
The project board for this assignment is located at https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/2

## Teamwork Reflection
The beginning of this submission has been cut and clear for our team. Each member was assigned a claim and required to provide evidence to the claim. This submission is also the first in which we utilized the openpilot community discord for questions and further information pertaining to the software.



