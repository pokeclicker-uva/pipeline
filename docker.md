This tutorial shows how to install an EC2 instance running Docker, as a requirement to run the CI/CD environment of the PokeClicker application. Installing this Docker environment is very easy, and only consists of running some simple commands in an EC2 instance. 

First of all, we want to create the EC2 instance. Depending on the amount of users, you might want a bigger instance. Overall, "micro" should be fine to run a test environment, so for this tutorial we'll create a "micro" instance. This can be done with the following steps:

1. Go to your AWS panel, open EC2 and choose "Instances" from the sidebar. Choose to add a new instance.
2. Choose the Amazon Linux x64 Micro (1GB RAM) option.
3. Leave all the other settings the same and choose "Create"
4. You might want to rename this instance to "Docker"

Login to your instance via ssh. Then, run the following commands sequentially to install and run Docker:

`sudo yum update -y`
 
`sudo yum install -y docker`
 
`sudo service docker start`

Next, create a user with which we will access the server via Jenkins to run docker-related commands:

`useradd dockeradmin`
 
`passwd dockeradmin`

Give this user the right permissions:

`usermod -aG docker dockeradmin`
 
`sudo mkdir /opt/docker`
 
`sudo chown -R dockeradmin:dockeradmin /opt/docker`

Finally, we want to enable remote access for this user. By default, remote access with username password combinations is disabled on EC2 instances. We can enable this by editing a ssh config file:

`sudo nano /etc/ssh/sshd_config`

Scroll down till you see a line with the following contents:

`PasswordAuthentication no`

And replace it with:

`PasswordAuthentication yes`

Next, do the following to exit and save the file:

1. CTRL+X
2. Type "y"
3. ENTER

Next, we need to restart sshd for our configuration changes to take effect:

`sudo service sshd restart`

Now the Docker server has been setup correctly,a and we can continue by setting up the Jenkins server.
