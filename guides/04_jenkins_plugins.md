In this part of the guide, we will install and configure the required plugins for PokeClicker building.

# Installing the plugins
Go to Jenkins => Manage Jenkins => Manage Plugins => Available. Here you can search and install plugins. Install the following plugins (if they are not installed already):

- Amazon S3 Bucket Credentials Plugin
- AWS CodePipeline Plugin
- Build Timeout
- Embeddable Build Status Plugin
- GitHub Branch Source Plugin
- Gradle Plugin
- Maven Info Plugin
- Maven Release Plug-in Plug-in
- NodeJS
- Pipeline: AWS Steps
- Publish Over SSH
- S3 publisher plugin
- Unleash Maven Plugin

Choose to restart Jenkins after installation. Now you have installed all required plugins.

# Configuring the plugins
Some of the plugins we just downloaded require some more configuration for them to work. For this, we want to go to Manage Jenkins => Global Tool Configuration. In this screen, we want to set some specific settings for each tool.

### Git
This tool is probably already setup correctly. Please check that the settings for this tool are equal to the following:
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/tool_git.png" width="50%" style="padding-left:20px;"  />

### JDK
PokeClicker runs on JDK 8. Create a configuration that equals the following:
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/tool_jdk.png" width="50%" style="padding-left:20px;"  />

### Maven
PokeClicker is build with Maven 3.6.0. Create a configuration that equals the following:
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/tool_maven.png" width="50%" style="padding-left:20px;"  />

### NodeJS
PokeClicker works with NodeJS version 11.10.1. You can set the refresh timeout for npm packages to your demand, we chose `120`. We also added the packages PokeClicker uses as global packages here; this ensures they are only refreshed in the timeout specified. This is not required though. These requirements are as follows: `@types/jest@~24.0.0 @types/node@~10.12.21 @types/react@~16.8.2 @types/react-dom@~16.8.0 react@~16.8.1 react-dom@~16.8.1 react-scripts@~2.1.3 typescript@~3.3.1`.
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/tool_nodejs.png" width="50%" style="padding-left:20px;"  />

After all these steps, all plugins are configured correctly and ready to use!
