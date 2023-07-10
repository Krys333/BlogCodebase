---
title: "Explore infrastructure as code through a simple anecdote"
date: 2023-04-19
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Terraform", "IaC", "AWS", "2023"]
description: "Learn the basics of IaC from the perspective of Terraform"
thumbnail: "images/blocks-thumbnail.jpg"
image: 'https://media.jfrog.com/wp-content/uploads/2022/06/13202833/863x300-1.png' 
---

In this blogpost I will explain Infrastructure as Code (IaC) in a easy-to-digest way. I hope my explanation is so simple that you will be able to repeat it to a 10 year-old and have them grasp the premise!

Before we start however, I have a separate post on getting started with Terraform. Explaining IaC is a good stepping stone into getting your first project going. So please go give that a read next for a more practical perspective. 

## What is IaC and why should you care? 

I like to simplify concepts, so let's pretend we are explaining this to a 10-year old. Imagine we are building a structure out of wooden blocks that vary in size. No IaC approach involves grabbing up a handful of blocks and starting to arrange them right off the bat. Nothing wrong with that. You can get exactly where you need to get to. Especially with a smaller project. So you can build a perfectly fine structure without IaC. However!...

Now let's imagine you want to do some more advanced actions, for example:
- Replicate the structure a 100 times!
- Replicate the structure in a different environment.
- Add/remove large sections of your building.
- Regularly scale it up, or down, as and when you need it.
- Build stuff with a team (easily).
- Manage complexity of a very big project with ease.
- Choose whether your block set is wooden, plastic, or metal. Think using GCP, AWS, or Azure. 
- Or even tear the building down quickly without leaving anything behind!

![Building blocks](/images/blocks-thumbnail.jpg)

This is what IaC (in context of Terraform) gives us. It is a tool that enables us to efficiently manage our infrastructure. To really drive the point home I have a list of technical points that correspond to the one above. 

- **Consistency and Reproducibility.** Infrastructure deployments are predictable and consistent across different environments, reducing human error.
- **Scalability and Agility.** Automation enables easy scaling up or down of infrastructure resources and quick replication of environments.
- **Version Control and Collaboration.** Infrastructure configurations can be treated as code, enabling versioning, change tracking, and seamless collaboration among team members.

## Conclusion

Infrastructure as Code (IaC) is a critical part of the modern development process. It enables collaboration, scalability, replicability and so much more. Not to mention, it also makes for an excellent conversation piece at a party. Puns aside, IaC is a powerful tool that is essential for any aspiring data engineer to know. 

Having read around the subject, I was hard-pressed to find any significant drawbacks of the approach. The only one I am willing to give some credit is the "Learning Curve" argument. Where there exists a curve associated with mastering the tools and languages used for IaC, such as CloudFormation or the aforementioned Terraform.

Saying that we are all in business of engineering. With a sink or swim approach to learning embedded in this field, I am confident anyone reading this post is not bothered by learning. So with that positive note I will draw to a close. Remember to read up on [Get started with Terraform](/blog/2023/05/create-your-first-project-with-terraform/) for a practical view of IaC.

Happy Terraforming!
