# Code Analysis for Software Security Engineering
## Code Review Strategy
OpenPilot contains 1,886 files, and roughly half of them are python scripts. The rest of the files consist of a combination of bash and C, C++ files. While the use of an automated tool was with in the realm of possibility, our team felt it was necessary to first try and scan the bulk of code using an automated scanner. It is worth mentioning that OpenPilot is a massively popular project meaning that our chances of finding active vulnerbailities may be slim. However, we wanted to give an automated scanner a try to test the waters and get a feel for the vulnerbailities we should expect to see. Jose and Jack both have experience using SonarCloud and felt it was the best option in going forth to scan the Python code first. We first forked the OpenPilot repository, added a `build.yml` plugin to our builds, and developed a `sonar-project.properties` with some minor changes to fit our scan criteria. To be able to compile, we needed our 'sonar-project.properties' file to ignore all forms of C code to run properly. We did so be adding the lines `sonar.c.file.suffixes=-` , `sonar.cpp.file.suffixes=-`, and `sonar.objc.file.suffixes=-`. This netted us with 7 bugs and 182 vulnerabilities to manually check over. While we believe there are a number of false positives, our team is satisfied with the results returned.

In terms of scanning the C code, SonarCloud needs to compile any C code to have it scanned. Our team felt it was necessary to first find an alternative approach to scanning this code, but ultimately felt it was proper to manually review the code for mistakes. Mainly due to the fact that the scripts compiling and processing data were all with in the Python scripts. 


## Findings From Code Review
SonarCloud Scan Results: https://sonarcloud.io/summary/overall?id=Rafterman29_openpilot

### Python Scripts

### CWE-200: Exposure of Sensitive Information to an Unauthorized Actor
Link: https://cwe.mitre.org/data/definitions/200.html

Code Review Source:
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uqEafnvRiIF-DU
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uiEafnvRiIF-C4
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uiEafnvRiIF-C5


In our automated scan of python scripts through SonarCloud, one concerning result returned was the use of mapped `http` addresses. This corresponds to CWE-200: Exposure of Sensitive Information to an Unauthorized Actor. Our results suggested use to ask whether our application data transits over a network that is considered untrusted, and whether
compliance rules require the service to encrypt data in transit. Both of which we answered yes to.We recommned mapping these return functuons to `https` addresses to mitigate sensitive information being transmitted through insecure channels. 

#### athnad.py
` if r.status_code == 302 and r.headers['Location'].startswith("http://u.web2go.com"):` changed to ` if r.status_code == 302 and r.headers['Location'].startswith("https://u.web2go.com"):`

#### helpers.py
`requests.put(f'http://{host}:{port}/qlog.bz2', data='')` changed to `requests.put(f'https://{host}:{port}/qlog.bz2', data='')` and ` return func(*args, f'http://{host}:{port}', **kwargs)` to ` return func(*args, f'https://{host}:{port}', **kwargs)`





### Panda Scripts

## Summary of Key Findings



## Contributions to OpenPilot



## Project Board
Link to team project board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/4



## Teamwork Reflection
