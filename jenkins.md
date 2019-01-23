### Steps for Jenkins Patching Upgrading and Downgrading

### Console Log in

- Log in to [GCP console](https://console.cloud.google.com/home/dashboard?project=ops-staging-179618)
- Select Project **ops-staging**
- Create snapshot of disk jenkins-home  with other name .
  For Example, Jenkins-home-20190123
-  Check once snapshot of disk **jenkins-home** has created and after assuring that also check if any other disk is has skipped for taking snapshot.

### Schedule Downtime

- Take downtime for activity by doing acknowledgement on nagios tool.
* [test.preprod](https://monitoring.one.market/) host

- Search for the respective host and schedule downtime for all the services on that host
- Select  Flexible Downtime duration

###  Shutdown process for Jenkins.

- Go to Jenkins dashboard

- Select Manage Jenkins

- Click on prepare for shutdown option

**Stops executing new builds, so that the system can be eventually shut down safely.**

### Upgrading Version:

- Login to Jenkins dashboard using below URL.

* URL:  https://test.preprod.one.market/pluginManager/

- Click on “**check now**” option for available plugins updates. If it is already checked before an hour ago then no need to check

- Select all plugins and skip that plugin has warning alert.

-  Click on “**Download now and install after restart**” option 

- Console will show the status of Jenkins plugin updates

- Checking availability of latest Jenkins version.

* URL:  https://jenkins.io/changelog/

- Above URL will show latest version of Jenkins
** For example : What's new in 2.161 (2019-01-20) **

- Changing Jenkins version in YAML file.

- Go to Google Cloud Console
- Go to Workloads
- Search and Select Jenkins
- Open YAML file

- Search for below line

** “image :  Jenkins /Jenkins: 2.156”**

-  Replace version number from 2.156 to 2.161 and save the changes.

-  Monitor the status continuously and after some time check for our default URL

* URL: <https://test.preprod.one.market>

** Now After entering below url our Jenkins dashboards has opened with version 2.161 **

- Verify plugins 

* URL: https://test.preprod.one.market/pluginManager/

- After successful upgradation of Jenkins version , will check by assigning a test job to Jenkins using below steps.

- Jenkins dashboard select option jenkintetster

- Go to develop 

- Select option “Build Now” in devlop

- After some time we will get output as given below

** “Finished :  Success” **

** Now our Jenkins has upgraded to latest version of 2.161 and after testing using jenkinstester all is working fine **

### Downgrading Version 

Login to Jenkins dashboard using below URL.

* URL:  <https://test.preprod.one.market>

Login to Google Cloud management console in ops-staging environment.

- Search for below line in YAML

** image :  Jenkins /Jenkins: 2.161 **

- Replace version number from 2.161 to 2.156 

- Replace Jenkins-home-20190123 to Jenkins-home

- Save YAML file

- Check the status of container from CLI  , It will showing that container is terminating for downgrading.

- Check link status using URL, which show Error Pager for time being.
* URL https://test.preprod.one.market 

- After some time version gets downgraded and we can now check by configuring user with security parameters  For that go to below URL

* URL:  https://test.preprod.one.market/configureSecurity/

- Add user like accounts.google.com:ssharma@onemarketnetwork.com

- After successful down gradation of Jenkins version , will check the status of last completed build using below steps

- Select option jenkintetster from Jenkins dashboard 

- Go to develop 

**Check in the  build history that last successful build was few minutes ago.**
