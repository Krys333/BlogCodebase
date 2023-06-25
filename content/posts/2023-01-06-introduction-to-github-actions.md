---
title: "Basic introduction to GitHub Actions"
date: 2023-01-06
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["How-to guide", "GitHub", "GitHub Actions", "2023"]
description: "Learn how to deploy files onto a Google Cloud Storage bucket using GitHub Actions."
thumbnail: "images/github-actions.jpg"
image: '/images/github-actions-hero.jpg' 
---

## Outline

GitHub Actions are a powerful way of automating your tasks. Often, when you work on a project you will regularly find yourself pushing new updates and features. Naturally then, these changes need to be published in several spaces; be it a GitHub repository, a cloud storage bucket, or anywhere else your code is set to function. This action alone can double and triple your work. 
This is where GitHub actions can do all the lifting for you.

In this short blog we will break down a GitHub action for you, allowing you to set one up.

## Getting started

GitHub actions are defined in your repository under directory .github/workflows/your-github-action-name.yml

You can either create the directory yourself, or you can use the UI to get cool suggestions, and have it create the directories for you. Depending on the contents of your repository, GitHub will make best possible guess at what you may want to do.

## Dissecting a GitHub Action pushing content to a Google Cloud Storage bucket

Here we will analyse a YAML file line-by-line to get a true understanding of what our GitHub action is doing. 

```yml
name: Push Contents To Google Cloud Storage

on: push

jobs:
  deploy_site:
    runs-on: 'ubuntu-latest'
    permissions:
      contents: read
    steps:
      - name: Checkout repository
        uses: 'actions/checkout@v3'
      - id: auth
        name: Authenticate to Google Cloud
        uses: 'google-github-actions/auth@v1'
        with:
          credentials_json: '${{ secrets.GOOGLE_CREDENTIALS }}'
      - id: 'upload-folder'
        uses: 'google-github-actions/upload-cloud-storage@v1'
        with:
          path: public
          destination: krystianbucko.com
          parent: false
```

The `name` property at the start refers to the name of your GitHub action. You can name it whatever you want, hopefully something clear and meaningful for later. 

The `on` property specifies when our github action is triggered. Think of it as 'when do I really want this automation to take place'. For my project, I want any updates I make to be sent to my Google bucket as soon as possible. In GitHub Actions that's by setting the property to `push` AKA `git push`.

Property `jobs` are blocks of sequential steps. The block I have defined for my project is called `deploy_site` (the name is arbitrary).

`runs-on` defines what system GitHub will spin up to run our job.

`permissions` states the range of access our job has. When we set `contents` to `read`, we enable the action to read our repository. 

`steps` refers to the individual steps our action takes to complete the job. We have used the property `name` to make it very clear what a step does. 

`uses` reuses an external github action. We want to keep the code DRY.

`actions/checkout@v3` refers to opening repository n the system. 

```yml
- id: auth
  name: Authenticate to Google Cloud
  uses: 'google-github-actions/auth@v1'
  with:
    credentials_json: '${{ secrets.GOOGLE_CREDENTIALS }}'
```
The above step authorises our github action to access our Google bucket. In order to do this you need to set up access credentials from your cloud provider. I use a JSON file to store my credentials and feed them to my GitHub action using a GitHub secret. I have a separate [blog post on creating GitHub secrets]({{< ref "2022-12-01-github-secrets" >}}). 

```yml
- id: 'upload-folder'
  uses: 'google-github-actions/upload-cloud-storage@v1'
  with:
    path: public
    destination: krystianbucko.com
    parent: false
```
The final step above takes care of the uploading process. I upload a specific folder from my repository using the `google-github-actions/upload-cloud-storage@v1` action. The `path` property refers to the name of the folder we wish to upload. `destination` refers to the name of your bucket. Because I am uploading a website, I do not want the contents of my upload to be within a folder, which is why we set the property `parent` to `false`.

If you have set up your action to be triggered by `push`, all that s left to do is just `git push`. You can check on the status of the action by going to your repository's "Actions" section. If all is well you should see a big green tick. Conveniently, GitHub does provide you with error logs if anything does not quite go to plan. I hope this helps you with automating your tasks. 

Stay tuned for more, and in the meantime, happy automating! :) 