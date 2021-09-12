(Link to Google Docs Format of proposal: https://docs.google.com/document/d/1JIi5gtc9I9Y2Bn9c19PtoRT0SrTvQwbxnjPsTpIBQM8/edit?usp=sharing)

Openpilot

Hypothetical Operational Environment

The prime operational environment in which the user will expect security functionality is during any instance in which the user is in operation of a vehicle connected to the openpilot software. Specifically, the operational environment would be on highways, roads, interstates, and parking lots. During operation of the vehicle in these environments, the user must have full assurance that the software is working as intended. Failure to do so would result in vehicular collisions, run off of the road, and possible injury to the user.

Systems Engineering View

https://ibb.co/K7CL3Sc

Perceived Threats
The most widely accepted threat perceived by users is the failsafe systems. The software effectively hacks into the controls of the vehicle in order to maintain autopilot control. Then, what happens if this control is suddenly revoked or unexpectedly fails? Will the vehicle come to a stop? Will a user have to take manual control? What can be expected of the software in these circumstances. Another threat is the fact that many circumstances cannot be accounted for in a theoretical environment. The software attempts its best to address all possible scenarios, but there will be something that the software was not explicitly designed to prepare for: what then will OpenPilot do? It may have potentially dangerous consequences. Thirdly, there is a huge question about liability. The software does not intend for any accidents to occur, but some are bound to eventually happen. Who, then, is liable for this occurring? Since it is an open source software there is no single individual to attribute this to. This could lead to potential legal issues in the future. Finally, and most dangerous of them all, is the potential for this software to be used for very harmful purposes. Having an open source autopilot system is nice in theory, but all it takes is one person to slyly gain access to a user’s vehicle to cause catastrophic damage. What then does this software do to prevent this from ever happening?


Security Features

The open pilot uses panda to proxies all messages between the Lane Keeping Assist System and the rest of the car. It has a state variable “controls_allowed” that determines whether to sent or not to send the control messages on the CAN bus. An experiment was conducted to send the CAN message to a Field Programmable gate array through which they used reverse engineering and were able to decode the messages using their decoder. They read the Steering message and modify the FlexRay message and control the steering using the joystick.

Also, there is a point mentioned in the safety model “Do not use messages not designed for ADAS or outside of the stock ADAS specification”. If other CAN messages are used except the ones designed for ADAS then there could be a case where cars can take control of themselves disobeying the human's command. Humans will be powerless if the bad software takes over the steering.

Motivation

Our team’s motivation for this project spans between a variety of factors. The most important being our acquisition of openpilot-compatible Comma Two Devkit. This allows our team to perform real-world security tests on the software. Furthermore, the openpilot software is an opensource project contributing to one of the auto industries biggest evolutionary challenges; self driving cars. The abstract model in which this machine learning software has been constructed is contrasted to the current status quo within the industry. The current industry standard is constructed off the basis of the software understanding and adapting to the environment arond the vehicle during commute, while openpilot’s software looks to develop its understanding through the actions of the user operating the vehicle during commute. Contribution to this project will not only provide our team experience into one of the auto industries biggest technological challenges, but gives us an opportunity to contribute our talent to a project we all feel is impactful to the industry.  

Project Description

Openpilot is an open source project that provides driver assistance comparable to Tesla’s autopilot. Openpilot has support for over 100 different vehicles, This software can be loaded on to Comma devices which include EON Gold DevKit, comma two, and comma three. The project currently has 227 contributors and is very active. In the past month, Aug 11, 2021- september 11, 2021, It has had 177 merged pull requests and 27 open pull requests. We believe the project to be increasing in popularity since Comma has just released their latest device, comma three, and they have a very active discord server with over 2000 members. The languages used in this project are: C++, C, Python, MATLAB, Perl, and Shell. All their documentation can be found on their github repository (https://github.com/commaai/openpilot). There is also a lot of good information in their blog posts (https://blog.comma.aii)  

Contribution Agreement

The openpilot project is licensed under the MIT License which gives permission for commercial use, Modification, Distribution, and Private use. The limitations are Liability and warranty. In order to contribute to the project you will need a Github account and fork the repositories from github, They also recommend joining their discord. Your changes will also need to pass all their tests, code style/linting. Then you create pull request against the master branch, all the contributing information can be found here ( https://github.com/commaai/openpilot/blob/master/CONTRIBUTING.md). There doesn’t appear to be contributor agreements or a CODE_OF_CONDUCT md file for this project. 

Security History
There has been an experiment conducted before where it was able to override the steering messages from the open pilot software camera. Imagine you are driving straight on a bridge, and someone overrides the control, and your car flies off the bridge. If the user makes any mistakes with safety and the driver fails to control the steer physically then this could be a scenario the user can face. Even the minor modification on Electric Power Steering can result in EPS overpowering human force leading to a disaster. The sensor can glitch, fail or misbehave so if users want to make modifications then they should test for all the worst possible scenarios. 

OpenPilot public github: https://github.com/commaai/openpilot
Private github https://github.com/chadknowlton/PrivateOpenPilotRepo 

Not many issues occurred for this assignment, as most of us had an idea of what we wanted to do for this proposal, when we wanted to meet up, and even came to a fast consensus on what project we wanted to do. The only “issue” if it could be called that, is deciding who did what section for the proposal. It was quickly resolved by simply asking each person what they wanted to do and filling in the gaps of each other section depending on our individual specialities, and making the workload even amongst all of us. We didn’t plan on changing anything yet as a result of this proposal.
