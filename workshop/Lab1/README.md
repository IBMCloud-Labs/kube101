# Lab 1

## Create and gain access to your cluster

**Create your cluster**

1. Login to IBM Cloud in the browser. Click on the low hand menu where it says “Kubernetes.” 
![](https://paper-attachments.dropbox.com/s_2C1D1D8DC07187847A6AF8315AD02FE0C0F2C847FF5808E191340C8D5AD46049_1557234589287_Screen+Shot+2019-05-06+at+11.06.40+PM.png)

2. Click on “create a cluster” and select the “free” tier as shown in this screenshot. Click on the default resource group, and select the geography closest to you. 
![](https://paper-attachments.dropbox.com/s_2C1D1D8DC07187847A6AF8315AD02FE0C0F2C847FF5808E191340C8D5AD46049_1557234676787_Screen+Shot+2019-05-06+at+11.07.46+PM.png)

3. Once you instantiate your cluster, you will be taken to this page with the following commands to gain access to your specific cluster. 
![](https://paper-attachments.dropbox.com/s_2C1D1D8DC07187847A6AF8315AD02FE0C0F2C847FF5808E191340C8D5AD46049_1557235021993_Screen+Shot+2019-05-06+at+11.10.07+PM.png)


**Gain access to your cluster**

1. Log in to your IBM Cloud account.

    `ibmcloud login -a https://cloud.ibm.com`

If you have a federated ID, use `ibmcloud login --sso` to get started.

2. Target the Kubernetes Service region in which you want to work.

    `ibmcloud ks region-set <your_region>`

3. Get the command to set the environment variable and download the Kubernetes configuration files.

    ibmcloud ks cluster-config <name_of_your_cluster>

**Note**: You may need to wait and first check the status of the cluster. 
`ibmcloud ks clusters | grep -i <name_of_your_cluster>`

4. Set the KUBECONFIG environment variable. Copy the output from the previous command and paste it in your terminal. The command output should look similar to the following.

    export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/<name_of_your_cluster>/kube-config-wdc04-<name_of_your_cluster>.yml

5. Verify that you can connect to your cluster by listing your worker nodes.

    kubectl get nodes

Once your client is configured, you are ready to deploy your first application, “guestbook.”

## Deploy your application

In this part of the lab we will deploy an application called `guestbook`
that has already been built and uploaded to DockerHub under the name
`ibmcom/guestbook:v1`.

1. Start by running `guestbook`:

   ```$ kubectl run guestbook --image=ibmcom/guestbook:v1```

   This action will take a bit of time. To check the status of the running application,
   you can use `$ kubectl get pods`.

   You should see output similar to the following:

   ```console
   $ kubectl get pods
   NAME                          READY     STATUS              RESTARTS   AGE
   guestbook-59bd679fdc-bxdg7    0/1       ContainerCreating   0          1m
   ```
   Eventually, the status should show up as `Running`.
   
   ```console
   $ kubectl get pods
   NAME                          READY     STATUS              RESTARTS   AGE
   guestbook-59bd679fdc-bxdg7    1/1       Running             0          1m
   ```
   
   The end result of the run command is not just the pod containing our application containers,
   but a Deployment resource that manages the lifecycle of those pods.
 
   
3. Once the status reads `Running`, we need to expose that deployment as a
   service so we can access it through the IP of the worker nodes.
   The `guestbook` application listens on port 3000.  Run:

   ```console
   $ kubectl expose deployment guestbook --type="NodePort" --port=3000
   service "guestbook" exposed
   ```

4. To find the port used on that worker node, examine your new service:

   ```console
   $ kubectl get service guestbook
   NAME        TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
   guestbook   NodePort   10.10.10.253   <none>        3000:31208/TCP   1m
   ```
   
   We can see that our `<nodeport>` is `31208`. We can see in the output the port mapping from 3000 inside 
   the pod exposed to the cluster on port 31208. This port in the 31000 range is automatically chosen, 
   and could be different for you.

5. `guestbook` is now running on your cluster, and exposed to the internet. We need to find out where it is accessible.
   The worker nodes running in the container service get external IP addresses.
   Run `$ ibmcloud cs workers <name-of-your-cluster>`, and note the public IP listed on the `<public-IP>` line.
   
   ```console
   $ ibmcloud cs workers <name-of-your-cluster>
   OK
   ID                                                 Public IP        Private IP     Machine Type   State    Status   Zone    Version  
   kube-hou02-pa1e3ee39f549640aebea69a444f51fe55-w1   173.193.99.136   10.76.194.30   free           normal   Ready    hou02   1.5.6_1500*
   ```
   
   We can see that our `<public-IP>` is `173.193.99.136`.
   
6. Now that you have both the address and the port, you can now access the application in the web browser
   at `<public-IP>:<nodeport>`. In the example case this is `173.193.99.136:31208`.
   
Congratulations, you've now deployed an application to Kubernetes!

When you're all done, you can either use this deployment in the
[next lab of this course](../Lab2/README.md), or you can remove the deployment
and thus stop taking the course. DO NOT REMOVE the deployment if you are moving on to Lab 2. 

1. To remove the deployment, use `$ kubectl delete deployment guestbook`.

2. To remove the service, use `$ kubectl delete service guestbook`.

You should now go back up to the root of the repository in preparation
for the next lab: `$ cd ..`

