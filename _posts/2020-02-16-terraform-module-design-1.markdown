---
layout: post
title:  "Terraform Module Design - Part 1: Intro"
date:   2020-02-16 17:00:32 -0500
categories: blog terraform
tags: terraform iaac concepts
---
I spend a good chunk of my day not so much deploying infrastructure, but creating the structures that go around the best ways to
deploy said infrastructure. The types of people I encounter are also what i'd consider to be very smart, resourceful people but need a way to tap into the knowledge of people from the past, who have travelled the roads, built the bridges and created the post offices.

From this, comes a need to codify our learnings into a repeatable pattern. Infrastructure as Code is the big driver behind that enables me to pass on the knowledge of how my bridge got over that river, or how we were able to connect our two post offices together.

My main tool of choice over the years has been Terraform . I enjoy the heavy focus on modularity and treating these module structures as artifacts themselves. However i've been a user of both Cloudformation from AWS and ARM from Azure, which can also support similar concepts (albeit, in the CFN world its a little less 'modular' and more 'multi decoupled stack'). I may write about these as well in the future...

Over a few posts I want to go over a few of my ideas and opinions i've formed on codifying IaaC for general users at all cloud skill levels to consume. They are:

- Anatomy and the 'Rules' of a good Module
- Deploying a Module
- Consuming a Module

And maybe a few more. They are not really about writing the module or using specific technology, more just thoughts and ramblings behind the why.

But before all that...

## Part 1: What even is a "Terraform Module"?
So you may have used Terraform a little bit, and heard that everyone is using these Module things, so what do they do? The first thing to grasp is where a module lives in grand scheme of Terraform; [In a short sentence I stole from Hashicorp:](https://www.terraform.io/docs/modules/index.html)

*A module is a container for multiple resources that are used together. Modules can be used to create lightweight abstractions, so that you can describe your infrastructure in terms of its architecture, rather than directly in terms of physical objects.*

So, what does this mean for our intrepid module builders and their consumers...


If we consider a module to be a collection of these AWS Resources:
- S3 Bucket
- EC2 Instance
- EC2 Role
- Security Group

And the module's readme has stated: *This Module will spin up an EC2 Instance, allowing for SSH Access from a single IP and an S3 bucket that the Instance can Read and Write to.*


The consumer may only be asked to provide values for terraform such as:
- *What name should the S3 Bucket and EC2 instance have?*
- *What S3 Operations should the EC2 instance need to do to the bucket? Read/Write or just Read?*
- *What IP address can i SSH From?*

The module author has wrote the module in such a way that he has abstracted the complexity away, the module author has included all the security controls we would expect from the resources used to create this stack. 

Our module consumer only needs to answer the questions above to take advantage of this, and save himself from maybe accidentally spinning up a wide open S3 bucket, giving himself a shiny 'Insecure S3 Bucket of the Week' award that you see every few days in [*The Register*](https://www.theregister.co.uk/).


## Continue?
If you want to keep listening to me about this topic, i've continued my thoughts over in another post, going over the questions I ask myself as I build out these things.

[Terraform Module Design - Part 2: Writing a Module]({% post_url 2020-02-22-terraform-module-design-2 %})

