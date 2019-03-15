This guide explains how to setup the build job for the backend. This guide consists of three parts:

1. Setup the Docker server
2. Specify the environment variables
3. Create the build job

# 1. Setup the Docker server
In this part we will specify the SSH server of Docker in the configuration of Jenkins. Go to `Manage Jenkins` => `Configure System` => `Publish over SSH`. Choose to add a new SSH configuration. Enter the following information for this instance:

Name: `docker_hosts`
Hostname: `docker.uva-se.nl` (Or whatever address your docker server is on, this can also be an ip. Be sure to ommit http:// and any slashes.)
Username: `dockeradmin` (Or whatever username you chose to use with the Docker server.)

Click the `Use password authentication, or use a different key` checkbox. As advanced settings, set it to the following:
Passphrase / Password: `mypassword` (The password you specified for the Docker server for the `dockeradmin` user.)
Port: `22` (SFTP: FTP over SSH. This makes sure you don't need any ftp server running on port 21.)

After you have done this, please click `Test Configuration` to check whether Jenkins can connect to your Docker server.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/jenkins_ssh_config.png" width="50%" style="padding-left:20px;"  />

# 2. Specify the environment variables


# 3. Create the build job
In Jenkins, create a new project of type `Maven Project`:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_pokeclicker.png" width="50%" style="padding-left:20px;"  />

At the job configure page, for the `Maven Info Plugin Configuration` section, please only check the `Github project` item and enter the backend GitHub URL: `https://github.com/pokeclicker/backend/`.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_1.png" width="50%" style="padding-left:20px;"  />

In the `Source Code Management` section you need to click the `Git` radiobutton and enter as repository url: `https://github.com/pokeclicker/backend`. Additionally, specify all branches you want to be built amd deployed by this job.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_2.png" width="50%" style="padding-left:20px;"  />

In the `Build Triggers` section check the `Build whenever a SNAPSHOT dependency is built` and `GitHub hook trigger for GITScm polling` items.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_3.png" width="50%" style="padding-left:20px;"  />

In the `Build Environment` section check the `Use secret text(s) or file(s)` item.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_23.png" width="25%" style="padding-left:20px;"  />

In the `Bindings` section we only have to set the secrets file. Choose your environment variables file and bind it to the name `sec`.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_4.png" width="50%" style="padding-left:20px;"  />

Then, in the `Build` section, we want to set the Root POM to `pom.xml` and the Goals and options to `clean install package`.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_5.png" width="50%" style="padding-left:20px;"  />

Next, we have to specify the postbuild options. This is where we copy all files to the Docker server and run the Docker image. However, we must first copy the environment variables (from the secret file) into the workspace. To do this, add a new postbuild step of type `Execute shell`. Enter the following command: `rm -f ./.env && cp $sec ./.env`.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_71.png" width="50%" style="padding-left:20px;"  />

Now, we need to copy all files to the Docker server using SSH. To do this, add a new postbuild step of type `Send files or execute commands over SSH`. Add a single `	SSH Server` with the following settings:

Name: `docker_hosts`
Source files: `Dockerfile,target/*.jar,.env,docker-compose.yml`
Remote directory: `//opt//docker`
Exec command: `cd /opt/docker; docker-compose stop; docker-compose build --no-cache; docker-compose up -d --force-recreate`

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/backend_72.png" width="50%" style="padding-left:20px;"  />

You can further modify the build job to your likings (for instance add a email notification for each failed build). Press `Save` and the build job is ready to be used.
 	
