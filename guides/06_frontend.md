In this guide, we will show you how to setup the PokeClicker frontend application for automated building and deployment in Jenkins. We deploy the static pages of the frontend in an AWS S3 Bucket. 

This guide consists of two parts:
1. Setup the AWS S3 Bucket
2. Create the secret file that specifies the API root
3. Create the Jenkins build job

# 1. Setup the AWS S3 Bucket
Create a new bucket in a region of your choice. After the bucket has been created, go to the `Permissions` tab. In this tab, click on `Bucket Policy`. In the input field, enter the following:

```
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::simonbaars-pokeclicker/*"
        }
    ]
}
```

Please substitude `simonbaars-pokeclicker` for the name of your bucket.

Next, go to `Public access settings` and make your settings match the following:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/public_access_settings.png" width="50%" style="padding-left:20px;"  />

All we have to do now is enable Static Website Hosting. Go to `Properties` => `Static website hosting`. Set your settings to match the following:

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/static_website_hosting.png" width="25%" style="padding-left:20px;"  />

# 2. Create the secret file that specifies the API root
The frontend has to be pointed To do this, go to `Credentials` => `Stores scoped to Jenkins` => `Jenkins` => `Global credentials (unrestricted)` => `Add Credentials`. In this form, enter the following information:

Kind: `Secret text`
Scope: `Global`
Secret: `http://docker.uva-se.nl/` (Or whatever address your docker server is on, this can also be an ip. Be sure to include http://.)
ID: `docker-api-root`
Description: `Docker API web address.`

Click `OK` to save this secret file.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/secret_text.png" width="50%" style="padding-left:20px;"  />

# 3. Create the Jenkins build job
This part of the tutorial explains how to create the Jenkins job to build and deploy the frontend. Click `New Item` in Jenkins and create a project of type `Freestyle project`.

In the `General` part we want to specify the GitHub URL of the job: `https://github.com/pokeclicker/frontend`.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_1.png" width="50%" style="padding-left:20px;"  />

In the `Source Code Management` section you must again specify the GitHub repo URL (`https://github.com/pokeclicker/frontend`) and the branches that you want to build and deploy.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_2.png" width="50%" style="padding-left:20px;"  />

In the `Build Triggers` section check the `GitHub hook trigger for GITScm polling` option.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_3.png" width="20%" style="padding-left:20px;"  />

In the `Build Environment` section check the `Use secret text(s) or file(s)` option.

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_4.png" width="20%" style="padding-left:20px;"  />

In the `Bindings` section

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_5.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_6.png" width="50%" style="padding-left:20px;"  />
<img src="https://github.com/pokeclicker/pipeline/raw/master/images/frontend_7.png" width="50%" style="padding-left:20px;"  />
