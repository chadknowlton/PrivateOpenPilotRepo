# Assurance Cases for Software Security Engineering

## Top Level Claims

### Claim 1: 
![EnvironmentAssuranceCase drawio](https://user-images.githubusercontent.com/46686977/136292647-dc19a9c9-02be-4392-a860-9f133fc9f3dd.png)


### Claim 2:
Openpilot minimizes the risk of remote code execution


### Claim 3
![Assurancecase3](https://user-images.githubusercontent.com/57100645/136295181-bf942290-c56a-42af-8cea-8197d0d59016.PNG)

### Claim 4
![Assurance Case](https://user-images.githubusercontent.com/25081252/136274858-dfaab8af-7d2e-4fa8-acc1-0552ac8d8bbd.png)



### Claim 5
![Phipps Assurance Case 5](https://user-images.githubusercontent.com/61159481/136259893-4b14075c-74a2-4231-bdd0-7200359b7a8f.png)




## Alignment with OpenPilot
In our assurance cases, we present a number of pieces of supporting evidence. For each of these pieces, we will discuss whether it aligns with functionality provided by OpenPilot. If it does not align with OpenPilot, we will also discuss whether it might be a good candidate for inclusion in our framework with future work.

### Evidence in Claim 1
1. Automatic Shutdown Switch - As far as I could find there is no explicit name given to this feature with the comma three device. However, several times throughout the documentation it makes reference to a switch-like object that, when circumstances beyond OpenPilot's control occur, control is automatically given back to the driver and out of the software's hands. The documentation makes this sound like a sudden, almost immediate change, but later evidence claims otherwise.
2. Driver Awareness Sensors - There are sensors within the vehicle similar to those found within Tesla Autopiloting including a camera based monitoring system and a "hands on wheel" detector. More information on this can be found on their website at: https://blog.comma.ai/understanding-the-openpilot-safety-model/. Moreover, all of these sensors work in conjunction with one another to ensure that the driver is attentive and ready to take the wheel when notified. 
3. Instrument Display Panel - This is a display panel which notifies the driver of any changes in vehicle status. This includes any control relinquishing. This display panel provides evidence that the automatic shut down isn't immediate nor unexpected. The display is meant to act as a notifier in order to give the driver ample time to react to any upcoming changes.
4 and 8. Lane Detection Sensors - These are sensors that ensure that the vehicle is on the road, on a safe path (with no upcoming hazards blocking the road), and send notifications to other parts of the software so that everything is constantly updated with the conditions of the road.
5. Integrated Lane Sensors - These are off-line lane detection sensors that are on the vehicle itself so that it can notice any on-the-road hazards that on-line sensors are not aware of.
6. Connective Sensors - These are on-line lane detection sensors that utilize GPS and other Satellite data in order to get a fast real-time indication of what the road ahead will look like.
7. Vehicle Dynamics Sensors - These sensors monitor the three major measurements of motion for the vehicle: the Yaw Rate, the Lateral Acceleration, and the Roll Rate. All of these are monitored in order to ensure that they are within safe parameters and if they are not for any reason then these sensors will notify the Automated Lane Centering Control Module to adjust acceleration or other controls of the vehicle in order to resume safe operation.

### Evidence in Claim 2


### Evidence in Claim 3
1. Device Capacitor - The comma three device features a capacitor that allows the device to maintain operation even when the vehicle loses power (less than 12 volts). The device will detect such a state and beep to notify the user. It will also allow for about five addition seconds of runtime before powering down. During this powerdown cycle, the current memory stored within the cache will stay maintained.
2. Persistent Memory Architecture -  The CPU of the comma device allows for the protection of data integrity with cache and memory protection in the event of a sudden powerdown cycle. This cycle is further assisted by capacitor in Claim 3 #1. 
3. Panda Safety Model - The safety model for OpenPilot outlines the main principles for the software to maintain compliance with safety. In the event of stall, the driver must be able to take control of the vehicle when the device shuts down.
4. Comma Connect - Cellular application that enables a bridge to the comma device. When the device is synced to the application, the application will be able to maintain device logs and data.

### Evidence in Claim 4


### Evidence in Claim 5
1. Initialization Shell File – Openpilot has a shell file which initializes the Comma device called [launch_chffrplus.sh](https://github.com/commaai/openpilot/blob/master/launch_chffrplus.sh) in its root directory. Part of its startup processes include disabling Bluetooth connection and performing a wireless LAN scan for a vehicle controller area network. Bluetooth is the only connection method which gets disabled here however, meaning that Cellular Data, Wifi, GPS, and wired connection ports are still active.
2. Driver Data Log Folder – Data logs for Openpilot get stored locally on the device running the software, [configured](https://github.com/commaai/openpilot/blob/master/selfdrive/loggerd/config.py) by default to a root folder `/data/media/0/realdata/` on the device. If the software is being emulated on a PC, it will instead be stored in a directory relative to the path home. Currently, the raw data is stored here.
3. Data Access Login Page – The Comma connect [login page](https://connect.comma.ai/) has three third party login options. These let users create accounts with Comma using existing Google, Apple, and GitHub accounts. As emphasized in Inference Rule IR1, since all three of these platforms are well known and trusted to be secure, the confidence which can be had in the credential verification of the Comma connect login is reasonable.
4. Driver Data Encryption Preprocessing – The Openpilot software does not provide any sort of pre-transfer data encryption methods within its 0.8.9 release. Since driving data is stored locally before being uploaded to the Comma servers, it may be beneficial to encrypt this information when it is stored so old data logs cannot be easily read from the Openpilot device storage.
5. Python Requests Module – The file [uploader.py](https://github.com/commaai/openpilot/blob/master/selfdrive/loggerd/uploader.py) within the `/selfdrive/loggerd/tools/` directory of the Openpilot software is responsible for uploading driving data to the Comma servers, and does so using the [Requests Module](https://docs.python-requests.org/en/latest/user/quickstart/#make-a-request) for Python. The Requests module allows for data to be sent using HTTP given a URL, the data, and any additional arguments. Requests will also verify SSL certificates for HTTPS requests passed to it, so if it can be shown that the URL used for Requests in Openpilot uses HTTPS then encryption is included in transmission. See evidence 6 for more on this.
6. Requests HTTPS Upload URL – Since the API host for Comma uses HTTPS as seen in [init.py](https://github.com/commaai/openpilot/blob/master/common/api/__init__.py) found in `/common/api/`, the data transmission is encrypted.


## Project Board
The project board for this assignment is located at https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/2

## Teamwork Reflection
The beginning of this submission has been cut and clear for our team. Each member was assigned a claim and required to provide evidence to the claim. This submission is also the first in which we utilized the openpilot community discord for questions and further information pertaining to the software.



