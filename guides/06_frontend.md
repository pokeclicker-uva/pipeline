In this guide, we will show you how to setup the PokeClicker frontend application for automated building and deployment in Jenkins. We deploy the static pages of the frontend in an AWS S3 Bucket. 

This guide consists of two parts:
1. Setup the AWS S3 Bucket
2. Create the Jenkins build job

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

<img src="https://github.com/pokeclicker/pipeline/raw/master/images/static_website_hosting.png" width="50%" style="padding-left:20px;"  />

# 2. Create the Jenkins build job
