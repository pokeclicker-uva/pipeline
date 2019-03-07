This tutorial shows how to install an EC2 instance running Jenkins, as a requirement to run the CI/CD environment of the PokeClicker application. 

First we need to create an EC2 instance. Jenkins does not run well with only 1GB of RAM, so at least 2 ("simple" instance) is recommended. Depending on the amount of users, you might want an even bigger instance.

1. Go to your AWS panel, open EC2 and choose "Instances" from the sidebar. Choose to add a new instance.
2. Choose the Amazon Linux x64 Simple (2GB RAM) option.
3. Set the following security settings:


<img src="https://github.com/pokeclicker/pipeline/raw/master/images/security_group_jenkins.png"
     alt="Security Group Jenkins"
      width="50%" style="padding-left:20px;"  />

4. Leave all the other settings the same and choose "Create"
5. You might want to rename this instance to "Jenkins"

Now, you need to add an exception for the Jenkins port (8080) and HTTP port (80) to the correct security group in EC2.

Next, login to your instance via ssh. Then, run the following commands sequentially to install and run Jenkins:

`sudo yum update –y`

`sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins.io/redhat/jenkins.repo`

`sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key`

`sudo yum install jenkins`

As Jenkins is going to build our projects, we need some tools that aid in building this projects. To do this, we can install "git", "maven" and a group of packages for development purposes using the following commands:

`sudo yum install -y git`

`sudo yum -y groupinstall "Development Tools"`

`sudo yum install -y java`

`sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo`

`sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo` 

`sudo yum install apache-maven`

Afterwards, we can start the server:

`sudo service jenkins start`

Now we can go to the jenkins instance by going to the ipv4 address of the server, prepended by :8080. However, we want Jenkins to be available at port 80. We can do this with the following command:

`iptables -t nat -A OUTPUT -o lo -p tcp --dport 80 -j REDIRECT --to-port 8080`

Now we can go to the URL of the server to open Jenkins. Do this, and go through the steps until you reach the following:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_0.png" width="50%" style="padding-left:20px;"  />

At this step, select "Select plugins to install". After you do that, you get a big categorized list of Jenkins plugins. Make sure the following boxes are checked:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_1.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_2.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_3.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_4.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_plugins_5.png" width="50%" style="padding-left:20px;"  />

You can keep the rest on the default settings. After you do this, Jenkins will be installed and build jobs can be configured. Please, now follow the tutorial "install docker for jenkins" to continue.
