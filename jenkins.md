This tutorial shows how to install an EC2 instance running Jenkins, as a requirement to run the CI/CD environment of the PokeClicker application. 

First we need to create an EC2 instance. Jenkins does not run well with only 1GB of RAM, so at least 2 ("simple" instance) is recommended. Depending on the amount of users, you might want an even bigger instance.

1. Go to your AWS panel, open EC2 and choose "Instances" from the sidebar. Choose to add a new instance.
2. Choose the Amazon Linux x64 Simple (2GB RAM) option.
3. Leave all the other settings the same and choose "Create"
4. You might want to rename this instance to "Jenkins"

Now, you need to add an exception for the Jenkins port (8080) and HTTP port (80) to the correct security group in EC2.

Next, login to your instance via ssh. Then, run the following commands sequentially to install and run Jenkins:

`sudo yum update –y`
`sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins.io/redhat/jenkins.repo`
`sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key`
`sudo service jenkins start`

As Jenkins is going to build our projects, we need some tools that aid in building this projects. To do this, we can install "git", "maven" and a group of packages for development purposes using the following commands:

`sudo yum install -y git`
`sudo yum -y groupinstall "Development Tools"`
`wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo`
`yum install apache-maven`

Now we can go to the jenkins instance by going to the ipv4 address of the server, prepended by :8080. Go through the default installation process of Jenkins, and choose to install recommended plugins. Once Jenkins is setup, please choose 
