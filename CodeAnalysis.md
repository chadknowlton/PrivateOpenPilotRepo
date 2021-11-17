# Code Analysis for Software Security Engineering
## Code Review Strategy
OpenPilot contains 1,886 files, and roughly half of them are python scripts. The rest of the files consist of a combination of bash and C, C++ files. While the use of an automated tool was with in the realm of possibility, our team felt it was necessary to first try and scan the bulk of code using an automated scanner. It is worth mentioning that OpenPilot is a massively popular project meaning that our chances of finding active vulnerbailities may be slim. However, we wanted to give an automated scanner a try to test the waters and get a feel for the vulnerbailities we should expect to see. Jose and Jack both have experience using SonarCloud and felt it was the best option in going forth to scan the Python code first. We first forked the OpenPilot repository, added a 'build.yml' plugin to our builds, and developed a 'sonar-project.properties' with some minor changes to fit our scan criteria. To be able to compile, we needed our 'sonar-project.properties' file to ignore all forms of C code to run properly. We did so be adding the lines 'sonar.c.file.suffixes=-' , 'sonar.cpp.file.suffixes=-', and 'sonar.objc.file.suffixes=-'. This netted us with 7 bugs and 172 vulnerabilities to check over.


## Findings From Code Review



## Summary of Key Findings



## Contributions to OpenPilot



## Project Board
Link to team project board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/4



## Teamwork Reflection
