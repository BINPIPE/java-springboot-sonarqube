# java-springboot-sonarqube
Sample Java Springboot Project to Demonstrate Declarative CI/CD Pipeline in Jenkins with SonarQube Quality Gates. 
++ Adding Slack Alerts to CI/CD declarative pipeline has also been included. Refer ++ below.


`Learning Resources for DevOps, SRE, Cloud & Engineering Management`

[![BINPIPE](https://img.shields.io/badge/BINPIPE-YouTube-red)](https://www.youtube.com/channel/UCPTgt4Wo0MAnuzNEEZlk90A)
[![Learn DevOps!](https://img.shields.io/badge/BINPIPE-Learn--DevOps-orange)](https://github.com/BINPIPE/resources/blob/master/devops-lesson-plans.md)
[![BINPIPE](https://img.shields.io/badge/Live--Classroom-blue)](https://forms.gle/tDJxDyj2nJyfsgsk7)
---

**Prerequisites**
```
-Install the below in Jenkins Server:
sudo apt install default-jdk
sudo apt install maven

-Run Sonarqube as Docker Container:
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

//Default credentials for SonarQube dashboard- admin/admin
```

**Configuring SonarQube Integration & Analysis to CI/CD Pipeline**

Follow the video for configuring the declarative pipeline with SonarQube Integration & Analysis.


++ **Slack Alerts in CI/CD Pipeline**

The following snippet enables the slack-alerts stage in the CI/CD pipeline. Watch the video to see the configurations and the `Jenkins-Slack` Integration Process.

```

```


<pre>
<a href="https://www.binpipe.org">BINPIPE</a> aims to simplify learning for those who are looking to make a foothold in the industry.
Write to me at <b>nixgurus@gmail.com</b> if you are looking for tailor-made training sessions.
For self-study resources look around in this repository, <a href="https://www.binpipe.org/">the Binpipe Blog</a> and <a href="https://www.youtube.com/channel/UCPTgt4Wo0MAnuzNEEZlk90A">Youtube Channel</a>.
</pre>

___
:ledger: Maintainer: **[Prasanjit Singh](https://www.linkedin.com/in/prasanjit-singh)** | **www.binpipe.org**
___

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

