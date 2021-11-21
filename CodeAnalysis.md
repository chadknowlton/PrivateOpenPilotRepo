# Code Analysis for Software Security Engineering
## Code Review Strategy
OpenPilot contains 1,886 files, and roughly half of them are python scripts. The rest of the files consist of a combination of bash and C, C++ files. While the use of an automated tool was with in the realm of possibility, our team felt it was necessary to first try and scan the bulk of code using an automated scanner. It is worth mentioning that OpenPilot is a massively popular project meaning that our chances of finding active vulnerbailities may be slim. However, we wanted to give an automated scanner a try to test the waters and get a feel for the vulnerbailities we should expect to see. 


Jose and Jack both have experience using SonarCloud and felt it was the best option in going forth to scan the Python code first. We first forked the OpenPilot repository, added a `build.yml` plugin to our builds, and developed a `sonar-project.properties` with some minor changes to fit our scan criteria. To be able to compile the python code, we needed our 'sonar-project.properties' file to ignore all forms of C code to run properly. We did so be adding the lines `sonar.c.file.suffixes=-` , `sonar.cpp.file.suffixes=-`, and `sonar.objc.file.suffixes=-`. This netted us with 7 bugs and 182 vulnerabilities to manually check over. While we believe there are a number of false positives, our team is satisfied with the results returned, but this needed to be changed in order to run the scan and have it pickup the C code as well. 

** Jose - add paragraph reflecting how you setup SonarCloud to see C code **

In exploring how to analyze the C code of Openpilot, we had also found success using Visual Code Grepper (VCG). Since Visual Code Grepper performs a static code analysis, it didn’t require for the C files to be compiled before carrying out a scan. For this analysis tool, we downloaded the 0.8.10 release build of Openpilot and VCG version 2.2.0. Once installed, the GUI of VCG allowed us to select the target directory where the Openpilot-0.8.10 root folder was located locally on the machine, perform a full scan on it, and export the table summarizing its findings as a csv file.



## Findings From Code Review
SonarCloud Scan Results: https://sonarcloud.io/summary/overall?id=Rafterman29_openpilot

## 

### CWE-200: Exposure of Sensitive Information to an Unauthorized Actor
Link: https://cwe.mitre.org/data/definitions/200.html

Code Review Source:
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uqEafnvRiIF-DU
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uiEafnvRiIF-C4
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk5uiEafnvRiIF-C5

#### athnad.py
` if r.status_code == 302 and r.headers['Location'].startswith("http://u.web2go.com"):` 

#### helpers.py
`requests.put(f'http://{host}:{port}/qlog.bz2', data='')` and ` return func(*args, f'http://{host}:{port}', **kwargs)` 

In our automated scan of python scripts through SonarCloud, one concerning result returned was the use of mapped `http` addresses. This corresponds to CWE-200: Exposure of Sensitive Information to an Unauthorized Actor. Our results suggested use to ask whether our application data transits over a network that is considered untrusted, and whether
compliance rules require the service to encrypt data in transit. Both of which we answered yes to.We recommned mapping these return functuons to `https` addresses to mitigate sensitive information being transmitted through insecure channels. 

##

### CWE-732: Incorrect Permission Assignment for Critical Resource
Link: https://cwe.mitre.org/data/definitions/732.html

Code Review Source:
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0lk528EafnvRiIF-LK#

```
    if input(msg) == 'y':
        print("Dowloading {}".format(url))
        with urllib.request.urlopen(url) as response, open(tera_path, 'wb') as out_file:
            shutil.copyfileobj(response, out_file)
        print("Successfully downloaded t_renderer.")
        os.chmod(tera_path, 0o755)
        return tera_path
    msg_cancel = "\nYou cancelled automatic download.\n\n"
    msg_cancel += manual_install
    msg_cancel += "Once installed re-run your script.\n\n"
```
 
This CWE states that " The product specifies permissions for a security-critical resource in a way that allows that resource to be read or modified by unintended actors." This risk was identified as a possibility within the `utils.py` file located in `\pyextra\acados_template`. On line 181 chmod is used to assign file read/write/execute permissions to user groups, and secure coding practices specify that the most restrictive permissions possible should be assigned to files and directories. Assigning less restrictive permissions can lead to unintended access to critical resource files. 

We determined that this identified risk was relatively acceptable within Openpilot, given where the risk was identified and its implementation. The resource file in question is a tera renderer utility which lets anybody read and execute the file, but only allows for the owner to write to it. Since the file will be running in a context which is neither a multi-user environment nor does it contain any confidential  information, it is acceptable for everyone to read it.  

## 

### CWE-259: Use of Hard-coded Password
Link: https://cwe.mitre.org/data/definitions/259.html

Code Review Source:
* https://sonarcloud.io/project/security_hotspots?id=Rafterman29_openpilot&hotspots=AX0_TGjHgvHzTIyGNH5H

```
QString adapter;  // Path to network manager wifi-device
  QDBusConnection bus = QDBusConnection::systemBus();
  unsigned int raw_adapter_state;  // Connection status https://developer.gnome.org/NetworkManager/1.26/nm-dbus-types.html#NMDeviceState
  QString connecting_to_network;
  QString tethering_ssid;
  const QString defaultTetheringPassword = "swagswagcomma";
  ```
  
 The use of a hard-code password could lead to a high risk of authentication failure within the system. This vulnerbaility was security issue was detected within  `selfdrive/ui/qt/offroad/wifiManager.h`. OpenPilot software is risk of credential leakage since this source is used within the production enviroment. Leakage or altering of these credentials could further lead the end user to have snesitive information leaked to the API service. Removal of the hard-coded password is strongly recommended. 
 
## 

### CWE-326: Inadequate Encryption Strength
Link: https://cwe.mitre.org/data/definitions/326.html

Code Review Source:
* https://sonarcloud.io/project/issues?id=Rafterman29_openpilot&open=AX0_TGgAgvHzTIyGNH1j&resolved=false&types=VULNERABILITY

```
size_t getRemoteFileSize(const std::string &url) {
  CURL *curl = curl_easy_init();
```
```
  std::map<CURL *, MultiPartWriter> writers;
  const int part_size = content_length / parts;
  for (int i = 0; i < parts; ++i) {
    CURL *eh = curl_easy_init();
```

The automated scanner detected these code snippets within `selfdrive/ui/replay/util.cc` due to an inadequate TLS version being used. It is recommended to enforce TLS 1.2 as the minimum protocol version and disallow versions like TLS 1.0. Failure in doing so could open the door to downgrade attacks where a malicious actor who is able to intercept the connection could modify the requested protocol version and downgrade it to a less secure version.


## Summary of Key Findings



## Contributions to OpenPilot



## Project Board
Link to team project board: https://github.com/chadknowlton/PrivateOpenPilotRepo/projects/4



## Teamwork Reflection
Our first priority when it came to starting this assignmnet was finishing the weekly quiz as early as possible. This set us up for two meetings (11/18 & 11/19) where we discussed our goals, challenges expected, and **Code Review Strategy**. We eventually settled on SonarCloud due to Jose and Jack having experience with the product. The Thursday meeting also allowed us to set our individuals goals in contributions to the assignment.

**Jack Rafter & Kyle Phipps:** Setup SonarCloud to read the python scripts, and document steps into our **Code Review Strategy**. Then analyze the returned data, and add to **Findings From Code Review**. 

**Dip Kiran Pradhan Newar & Jose Hernandez:** Setup SonarCloud to read the C & C++ scripts, and document steps into our **Code Review Strategy**. Then analyze the returned data, and add to **Findings From Code Review**. 

**Chad Middleton:** Discuss the findings with the team, determine which should be put into our **Summary of Key Findings**. 

**Full Team:** Meet and discuss our **Contributions to OpenPilot** portion. 

Our final goal was to have the document setup and finalized before our meeting with professor. Our team successfully setup our SonarCloud scanner, and documented the found CWE's as of 11/21. 

As this is our final submission for the class, our team really wanted to get a head-start to give us time to breath and work through the assignmnet in close detail. Our communication strategy and approach in assigning roles has really helped us to a point in which we wished we had pursued this strategy earlier in the semester. To conclude, our communication, presence, and overall individual work has been excellent for this assignment. 
