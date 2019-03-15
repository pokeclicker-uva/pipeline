Now we have started Jenkins, you can go to the URL at which Jenkins is deployed. Do this, and go through the steps until you reach the following:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_0.png" width="50%" style="padding-left:20px;"  />

At this step, select "Select plugins to install". After you do that, you get a big categorized list of Jenkins plugins. Make sure the following boxes are checked:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_1.png" width="30%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_2.png" width="30%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_3.png" width="30%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_4.png" width="30%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_5.png" width="30%" style="padding-left:20px;"  />

You can keep the rest on the default settings. After you do this, Jenkins will be installed and build jobs can be configured. 

Before we configure the first job, we will show how to configure the security settings. In Jenkins, go to `Manage Jenkins` -> `Configure Global Security` -> `Authorization`. Set the authorisation settings to the following:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/security_jenkins.png" width="50%" style="padding-left:20px;"  />
