## Operation Scenario
Tencent Kubernetes Engine (TKE) is a highly scalable high-performance container management service allowing you to easily run applications on hosted CVM instance clusters. In this tutorial, you will understand how to use TKE to quickly create and manage container clusters and how to quickly and flexibly deploy your services in the clusters.    

## Steps
### Creating a Cluster
At first, you need to create a cluster. A cluster refers to the collection of cloud resources required by container operation, including several CVM instances, load balancers, and other Tencent Cloud resources.
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. Click **Create** above the list of clusters in the **Cluster Management** page. See the figure below:
![](https://main.qcloudimg.com/raw/657fdbd2086f82130ca5ee3464ad27b7.png)
3. Set the basic information for the cluster on the **Create Cluster** page and click **Next**. See the figure below:
 - **Cluster Name**: The name of a cluster to create, with a length limited to 60 characters.
 - **Project of New-added Resource**: Select based on actual needs. Newly added resources will be automatically assigned to this project.
 - **Kubernetes Version**: Multiple Kubernetes versions are provided for your choice. Click [here](https://kubernetes.io/docs/home/supported-doc-versions/) to view feature differences of the versions.
 - **Runtime Component**: Choose “docker” or “containerd”. For more details, see [Differences Between Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: Select the closest region based on your location. This helps minimize access latency and improve download speed.
 - **Cluster Network**: Assigns an IP address that is within the node’s network address range to the CVMs in the cluster. For details, see [Container and Node Network Configuration](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Container Network**: Assigns an IP address that is within the container’s network address range to the containers in the cluster. For details, see [Container and Node Network Configuration](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Image Provider**: To be selected based on your requirements.
 - **Operating System**: To be selected based on your requirements.
 - **Cluster description**: Enter the information about the cluster, which will be displayed on the **Cluster Information** page.
 - **Advanced Settings**: You can set IPVS.
 IPVS is suitable for scenarios where large-scale services are run on a cluster, and it  cannot be disabled once enabled. For more information, see [Enabling IPVS in a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
![](https://main.qcloudimg.com/raw/d49afe5f602d29d641ced8a56991c3a2.png)
4. Select the model and click **Next**. See the figure below:
 - **Create Cluster**: To be selected based on your requirements.
 - **Master**: The deployment method of “Master” determines the management mode for your cluster. There are two cluster modes, “fully-managed” and “self-managed”. For more details, see [Cluster Types](https://intl.cloud.tencent.com/document/product/457/30635#cluster-type).
 - **Node**: Configures the worker node that is actually used by the cluster to run services. You can purchase a CVM as the **Node** when you create the cluster, or you can add the **Node** after the cluster has been created.
 - **Billing method**: This provides the Pay as you go billing mode. For more details, please see [Billing Method](https://intl.cloud.tencent.com/document/product/213/2180).
 - **Node Model**: This can be selected when **Node** is selected as **Add**. You can select an existing CVM as the **Node** and you can also add a **Node** after the cluster is created.
![](https://main.qcloudimg.com/raw/aa2446d6cf8e17def9c353afc36fa42b.png)
5. Enter the CVM configuration and click **Next**. See the figure below:
 - **Data disk mounting**: Check this based on your own requirements. After checking it, the following operations will occur:
    - The data disk will automatically be mounted to the mount point you designated and will be automatically formatted to the ext4 file system format. 
    - The container will be saved to the container directory of the mount point. 
    - This option is only valid for nodes that have one data disk.
 - **Security group**: The security group works as a firewall to control network access of the CVM. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login method**: Three login methods are available.
    - **Custom Password**: Set a corresponding password as prompted.
    - **SSH Key Pair**: A key pair is a pair of parameters generated by an algorithm. It is a way to log in to a CVM instance that is more secure than regular passwords. For more details, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random Password**: A password will be automatically generated and sent to you through internal message.
 - **Auto adjustment**: A scaling group with a maximum of two nodes can be created automatically.
![](https://main.qcloudimg.com/raw/960e92c51bd77ed5bf88bf7ef55e5c7e.png)
6. Check that the settings information, and click **Complete** to complete the creation of the new cluster. See the figure below:
![](https://main.qcloudimg.com/raw/b14c652a4069a87eeef0d76d57dab50b.png)
7. The created cluster is displayed in the cluster list.
![](https://main.qcloudimg.com/raw/8e8c2c6cf2f2150b298a59c468128ee7.png)

### Creating a Service
After a cluster is created, you need to create a service. A service is a microservice comprised of multiple containers with the same configuration and rules used to access these containers.
1. Click on the cluster ID for which the service is to be created to enter Deploymentpage. Click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/4e84b38183f3e618534c6d16e23be6e1.png)
2. Set the workload basic information. See the figure below:
 - **Workload Name**: The name of the workload to be created.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as “k8s-app = workloadname”.
 - **Namespace**: Select a namespace based on your requirements.
 - **Type**: Select a type based on your requirements.
![](https://main.qcloudimg.com/raw/3a6e85e181371569e6034c8dfa40e481.png)
3. (Optional) Set the volume. Click **Add Volume** when you specify a specific path to which a container is mounted. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678). See the figure below:
> If no source path is specified, a temporary path is assigned by default.
> 
 - **Type**: The seven types of volumes that are supported are temp directory, CVM path, NFS disk, existing VPC, Tencent Cloud block storage, ConfigMap, and Secret. For a more detailed introduction, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
 - **Name**: Name of volume.
![](https://main.qcloudimg.com/raw/a4e6150eedd0c7385b4a170649042cee.png)
4. Set **Containers in the Pod**. See the figure below:
 - **Name**: Enter the name of the container to create.
 - **Image**: Click **Select Image** to select an image from My Images, My Favorites, TencentHub Image, DockerHub Image or other images.
 - **Image Tag**: The default version selected for TKE. If you need to use a different image tag, click the tag display box to select one.
 - **CPU/memory limit**: Request is used to pre-allocate resources. When the nodes in the cluster do not have enough resources for the request, the container will fail to be created. Limit specifies the maximum usage of resources of container to avoid abnormal excessive consumption of node resources.
 - **GPU limit**: Set the limit based on your requirements.
 - **Environment variable**: Variable name can only contain uppercase and lowercase letters, numbers, and underscores and cannot begin with a number
![](https://main.qcloudimg.com/raw/fc1425d8ba8d84599a3b84a7376b6d7d.png)
5. Set the **Number of Pods**. See the figure below:
 - Manual adjustment: Set the number of pods. The number of pods in this example is set as 1. You can click “+” or “-” to change the number of pods.
 - Auto adjustment: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
![](https://main.qcloudimg.com/raw/292f93f595f95dd798385470f1f5dac7.png)
6. Configure the access settings. See the figure below:
 - **Service**: Check **Enable**.
 - **Service Access**: The method for accessing a service determines the network attribute of this service. Different access methods offer different network capabilities. For more information about the four access methods, please see [Configuration of Service Access Methods](https://intl.cloud.tencent.com/document/product/457/9098).
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**：Select **Protocol**, and fill in the **Container port** and **Service port**.
![](https://main.qcloudimg.com/raw/bcab65ccaefa2ae76d1a603b5be3e64d.png)
7. Click **Create workload** to complete the creation of the service. The created service will appear in the list of services.

#### Viewing Resources
In previous steps, you have created a cluster and a service. In this step, you can view all the resources you created.
#### Viewing Cluster
1. Click **Cluster** in the left sidebar, and select the ID of a cluster in the cluster list page. See the figure below:
![](https://main.qcloudimg.com/raw/27fe4213679dd9db6c30337b261b2eb9.png)
2. After clicking, the Deployment page appears by default. See the figure below:
 - **Basic Info**: It displays the basic cluster information.
 - **Node Management**: A node is a CVM registered in the cluster. You can create a node, add an existing node, and create scaling rules here.
 - **Namespace**: A namespace is an abstract collection of a group of resources and objects. You can create and delete namespaces here.
 - **Workload**, **Service**, **Configuration management**, **Storage**: These are resource objects often used in Kubernetes. For more details, see [Types of Objects](https://intl.cloud.tencent.com/document/product/457/30658#.E5.AF.B9.E8.B1.A1.E5.88.86.E7.B1.BB). 
 - **Log**: Displays the related log information.
 - **Event**: You are redirected to this page when creating a service. It displays the details during the creation of service.
![](https://main.qcloudimg.com/raw/660416e8efb5066f2998dd1343bfba43.png)

### Viewing Services
1. In the left sidebar, click **Clusters** to go to the **Cluster Management** page.
2. Click on the cluster ID of the created service and select **Service** > **Service**. See the figure below:
![](https://main.qcloudimg.com/raw/727dda83385a8df6f5f8a43ce0235b67.png)
3. Click the service name in the **Service** list to enter the service details page. See the figure below:
 - **Details**: Displays the basic information and the advanced settings information of the service.
 - **Event**: Displays the event information that has occurred in the last hour.
 - **YAML**: Services can be updated by editing YAML.
![](https://main.qcloudimg.com/raw/7174e1a17add9e10de02cf2ab64605f1.png)

### Deleting Resources
In this tutorial, you have enabled two types of resources: clusters and services. In this step, you can delete all the resources to avoid unnecessary costs.
### Deleting a Cluster
1. Click **Clusters** in the left sidebar, and select **More** > **Delete** to the right of the list of the cluster to be deleted. See the figure below:
![](https://main.qcloudimg.com/raw/0f58c601a0798b606524f85ce6956a0b.png)
2. After confirming the information in the pop-up box, click **OK** to delete the cluster. See the figure below:
>
>- The cluster cannot provide services during deletion. Please prepare in advance to avoid the impact.
>- When a cluster is deleted, the services under this cluster will also be deleted along with it.
>
![](https://main.qcloudimg.com/raw/3895976c887248aac68eb4f225f5f169.png)


#### Delete a Service
1. In the left sidebar, click **Clusters** to go to the **Cluster Management** page.
2. Click the cluster ID of the service to be deleted to enter the cluster details page.
3. Select **Service** > **Service** to enter the service information page.
4. Click **Delete** to the right of the service list. See the figure below:
![](https://main.qcloudimg.com/raw/2364fa8f566afba9a7504a8e4d8ce531.png)
5. Click **OK** in the pop-up box to delete the service.

### More
In this tutorial, you have learned how to configure, deploy, and delete services in Tencent Cloud TKE. With Tencent Cloud TKE, you don't need to install, operate, maintain, or expand your cluster management infrastructure. You can enable and disable Docker applications, query full status of the cluster, and use various cloud services by simply calling APIs.

Go to the next tutorial and learn about the basic concepts and operations of [Cloud load balancer](https://intl.cloud.tencent.com/document/product/457/9110) and [Image registry](https://intl.cloud.tencent.com/document/product/457/9118) and quickly build services by viewing [Examples on How to Get Started](https://intl.cloud.tencent.com/document/product/457/11138).

​                                          
