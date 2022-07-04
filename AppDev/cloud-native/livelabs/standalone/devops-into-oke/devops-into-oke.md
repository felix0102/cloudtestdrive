![](../../../images/customer.logo2.png)

# Using the OCI DevOps service to update and re-deploy an example microservice into the Oracle Kubernetes Environment.

**Lab conventions**

We have used a few layout tricks to make the reading of this tutorial more intuitive : 

- If you see a "Bullet" sign, usually associated with numbered steps this means **you** need to perform some sort of **action**.  This can be 
  - Opening a window and navigating to some point in a file system
  - Executing some command on the command line of a terminal window :
    -  For example : `ls -al`

As we cover quite some theoretical concepts, we included pretty verbose explanations.  To make the lab easier to grasp, we placed the longer parts in *Collapsibles*:

<details><summary><b>Click this title to expand!</b></summary>


If you feel you are already pretty familiar with a specific concept, you can just skip it, or read quickly through the text, then re-collapse the text section by re-clicking on the title. 

---

</details>

## Prerequisites

These labs can be run in many different ways, but in all cases you will need access to a Oracle Cloud Tenancy and be signed in to it.

Please look at the instructions in the **Oracle Cloud Free Tier** section for details of how to sign up for a free trial tenancy and how to log into it. If you already have access to a tenancy (you may be in an instructor led lab, or have a pre-existing tenancy) then go direct to Prerequisites Step 2 which covers how to login to the tenancy.

## Lab navigation

You can navigate to the modules themselves by using the navigation list on the left. Some modules have a lot of sections, so to make navigation easier you can expand a module by clicking the '+' next to the module name in the modules list, you can shrink a module in the list by clicking the '-' by it's name. 

![](images/livelabs-expand-module.png) ![](images/livelabs-close-module.png)

You can go directly to a module or section within a module by clicking on the name in the navigation list

## Getting Help

If you are in an instructor led lab then clearly just ask your instructor, if you are working through this self guided then each module has a section at the end for getting help. 

## What's in this document ?

This document is a summary of the various modules in the lab. This document itself does not contain the lab instructions

### Getting Started

This explains how to get access to a Free trial tenancy if you need one. In many lab situations you will have already done this.

## Setup using the all-in-one script

This module shows you how to use the "all-in-one" scripts to setup the environment for your lab in one go. If you are running in a free trial, or have full admin rights to your tenancy **and** are running in your home region this is the preferred approach, just follow the instructions in this module then once completed jump directly to module **Part 1** skipping the remaining setup modules.

If however you are not in a free trial, do not have full admin rights, not in your home region, or need to modify the default choices for some reason then please use the remaining setup modules instead.

## Setup your core tenancy using scripts

This module takes you through the process of using the scripts we have provided to gather data, create compartments,and a database used by the microservices running in Kubernetes. If you have already created these in a previous lab you can skip this module

Please follow the tasks in the **Setup your core tenancy using scripts** section (click the name in the labs index)

## Setup the Kubernetes environment using scripts

This module takes you through the process of using the scripts we have provided to create a Kubernetes cluster. If you have already created this in a previous lab you can skip this module

Please follow the tasks in the **Setup your kubernetes environment using scripts** section (click the name in the labs index)

## Setup your container images using scripts

This module takes you through the process of using the scripts we have provided to build the container images you will be using in your Kubernetes cluster and to push them into the Oracle Container Image Registry (OCIR) If you have already created these in a previous lab you can skip this module

Please follow the tasks in the **Setup your container images using scripts** section (click the name in the labs index)


## Installing the initial Kubernetes services using scripts

To get the microservices we will be using running in Kubernetes there are a number of tasks, to make it easier and allow for a Dev Ops focused lab we have created a script that will automatically go through the steps in the main Kubernetes lab. If you already have the storefront and stockmanager microservices running in Kubernetes you can skip this module.

Note that if the Kubernetes cluster has not finished being created you can proceed to a subsequent module, then return to this one later (as long as you complete it before you start the deployments process it's fine)

Please follow **Installing the initial Kubernetes services using scripts** section.

## Devops setup - introduction

This section describes the steps you will need to to to prepare for using the DevOps environment.

Please read **Devops setup - introductions** section. When you've completed it click the `back` button on your browser to return to this page.

## Devops setup - setting up your vault

To store confidential or frequently changing information you don't want to hard code it into your source code systems, so Dev Ops allows you to store this in an OCI Security vault. This module shows you how to set that vault up.

Please follow the steps in **Devops setup - setting up your vault** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops setup - configuring ssh access to OCI API's

To manipulate the OCI Code repositories you will need to have an ssh based authentication token setup. This modules takes you through the processes in doing this.

Please follow the steps in **Devops setup - configuring ssh access to OCI API's** section. When you've completed them click the `back` button on your browser to return to this page.


## Devops setup - configuring security policies

Like all of the servcies within OCI the DevOps service requires a specific set of security policies, This module takes you through the steps needed to set those up.

Please follow the steps in **Devops setup - configuring security policies** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops - Creating your DevOps project

To do devops work you need a DevOps project, this module shows you how to create and configure that.

Please follow the steps in **Devops - Creating your DevOps project** section. When you've completed them click the `back` button on your browser to return to this page.


## Devops - Getting the sample code and uploading to a OCI repository

To run a build you need code to actually compile, this module shows you how to download the sample code, create your own OCI Code repository and to transfer the sample code to that.

Please follow the steps in **Devops - Getting the sample code and uploading to a OCI repository** section. When you've completed them click the `back` button on your browser to return to this page.


## Devops - Examining and updating the build_spec.yaml file

The build_spec.yaml file is the core of the build process. This module explains the various parts of the build_spec.yaml file, and then shows you how to setup some vault secrets to use within it. The you upload your version of the build_spec.yaml file to the OCI Code Repository

Please follow the steps in **Devops - Examining and updating the build_spec.yaml file** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops - Creating your DevOps build pipeline

DevOps build pipelines provide an ordered sequence of stages for running abuild and creating the results. This module shows you how to set one up and get it running.

Please follow the steps in **Devops - Creating your DevOps build pipeline** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops - Updating your build pipeline to output artifacts

Once you have build artifacts in yur build pipeline you need to pass them from the pipeline to registries and image repositories. This module shows you how to add a new stage to your build pipeline to do this transfer.

Please follow the steps in **Devops - Updating your build pipelie to output artifacts** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops - Creating the deployment pipeline

Creating artifacts form a build pipeline is good, but even better is having them automatically deployed into the target environments. This module shows you how to create a deployment pipeline to run this process.

Please follow the steps in **Devops - Creating the deployment pipeline** section. When you've completed them click the `back` button on your browser to return to this page.

## Devops - Devops - Testing the CICD process and automatic triggers

This final module of the lab shows you how to have your deployment pipeline automatically triggered from the build pipeline, and then lets you test out the process. Lastly you then look at how to have this process triggered automatically when code is pushed into your OCI Code repo.

Please follow the steps in **Devops - Testing the CICD process and automatic triggers** section. When you've completed them click the `back` button on your browser to return to this page.

## Resetting your tenancy

Should you wish (or need) to do so this module shows you how to use a script to remove the resources you created in this lab


## At the end of the tutorial

We hope you enjoy doing the labs, and that they will be useful to you. 

When you finish the modules in this lab the take the time for a cup of tea (or other beverage of your choice). While you're having that well earned break we recommend that you visit the [Oracle live labs site](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/home) for a wide range of other labs on a variety of subjects.

## Acknowledgements

* **Author** - Tim Graves, Cloud Native Solutions Architect, OCI Strategic Engagements Team, Developer Lighthouse program
* **Last Updated By** - Tim Graves, March 2022

