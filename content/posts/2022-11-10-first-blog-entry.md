---
title: "Develop a website just like this - easily and quickly"
date: 2022-11-10
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["How-to guide", "HUGO framework", "2022"]
description: "Hosting your website as a static site will improve performance and improve security."
thumbnail: "images/hugo.jpg"
image: '/images/web-dev.jpg' 
---

## Outline

HUGO is an amazing tool allowing you to get a site up and running in a matter of hours (even for a beginner). The way it does this is by taking your selected theme and compiling the HTML files for you. This article will show you how to do just that. We will follow a few basic steps:

- Install HUGO
- Download a theme suited to your project
- Customize the theme
- Add your content
- Deploy the website 

Do bare in mind that this is the high-level overview of the project. Throughout, I link to plenty of useful articles to assist you in dealing with the nitty-gritty details.

## Step 1 - Install HUGO

Setup HUGO on your machine. Depending on your OS, you are best to follow the basic installation here: https://gohugo.io/installation/

Bare in mind that you will need a package manager (such as Chocolatey, or Docker) to get it on your machine.

## Step 2 (optional)

Get to grips with the base components of the framework. A great start is to get a basic theme up and running on a locally hosted server: https://gohugo.io/getting-started/quick-start/

The above guide is amazing as it sets out the steps very clearly. Once you have the basic project up and running, it will be much easier to see how the larger themes operate. I recommend step to anyone who is new to web-development.

## Step 3 - Select a theme

There are a few websites that offer themes for hugo. The honourable mentions include the official HUGO website - https://themes.gohugo.io/, as well as Jamstack Themes - https://jamstackthemes.dev/ssg/hugo/. 

You will find that most themes give you several options to set everything up. The key here is to get the theme files on your machine. Most commonly it is either a direct zip file download, or the option to clone a git repository.

Once you have your hands on the files, the bulk of the setup consists of creating a file called 'theme.toml'. Inside the file you will need to specify the name of the theme you are using. Your selected theme should have the exact content of your configuration file. 

### Be wary of the base URL line

Once you have created a toml file, chances are it similar to the example below. Make sure that you set the base URL of your project to the root URL of your website. I failed to do this properly and was pulling my hair out wondering why my hugo site was not building properly. 

Don't be me. Declare this properly. 

```toml
baseURL = "https://examplesite.com/"
languageCode = "en-us"
theme = "hugo-atlantic-theme"
```

## Step 4 - Content

This section relies heavily on the layout of your theme. Chances are, you will have a content folder in your file structure. That is where your new custom content should live. 

My recommendation is that you play around with the theme and see how far you can push the customisation to your liking. Remember that if you break something you can always just reset the folder structure. 

## Step 5 - Deploy your site

Once you feel like your project is ready to go, you will naturally be looking to show it off to the world. There are several options available to you in doing so. You can: 

- Host your website on your own domain using a bucket such as AWS S3, or Azure - https://gohugo.io/hosting-and-deployment/hugo-deploy/
- Host your project on GitHub Pages. A free alternative to web hosting - https://gohugo.io/hosting-and-deployment/hosting-on-github/

Depending on where you wish to deploy the site, you may be looking at changing your base URL declaration. 

I hope this high-level guide helps you with your project. If you do have any questions just pop over to my contact page and shoot me over an email. I am looking forward to it! 


In the meantime, happy hosting!