# Scale a WebLogic Cluster through WKTUI and explore Verrazzano Consoles

## Introduction

We have deployed the WebLogic *opdemo* application. In this lab, we will access the application and explore grafana console, WebLogic Kubernetes Toolkit UI and WebLogic Remote Console.

Estimated time: 10 minutes

### Objectives

In this lab, you will:

* Access the WebLogic application deployed to OKE.
* Access the WebLogic Administration Console.

### Prerequisites

* You have access to the remote desktop.
* Verrazzano installed on a Oracle Kubernetes Cluster.
* WebLogic *opdemo* application is deployed to Oracle Kubernetes Cluster using WebLogic Kubernetes Toolkit UI.

## Task 1: Access the WebLogic Application and show load balancing

1. Open Chrome browser, Click the first Bookmark *WebLogic App*.
    ![weblogic application](images/weblogic-application.png)

2. Click the refrest button to access the application again, and you will notice request is served by another managed server instance. which reflect load balancing between two managed servers.
    ![application managed 1](images/application-man-1.png)
    ![application managed 2](images/application-man-2.png)

## Task 2: Showcase the WebLogic Console and explore domain resources

1. Open a new tab in Chrome browser and Click the second Bookmark *WebLogic Console*.
    ![weblogic console url](images/weblogic-console-url.png)

2. Enter the credential and click *Login*.
    ![weblogic login](images/weblogic-login.png)

3. Click *Environment* -> *Servers*, to view the running servers inside the domain.
4. Click *Deployments*, to view the deployed *opdemo* application.
5. Click *Services* -> *Data sources*, to view the JDBC datasource for the application.


## Task 3: Explore the Rancher and Grafana Console

1. Open a new tab in Chrome browser and Click the third Bookmark *Rancher Console*. Click *Login with Keycloak*. Enter *verrazzano* as Username and *X7jve6ftLz3NKvY9* as Password and  then click *Sign in*.
    ![rancher url](images/rancher-url.png)
    ![rancher signin](images/rancher-signin.png)

3. From the home page of the rancher console, you can view the Verrazzano Links. you can access any of these consoles from rancher console.Click *Hamburger menu* -> *Verrazzano*.
    ![rancher home](images/rancher-home.png)


4. Click *Applications*. This section shows all the applications with their namespace and is managed by Verrazzano. Click the *hello-helidon-appconf* application within the *hello-helidon* namespace.
    ![deployed application](images/deployed-application.png)


5. You can view the pods associated with the application. The pod name contains an auto-generated unique string to identify that particular replica. To view the Component associated with the application, click *Components*.
    ![view pods](images/view-pods.png)
    ![helidon components](images/weblogic-components.png)


6. Click *Hamburgar menu* -> *local*, to open the *Cluster Explorer*. The *Cluster Explorer* allows you to view and manipulate all of the custom resources and CRDs in a Kubernetes cluster from the Rancher UI.
    ![view local](images/view-local.png)
    ![cluster dashboard](images/cluster-dashboard.png)


7. Open a new tab in Chrome browser and Click the fourth Bookmark *Grafana Console*.
    ![grafana url](images/grafana-url.png)


8. The Grafana Home Page opens. Select *Home*  at the top left.

9. Type *WebLogic* and you will see *WebLogic Server Dashboard* under *General*. Select *WebLogic Server Dashboard*.

    ![weblogic dashboard](images/weblogic-dashboard.png)

    Here you can observe the two managed servers under *test-domain*. You can view *Heap Usage*, *JVM Heap*, *CPU Load* and other data.



## Task 4: Scale a WebLogic cluster through WKTUI

1. In Remote Desktop, Open WKTUI. 

2. Click *Component* under *Verrazzano*, and then click *Edit* icon for cluster section as shown below.
    ![cluster size](images/cluster-size.png)

3. Change the *Replicas* value from *2* to *3* and click *OK*. 
    ![replica value](images/replicas-value.png)

4. Click *Deploy Component* to re-deploy the *opdemo* application.

5. Open the terminal, copy and paste the following command to the terminal. 
    ```bash
    <copy>kubectl get pods -n test-domain-ns -w</copy>
    ```
    ![view scaling](images/view-scaling.png)


## Task 5: Showcase changes in application, WebLogic Remote Console console and Verrazzano Console

1. Access the application URL, and verify that application is running on managed server 3 as well. 
    ![app man 3](images/app-man-3.png)


2. Refresh the grafana console, and you can view *managed-server3* here as well.
    ![grafana man 3](images/grafana-man-3.png)

3. Open WebLogic Remote Console, and you can show *managed-server3* updated here as well.
    ![remote console](images/remote-console.png)

## Acknowledgements

* **Author** -  Ankit Pandey
* **Contributors** - Maciej Gruszka, Sid Joshi
* **Last Updated By/Date** - Ankit Pandey, September 2023
