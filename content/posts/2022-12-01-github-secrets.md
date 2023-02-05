---
title: "Github Actions Secrets - Conceal sensitive data with 'secret' variables"
date: 2022-12-01
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Github Secrets", "Github", "How-to guide", "December 2022"]
description: "A quick intro into Github secrets and how to use them."
thumbnail: "images/github-secrets.jpg"
image: "https://images.unsplash.com/photo-1571171637578-41bc2dd41cd2?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&1600x900"
---

## What are github secrets?

Imagine you are working on a project that demands sensitive credentials to be used in your code. In my example, I connect my Github repo to a google storage bucket. The idea is that every time I push to my repo, I want some files to be sent to the storage bucket.

In order for this to work, I need to specify sensitive credentials in my code. As I store my code in a public repository, making the information plain to see and read is clearly a bad idea. This is where Github secrets come in to save the day.

> I use Github Actions to push files into Google cloud Storage. We cover this automation in my 'GitHub Actions' blog post.

## An example

Imagine you are working on a Github action and get to the authentication section. Anyone seeing this will be able to access your service using these credentials. 

```yml
    - id: 'auth'
      name: 'Authenticate to Google Cloud'
      uses: 'google-github-actions/auth@v1'
      with:
        identity_provider: 'my_user_credentials123'
        service_account: 'my_password123'
```
To cover for this we will create a Github secret which will replace credentials with a variable name, which is only accessible to your account.

## Setting up Secrets

To set up the secret go to your repository using Github. Then click Settings > Secrets and variables > Actions.

You should be able to see a screen where all your secret credentials will be stored. This will be empty if you have not created anything yet. Proceed by clicking the green "New repository secret" button. 

You should now be prompted to enter the name for your secret, as well as the 'secret' value in a separate box. The name of your secret should follow this format:

- Secret name MUST start with a letter or an underscore.
- Secret name can include alphanumeric characters and underscores only.
- Spaces are not allowed. 

Once submitted, the secret name defaults to ALL CAPS. So a secret called 'heLLO123_' is formatted to 'HELLO123_'. This will be relevant in the following section. 

## Using the secret

Remember the example with plain text credentials. Here is the same example however, we are now using the created secrets. Imagine the 'HELLO123_' is the secret storing our identity provider credential. The 'GOOGLE_PASS' on the other hand is where we store our password. To use the secret simply use ${{ secrets.SECRET_NAME1 }}.

```yml
    - id: 'auth'
      name: 'Authenticate to Google Cloud'
      uses: 'google-github-actions/auth@v1'
      with:
        identity_provider: '${{ secrets.HELLO123_ }}'
        service_account: '${{ secrets.GOOGLE_PASS }}'
```

That is all there is to the secret ;) Hopefully this information will help you stay secure when deploying your actions.

In the meantime, happy automating!