![](../../../common/images/customer.logo2.png)

# Setting up the core OCI environment using scripts

This module walks you through the process of setting up the core OCI features needed for all of the related labs.

Note that at some points you will need to say if you are in a `free trial tenancy`. This is referring to the 30 day free trial tenancies that Oracle offers with a few hundred US$ of resources available to you at no cost. In most cases for these labs you will be using a `free trial tenancy`, but it is also possible to run these labs where multiple people are sharing a free trial tenancy, or you are using a commercial (paid for) tenancy to run the labs (this is usually if a dedicated session is being rub for your organization). In that case you may be told to follow slightly different instructions, for example to ensure that you each use a different compartment to separate your work for each other or anything that your company may have already setup.

To speed things up for people who are just starting with this set of labs (or deleted their previously created environment) we have provided some scripts that you can use to set things up quickly, consistently and with less opportunity for mistakes.

<details><summary><b>Already done some of the labs ?</b></summary>

If you have done some of the other Helidon and Kubernetes labs connected to the one you are currently doing you will have setup the core OCI environment in those labs and perhaps retained it, as long as you have the following setup you're fine (if all of the following are missing it's easiest to just proceed with running the module below from Task 1.)

Step installed - The `$HOME/keys directory` exists and contains the `step` command and `root.crt` `root.key` files).

Note that if you have only done the Helidon VM based labs you will not have installed Step.

<details><summary><b>Step not installed ?</b></summary>

Can download step and create the certificates using the `$HOME/helidon-kubernetes/setup/common/download-step.sh` script

</details>

User information captured (initials and user identity) Entries for `USER_INITIALS` and `USER_OCID` in `$HOME/hk8sLabsSettings`

<details><summary><b>User information or initials missing ?</b></summary>

Can setup the user initials using the `$HOME/helidon-kubernetes/setup/common/initials-setup.sh` script

Can setup the user ocid using the `$HOME/helidon-kubernetes/setup/common/user-identity-setup.sh` script

</details>

Compartment created - Entry for `COMPARTMENT_OCID`  in `$HOME/hk8sLabsSettings`

<details><summary><b>Compartment info missing ?</b></summary>

Can setup the compartment (or re-use and existing one) using the `$HOME/helidon-kubernetes/setup/common/compartment-setup.sh` script

</details>

Database created - Entry for `ATPDB_OCID`  in `$HOME/hk8sLabsSettings` and `$HOME/Wallet.zip` exists

<details><summary><b>Database info missing ?</b></summary>

Can setup the database (or re-use and existing one) using the `$HOME/helidon-kubernetes/setup/common/database-setup.sh` script

</details>
---
</details>

## Task 1: Downloading the latest scripts

There are a number of scripts that we have created for this lab to make life easier, if you have previously downloaded those then you should ensure you have the latest version, if you haven't downloaded them then you will need to do so.

If you are not sure if you have downloaded the latest version then you can check

  - In the OCI Cloud shell type 
  
  - `ls $HOME/helidon-kubernetes`

If you get output like this then you need to download the scripts, follow the process in **Task 1a**

```
ls: cannot access /home/tim_graves/helidon-kubernetes: No such file or directory
```

If you get output similar to this (the file names and count may vary slightly as the lab evolves) then you have downloaded the scripts previously, but you should get the latest versions, please follow the steps in **Task 1b**

```
base-kubernetes          configurations       deploy.sh   monitoring-kubernetes  README.md     servicesClusterIP.yaml  stockmanager-deployment.yaml  undeploy.sh
cloud-native-kubernetes  create-test-data.sh  management  README                 service-mesh  setup                   storefront-deployment.yaml    zipkin-deployment.yaml
```

### Task 1a: Downloading the scripts

We will use git to download the scripts

  1. Open the OCI Cloud Shell

  2. Make sure you are in the top level directory
  
  - `cd $HOME`
  
  3. Clone the repository with all scripts from github into your OCI Cloud Shell environment
  
  - `git clone https://github.com/CloudTestDrive/helidon-kubernetes.git`
  
  ```
  Cloning into 'helidon-kubernetes'...
remote: Enumerating objects: 723, done.
remote: Counting objects: 100% (723/723), done.
remote: Compressing objects: 100% (452/452), done.
remote: Total 723 (delta 423), reused 537 (delta 249), pack-reused 0
Receiving objects: 100% (723/723), 110.23 KiB | 0 bytes/s, done.
Resolving deltas: 100% (423/423), done.
```

Note that the precise details will vary as the lab is updated over time.

Please go to **Task 2** Do not continue with anything else in task 1

### Task 1b: Updating previously downloaded scripts

We will use git to update the scripts

  1. Open the OCI Cloud shell type
  
  2. Make sure you are in the home directory
  
  - `cd $HOME/helidon-kubernetes`
  
  3. Use git to get the latest updates
  
  - `git pull`

```
remote: Enumerating objects: 21, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 14 (delta 6), reused 14 (delta 6), pack-reused 0
Unpacking objects: 100% (14/14), done.
From https://github.com/CloudTestDrive/helidon-kubernetes
   51c1ba8..f3845ad  master     -> origin/master
Updating 51c1ba8..f3845ad
Fast-forward
 setup/common/compartment-destroy.sh                 | 50 ++++++++++++++++++++++++++++++++++++++++++++++++++
 setup/common/compartment-setup.sh                   | 14 ++++++++++++++
 setup/common/database-destroy.sh                    | 38 ++++++++++++++++++++++++++++++++++++++
 setup/common/database-setup.sh                      | 15 ++++++++++++++-
 setup/common/delete-from-saved-settings.sh          | 12 ++++++++++++
 setup/common/initials-destroy.sh                    |  3 +++
 setup/common/{get-initials.sh => initials-setup.sh} |  2 +-
 setup/common/kubernetes-destroy.sh                  | 57 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 setup/common/kubernetes-setup.sh                    | 24 ++++++++++++++++++------
 setup/common/oke-terraform.tfvars                   |  2 ++
 10 files changed, 209 insertions(+), 8 deletions(-)
 create mode 100644 setup/common/compartment-destroy.sh
 create mode 100644 setup/common/database-destroy.sh
 create mode 100644 setup/common/delete-from-saved-settings.sh
 create mode 100644 setup/common/initials-destroy.sh
 rename setup/common/{get-initials.sh => initials-setup.sh} (89%)
 create mode 100644 setup/common/kubernetes-destroy.sh
```

Note that the output will vary depending on exactly what changes have been made since you first download the scripts or last updated them.

Please continue with **Task 2**

## Task 2: Downloading step certificate tools

The `step` command is used to create a root certificate, you will need this for secure connections

If you have already downloaded `step` as part of a previous lab and have setup a root certificate then you can move on to **Task 3**, do not continue with any other steps in task 2

If you do not know if you have downloaded `step` then you can check

 - In the OCI CLoud shell type
 
 - `ls $HOME/keys`

If you get output like this then you have setup both the `step` command and the root certificate, in this case go to **Task 3**, do not continue with any other steps in task 2

```
root.crt  root.key  step

```

If you get output like this then you need to download `step` and create the root certificate, follow the process in **Task 2a**, do not do any of the steps in task 2b

```
ls: cannot access /home/tim_graves/key: No such file or directory
```

If you get output like this then you have the `step` command you just need to setup the root certificate, please go to **Task 2b**, do not do any of the steps in Task 2a

```
step
```


### Task 2a: Scripted download of step and creating the root certificate

<details><summary><b>What does this script actually do ?</b></summary>  

The script goes to a web page that lists the latest version of the step distribution, from there it works out the actual download location, downloads and unpacks step

It then used step to create a self signed "root" certificate that can be used to sign certificates for the web services later on in the lab.

---

</details>

To make setting `step` up easier (manually it requires a lot of visits to different pages to get the download details) I have created a script that will do the page navigation, parsing, downloads, unpacking, and installation of `step` for you.

  1. Open the OCI cloud shell and go to the scripts directory, type
  
  - `cd $HOME/helidon-kubernetes/setup/common`
  
  2. Run the download script, In the OCI cloud shell type
  
  - `bash ./download-step.sh`
  
  ```
  /home/tim_graves/keys does not exist creating
Locating download page for latest version of step and removing whitespace
Latest version location page is https://github.com/smallstep/cli/releases/tag/v0.18.0
Identifying latest Version of step download linkk
Latest step download location is https://dl.step.sm/gh-release/cli/gh-release-header/v0.18.0/step_linux_0.18.0_amd64.tar.gz
... 
... Lots of output
...
Root certificate processing
Creating root certificate
Your certificate has been saved in root.crt.
Your private key has been saved in root.key.
```

This output is for `step` version 0.18.0 the output you get will probably vary.

This has downloaded the latest version of `step` and created the root certificate, please continue with **Task 3**


### Task 2b: Creating the root certificate

Assuming you have `step` you can easily create the self signed root certificate

  1. Open the OCI Cloud shell and type
    
  - `$HOME/keys/step certificate create root.cluster.local $HOME/keys/root.crt $HOME/keys/root.key --kty=RSA --profile root-ca --no-password --insecure`
  
  ```
  Your certificate has been saved in root.crt.
  Your private key has been saved in root.key.
```

Your root certificate is now created and you're ready to go.

Now please go to **Task 3**, do not continue with any other steps in task 2


## Task 3: Checking resources are available

<details><summary><b>What does this script actually do ?</b></summary>  

The script basically has a list of resources that are needed to do the core lab setup (some of the labs based on this core content have their own requirements checking scripts that are detailed in those labs)

In effect it tries to make sure that there are enough resources to create the compartments, databases and kuernetes cluster needed.

It also looks in the the "state" file (`$HOME/hk8sLabsSettings`) maintained by the scripts to see if a resource has already been created, if they have it skips that check.

---

</details>

This lab uses a number of compute and networking resources, this task checks to see to see if enough resources are available to run the core capabilities (some optional labs have additional requirements and may not be checked).  Generally if there is a resource limitation it's best to find out before starting a lab rather than later !

We do this check in-case lab students may be running multiple activities in their tenancies that have already consumed resources, or in the case of a free trial tenancy that has exceeded the trial limits the resources available are reduced, and these labs will not fit into the remaining "always free" capacity. In some situations (e.g. a shared tenancy with lots of people doing a lab) resource availability may change between running this script and creating the resources, but this is a good indicator. If you have already created the resources as part of another lab in this series it will try and correctly handle that.

  1. If you are not already there open the OCI cloud shall and go to the scripts directory, type
  
  - `cd $HOME/helidon-kubernetes/setup/common`
  
  2. Run the script
  
  - `bash check-minimum-resources.sh`
  
  ```
Using default context name of one
No existing settings
No existing compartment information
Checking for compartment availability
You asked for 1 of resource compartment-count in service compartments in region congratulations 999 are available
You have enough compartments available to run this lab
No existing database information
Checking for database resource availability
You asked for 1 of resource atp-ocpu-count in service database in region congratulations 8 are available
You have enough ATP database cpus available to run this lab
No already configured OKE context one, checking resource availability
Checking for VCN availability for Kubernetes workers
You asked for 1 of resource vcn-count in service vcn in region congratulations 50 are available
You have enough Virtual CLoud Networks to create the OKE cluster
Checking for E4 or E3 processor core availability for Kubernetes workers
You asked for 3 of resource standard-e4-core-count in service compute in availability domain gKLQ:ME-DUBAI-1-AD-1, congratulations 100 are available
You asked for 3 of resource standard-e3-core-ad-count in service compute in availability domain gKLQ:ME-DUBAI-1-AD-1, congratulations 100 are available
You have enough E4 shapes to create the OKE cluster
You asked for 1 of resource lb-10mbps-count in service load-balancer in region congratulations 2 are available
You have enough load balancers available to setup your core cluster services
Congratulations, you have either got an existing compartment and / or OKE cluster created from other labs, or
if not based on current resource availability (which if other people are using this tenancy
may of course change before the OKE cluster is created) there are sufficient resources to do this lab
```

  In a new free trial tenancy where you are just staring to use it the output will be **similar** to the above, and in the vast majority of cases all the resources will be available. The output is I hope fairly self explanatory, if there are resource limits that mean the lab cannot be run then they should be reported by the script, and guidance on fixing them provided. If you have previously run related labs and those resources are still in use then the output will report that and not check for unneeded additional resources.
  
  Assuming you have the available resources please proceed with Task 4.
  
## Task 4: Configuring the core environment

If you are running in a free trial tenancy allocated to you then follow the process outlined below, so please skip over the expansion.

<details><summary><b>Only read if you are not in a free trial tenancy, or are sharing a free trial with other people !</b></summary>

If you are running in a shared or commercial tenancy, or are sharing your free trial tenancy with other users then the process below will generally work, however you will want to be sure to say that you are not in a free trial tenancy when asked and follow the instructions given to perform the required processes step by step. There is more information on those individual steps [at this location](https://github.com/oracle/cloudtestdrive/blob/master/AppDev/cloud-native/scripted-setup/per-script-instructions-core-environment.md) if you chose to follow them rather than these instructions then when you have completed them skip to Task 4

---

</details>

There are a number of activities required to configure the core environment, these include identifying your self by your initials, locating your user information, setting up compartments, and creating a database. The core-environment-setup script will gather some information and then do the core work for you. You may have already done this as part of a related lab in your tenancy, if so the scripts will recognize previously created resources (provided they have not been destroyed of course) so there is no harm in re-running the scripts.

<details><summary><b>What does this script actually do ?</b></summary>  

The script is a wrapper around several other scripts that create and configure resources for us needed to do any of these code OKE based labs.

The information gathered and the OCID's of the resource created are stored in the `$HOME/hk8sLabsSettings` file for reuse by other scripts and also to identify resources that have already been created so they can be reused.

To start with it asks for your initials as these are used on multiple places for default resource names.

Next it automatically gathers information about your user, this is also saved so for example when creating a authentication token it can access your account.

After that it will create a compartment to create resources in, by default this is called CTDOKE as a sub compartment of the tenancy root, though you can override the name if you want or use an existing compartment. If you do not want to create this compartment in the tenancy root then set the value of  `COMPARTMENT_PARENT_OCID` in the `$HOME/hk8sLabsSettings` to be that of the compartment that will be the parent of your CTDOKE compartment (this is most often used in non free trial tenancies)

Next it creates an Autonomous Transaction Processing database using a admin  password it generates, it will then download the wallet file so it can be used later.

Finally it extracts connection information from the downloaded wallet file, and using that establishes a connection to the database and creates the user that will be used by the microservices , tidying up after itself.

---

</details>


  1. If you are not already there open the OCI cloud shall and go to the scripts directory, type
  
  - `cd $HOME/helidon-kubernetes/setup/common`
  
  2. Run the script
  
  - `bash ./core-environment-setup.sh`
  
  3. When asked if you are in a Free trial tenancy enter `y` if you are (if you are not sure then you probably are in a free trial tenancy, in a taught class your instructor will make it clear if you are not). If you are not then enter `n` and follow the instructions (possibly also doing this step by step, see the link in the expansion if you need more information n this)
  
  ```
  This script will run the required commands to setup your core environment
  It assumes you are working in a free trial tenancy exclusively used by yourself
  If you are not you will need to exit at the prompt and follow the lab instructions for setting up the configuration separatly
  Are you running in a free trial environment (y/n) ?
```
   
  4.  When prompted by the script enter your initials and press return, it is important that when you enter your initials you use lower case only and only the letters a-z, no numbers of special characters. In the example below as my name is Tim Graves I used `tg` as the initials. Of course unless your initials are also `tg` you would enter something different !
  
  
  ```
  Please can you enter your initials - use lower case a-z only and no spaces, for example if your name is John Smith your initials would be js. This will be used to do things like name the database
tg
OK, using tg as your initials
```
  5. The script will then locate your user information, this is automatic and doesn't require any input, you will see output similar to 
  
  ```
  Loading existing settings
No existing user info, retrieving
Checking for local user
Checking for federated user
You are a federated user, getting information
You are a federated user, your user name is oracleidentitycloudservice/tim.graves@oracle.com, saved details
```

  6. The script next creates a compartment to work in, you will be asked if you want to use the tenancy root as the parent, if you are in a free trial tenancy then enter `y` 
  
<details><summary><b>Only read if you are not in a free trial tenancy !</b></summary>

  You should chose the tenancy root unless you are in a commercial tenancy and you explicitly understand you need to work somewhere other than the tenancy root. If you really want to create or reuse a compartment somewhere other than the tenancy root enter `n` and follow the instructions that will be displayed.
  
</details>
  
  ```
  Loading existing settings
No reuse information for compartment
Parent is tenancy root
This script will create a compartment called CTDOKE for you if it doesn't exist, this will be in the Tenancy root. If a compartment with the same name already exists you can re-use change the name to create or re-use a different compartment.
If you want to use somewhere different from Tenancy root as the parent of the compartment you are about to create (or re-use) then enter n, if you want to use Tenancy root for your parent then enter y
Use the Tenancy root (y/n) ?
```

  7. You will be asked if you want to use CTDOKE as the compartment name, if you are in a free trial tenancy enter `y`
  
<details><summary><b>Only read if you are not in a free trial tenancy, or are sharing a free trial with other people !</b></summary>

Unless you are in a commercial tenancy or sharing a free trial tenancy with outer users you can use CTDOKE as the compartment name, just enter `y`. If you know you need to use a different compartment (perhaps there are multiple users in the free trial doing the lab, or a commercial tenancy admin has told you to do it elsewhere) then please enter `n` here, and follow the prompts to enter a different name.
  
If you have chosen a different compartment as the parent (by setting COMPARTMENT_PARENT_OCID in $HOME/hk8sLabsSettings that will be displayed instead of `Tennancy root`. 
  
</details>
  
  ```
  We are going to create or if it already exists reuse use a compartment called CTDOKE in Tenancy root, if you want you can change the compartment name from CTDOKE - this is not recommended and you will need to remember to use a different name in the lab.
 Do you want to use CTDOKE as the compartment name (y/n) ? 
 ```
 
  8. The script will create the compartment. 
  
  ```
  OK, going to use CTDOKE as the compartment name
Compartment CTDOKE, doesn't already exist in the Tenancy root, creating it
Created compartment CTDOKE in the Tenancy root It's OCID is ocid1.compartment.oc1..aaaaabaas5lazl434a7oizjiuife3tjffwucxrbom2zdhyhvh5t66mb75olq
It may take a short while before new compartment has propogated and the web UI reflects this
```
  
  
## Task 5: Creating the database

The microservices that form the base content of these labs use a database to store their data, so we need to create a database. The following script will create the database in the compartment we just created, then download the connection information (the "Wallet") and use that to connect to the database and create the user used by the labs.

 1. We will run a script to setup this environment

 2. If you are in a free trial tenancy you will be creating a new database so enter `y` 
  
<details><summary><b>Only read if you have an existing database to re-use</b></summary>
 
If you have an existing database in this compartment, perhaps created doing another lab which used a different database then please enter `n` and when prompted enter that name - you will need to know the ADMIN password for that database and will be prompted for it.

</details>
 
  ```
  Loading existing settings information
No reuse information for database
Operating in compartment CTDOKE
Do you want to use tgdb as the name of the database to create or re-use in CTDOKE?
```
 
 3. The script will create the database 
   
  ```
OK, going to use tgdb as the database name
Checking for database tgdb in compartment CTDOKE
Database named tgdb doesn't exist, creating it, there may be a few minutes delay
Action completed. Waiting until the resource has entered state: ('AVAILABLE',)
Database creation started
The generated database admin password is 19342873846_SeCrEt Please ensure that you save this information in case you need it later
Downloading DB Wallet file
There may be a delay of several minutes while the database completes its creation process, dont worry.
  
  ```
  
  12.   The script will then setup a temporary set of access credentials using the wallet, connect to the database using the password it generated (or in the case of a database that you are re-using the password you provided) and setup the labs user in the database.
  
  If you are reusing a database and had already setup the labs user then you may get error messages that the user conflicts with the existing one.
  
  ```
  Downloaded Wallet.zip file
Preparing temporary database connection details
Getting wallet contents for temporaty processing
Archive:  Wallet.zip
  inflating: README                  
  inflating: cwallet.sso             
  inflating: tnsnames.ora            
  inflating: truststore.jks          
  inflating: ojdbc.properties        
  inflating: sqlnet.ora              
  inflating: ewallet.p12             
  inflating: keystore.jks            
updating temporary sqlnet.ora
Connecting to database to create labs user

SQL*Plus: Release 19.0.0.0.0 - Production on Fri Nov 19 21:22:24 2021
Version 19.13.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.


Connected to:
Oracle Database 19c Enterprise Edition Release 19.0.0.0.0 - Production
Version 19.13.0.1.0


User created.


Grant succeeded.


Grant succeeded.


Grant succeeded.


Grant succeeded.

Disconnected from Oracle Database 19c Enterprise Edition Release 19.0.0.0.0 - Production
Version 19.13.0.1.0
Deleting temporary database connection info
The database admin password is 2005758405_SeCrEt Please ensure that you save this information in case you need it later
```
  
  12. **IMPORTANT** The database password is auto-generated and will not be displayed again. you are **strongly** recommended to save the generated database password (`2005758405_SeCrEt` in this case) in case you need to administer the database later. If there is an existing `$HOME/Wallet.zip` then it will be saved before downloading the new wallet.
```


## Acknowledgements

* **Author** - Tim Graves, Cloud Native Solutions Architect, OCI Strategic Engagements Team, Developer Lighthouse program
* **Last Updated By** - Tim Graves, February 2022