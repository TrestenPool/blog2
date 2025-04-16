---
layout: post
title: Migration Yelp-Camp WebApp from Heroku to AWS Elastic Beanstalk and MongoDB
  Atlas to AWS DocumentDB
date: 2023-08-24 13:43 -0500
author: Tresten Pool
categories: [migration]
tags: [AWS, MongoDB, DocumentDB] 
image:
  path: /2023-08-24-migration-yelp-camp-webapp-from-heroku-to-aws-elastic-beanstalk-and-mongodb-atlas-to-aws-documentdb/profile.jpeg
---


# Table of contents
- [Table of contents](#table-of-contents)
- [Goal](#goal)
- [Database Migration](#database-migration)
  - [Steps](#steps)
- [App migration](#app-migration)
  - [EB CLI](#eb-cli)
    - [Installing the EB CLI using pip](#installing-the-eb-cli-using-pip)
    - [use EB to generate the configuration file](#use-eb-to-generate-the-configuration-file)
  - [How to access the logs, so helpful](#how-to-access-the-logs-so-helpful)
  - [Errors Encountered](#errors-encountered)
    - [Environment variables](#environment-variables)
    - [See the status of the Elastic Beanstalk](#see-the-status-of-the-elastic-beanstalk)
    - [Cloudformation failed multiple times trying to create my stack](#cloudformation-failed-multiple-times-trying-to-create-my-stack)
    - [Nginx 502](#nginx-502)
  - [Configuring Express app for Elastic Beanstalk](#configuring-express-app-for-elastic-beanstalk)
- [References](#references)

<!-- GOALS -->
# Goal
  - migrate a web app that was built as the main project for a web developer bootcamp udemy class to AWS.
  - The app was built with ExpressJS as the backend and bootstrap for the frontend
  - We want to migrate the following
    - Mongodb to AWS DocumentDB
    - Heroku to Elastic Beanstalk for the hosting of the webapp

<!-- DATABASE MIGRATION -->

# Database Migration

## Steps
  - backedup the db that was uploaded to mongodb atlas
  - just created a DocumentDB single instance and imported all the data there
  - DocumentDB does not have a public endpoint, meaning that you cannot connect to the db from your local computer it has to be from a vpc

<!-- END OF DATABASE MIGRATION -->





<!-- APP MIGRATION -->
# App migration


## EB CLI
  - ![eb documentation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-getting-started.html)


### Installing the EB CLI using pip 
  - `pip install awsebcli`
  - The AWS Elastic Beanstalk Command Line Interface (EB CLI) is a command line client that you can use to create, configure, and manage Elastic Beanstalk environments. For more information about the EB
  - [Installing the cli](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)

### use EB to generate the configuration file
  - `eb init --platform node.js --region us-east-2`
    - this will require an access key and secret key
      - to create these go into iam and create access keys for a user you would like to use preferrably not the root user
    - This will create a folder in the root directory named `.elasticbeanstalk`
    - This will create a file under that folder named `config.yml`
      ```yml
      branch-defaults:
        main:
          environment: YelpCamp-env
      environment-defaults:
        YelpCamp-env:
          branch: null
          repository: null
      global:
        application_name: YelpCamp
        default_ec2_keyname: YelpCamp
        default_platform: Node.js 18
        default_region: us-east-2
        include_git_submodules: true
        instance_profile: null
        platform_name: null
        platform_version: null
        profile: eb-cli
        sc: git
        workspace_type: Application
      ```

## How to access the logs, so helpful
  - explain


## Errors Encountered

### Environment variables
  - eb setenv
  - eb printenv

### See the status of the Elastic Beanstalk
  - `eb status`

### Cloudformation failed multiple times trying to create my stack
  - Errors I would get
  - ![alt-text]()

### Nginx 502
  - explain
  - created new file .ebextensions/app.config
    - ```
    option_settings:
    aws:elasticbeanstalk:application:environment:
      PORT: "8080"
    ```
      

## Configuring Express app for Elastic Beanstalk

  - couple of steps must be performed in order to get the app ready to be deployed to elastic beanstalk
    - [Deploying expressjs to aws](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_nodejs_express.html)


<!-- END OF APP MIGRATION -->

  
# References
  - {% include embed/youtube.html id='Png6NIV73qc' %}