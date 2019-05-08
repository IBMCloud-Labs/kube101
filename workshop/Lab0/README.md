# Lab 0: Get the IBM Cloud Container Service

Before you begin learning, you need to install the required CLIs to create and manage your Kubernetes clusters in IBM Cloud Container Service and to deploy containerized apps to your cluster.

This lab includes the information for installing the following CLIs and plug-ins:

* IBM Cloud CLI, Version 0.5.0 or later
* IBM Cloud Container Service plug-in
* Kubernetes CLI, Version 1.10.8 or later

# Install the IBM Cloud command-line interface

1. Go to this link: https://www.katacoda.com/courses/kubernetes/playground
2. Expand to full screen by clicking on the right hand icon beside the gear icon.
![](https://paper-attachments.dropbox.com/s_D8A14BDF28207FA36C22286DD4C95973B9B2CC1251CEE085A6FB91263BC0E46C_1557185836656_Screen+Shot+2019-05-06+at+3.46.13+PM.png)

3. As a prerequisite for the IBM Cloud Container Service plug-in, install the [IBM Cloud command-line interface](https://clis.ng.bluemix.net/ui/home.html) by running in the terminal`curl -sL https://ibm.biz/idt-installer | bash`. Once installed, you can access IBM Cloud from your command-line with the prefix `bx`.

4. Log in to the IBM Cloud CLI: `ibmcloud login`.
Enter your IBM Cloud credentials when prompted.

   **Note:** If you have a federated ID, use `ibmcloud login --sso` to log in to the IBM Cloud CLI. Enter your user name, and use the provided URL in your CLI output to retrieve your one-time passcode. 

# Verify the IBM Cloud Container Service plug-in
To verify that the plug-in is installed properly, run the following command:
```ibmcloud plugin list```
The IBM Cloud Container Service plug-in is displayed in the results as `container-service`.

# Download the Kubernetes CLI

[Katacoda](https://www.katacoda.com/courses/kubernetes/playground#) has the latest version of Kubernetes CLI installed, no need to install for this tutorial.

**IMPORTANT FYI**: Note that the [Katacoda Kubernetes](https://www.katacoda.com/courses/kubernetes/playground#) playground needs to be connected to the internet at all times or you will get this message.

![](https://paper-attachments.dropbox.com/s_D8A14BDF28207FA36C22286DD4C95973B9B2CC1251CEE085A6FB91263BC0E46C_1557190439473_Screen+Shot+2019-05-06+at+5.47.35+PM.png)

If you lock your laptop, restart, sleep, or leave your laptop to use the bathroom you will have to begin from scratch and install the CLIs from the top of this lab. Try to complete Lab 0, 1, and 2 in one sitting. 

# Download the Workshop Source Code
Repo `guestbook` has the application that we'll be deploying.
While we're not going to build it we will use the deployment configuration files from that repo.
Guestbook application has two versions v1 and v2 which we will use to demonstrate some rollout
functionality later. All the configuration files we use are under the directory guestbook/v1.

**Gitbash download for Windows OS if Katacoda isn't working**: https://git-scm.com/download/win 


