# Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes

![Screenshot 2023-03-28 at 9 38 09 PM](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)

1) CI - ensures that build is smoths, tests successful , image is create, Code quality is good.
2) CD - Ensures that deployment or delivery process is done
3) WHEN WE ARE USING DOCKER AS AGENT THEN WE DON'T NEED TO WORRY ABOUT THE TOOLS CONFIGURATIONS AT ALL
4) IF WE USE THE DOCKER AS AGENT WE CAN SKIP THE INSTALLATIONS AND CONFIGURATIONS OF THE TOOLS

![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/b09c9b10-6f6b-4c0b-90cf-db59e6ba3eca)
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/7b6d51b7-9519-46f2-8f9b-4fa3c80d4ab1)
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/d2bf3ec2-9cfb-44b1-ac77-3fd1e82a40b9)
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/57b72edd-6733-4d1a-9a5c-5b744a9789b4)
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/349a7432-f84f-490f-817b-a4aef3f1a40a)

# --
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/8a405fb7-f8a1-4171-ba39-9ba68e56f0de)
![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/1c9697b9-df8d-4a1a-9f7b-896c6e313b9d)


# Installation of any controllers like ARGO-CD in kubernetes
--
1) Installation of the tools should be done using kubernetes operators
2) Operators will manage the life cycle of the kubernetes controllers(updates, etc)
3) Go to ``` https://operatorhub.io/ ``` and search for ARGO CD and install it
4) check pods unders operators namespace, svc and etc
5) Go to ```https://argocd-operator.readthedocs.io/en/latest/usage/basics/``` and create deployment
6) ```
   apiVersion: argoproj.io/v1alpha1
         kind: ArgoCD
         metadata:
           name: example-argocd
           labels:
             example: basic
         spec: {}
   ```

8) ``` kubectl edit svc example-argocd-server ``` bydefault argocd-server will be with clusterip change it to NodePort ip under type
9) ``` minikube service argocd-server ``` To start argocd-server for web UI
10) ``` minikube service list ``` Now the example-argocd-server type will be changed to NodePort and we will get ip:port address as well if not check with -o wide
11) ``` kubectl get pods ```
12) ``` kubectl get secret ``` To find all the secrets
13) ``` kubectl edit secret example-argocd-cluster ``` Select argo-cluster to find the password of ARGO CD -- username is admin
14) ``` echo cmlhMkhvUEY5dWRtMzZTWVJwbkdnQjFLUVhXa3FFRFo= | base64 -d ``` Bydefault password will be encrypted so we have to decode it using base64
15) ``` We get the password for the secret ``` kubectl edit secret example-argocd-cluster ``` and find initial password it will be open in vim editor
16) after entering the password click on new app
17) ![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/0cd72525-e2c0-4ab4-a1d7-fbb8b64e53e4)
18) path -- here we have to give path of manifest files as per github
19) ![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/1bb56a44-0f69-4159-a696-97ebf4f30379)
20) App details
21) ![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/c9adf8fc-d295-486f-a967-c96688d761b5)
22) Dashboard ARGO CD
23) ![image](https://github.com/pavankumar0077/Jenkins-Zero-To-Hero/assets/40380941/6a3f1c0a-9215-4e85-b185-e6f64be8300e)
24) To access the application ``` kubectl get svc -o wide ``` and select spring-boot-svc WHICH we have created the service using service.yml file --select the name
25) Get the minikube ip ``` minikube ip ```
26) find the port number from svc and add minikube ip : svc port
27) ``` http://192.168.39.30:31702/ ```
28) Now you can able to access the applicaiotn using service port, we can also check using minikube ssh with cluster ip or pod ip but for web ui alwasy recommeded to use service port and minkube ip.




Here are the step-by-step details to set up an end-to-end Jenkins pipeline for a Java application using SonarQube, Argo CD, Helm, and Kubernetes:

Prerequisites:

   -  Java application code hosted on a Git repository
   -   Jenkins server
   -  Kubernetes cluster
   -  Helm package manager
   -  Argo CD

Steps:

    1. Install the necessary Jenkins plugins:
       1.1 Git plugin
       1.2 Maven Integration plugin
       1.3 Pipeline plugin
       1.4 Kubernetes Continuous Deploy plugin

    2. Create a new Jenkins pipeline:
       2.1 In Jenkins, create a new pipeline job and configure it with the Git repository URL for the Java application.
       2.2 Add a Jenkinsfile to the Git repository to define the pipeline stages.

    3. Define the pipeline stages:
        Stage 1: Checkout the source code from Git.
        Stage 2: Build the Java application using Maven.
        Stage 3: Run unit tests using JUnit and Mockito.
        Stage 4: Run SonarQube analysis to check the code quality.
        Stage 5: Package the application into a JAR file.
        Stage 6: Deploy the application to a test environment using Helm.
        Stage 7: Run user acceptance tests on the deployed application.
        Stage 8: Promote the application to a production environment using Argo CD.

    4. Configure Jenkins pipeline stages:
        Stage 1: Use the Git plugin to check out the source code from the Git repository.
        Stage 2: Use the Maven Integration plugin to build the Java application.
        Stage 3: Use the JUnit and Mockito plugins to run unit tests.
        Stage 4: Use the SonarQube plugin to analyze the code quality of the Java application.
        Stage 5: Use the Maven Integration plugin to package the application into a JAR file.
        Stage 6: Use the Kubernetes Continuous Deploy plugin to deploy the application to a test environment using Helm.
        Stage 7: Use a testing framework like Selenium to run user acceptance tests on the deployed application.
        Stage 8: Use Argo CD to promote the application to a production environment.

    5. Set up Argo CD:
        Install Argo CD on the Kubernetes cluster.
        Set up a Git repository for Argo CD to track the changes in the Helm charts and Kubernetes manifests.
        Create a Helm chart for the Java application that includes the Kubernetes manifests and Helm values.
        Add the Helm chart to the Git repository that Argo CD is tracking.

    6. Configure Jenkins pipeline to integrate with Argo CD:
       6.1 Add the Argo CD API token to Jenkins credentials.
       6.2 Update the Jenkins pipeline to include the Argo CD deployment stage.

    7. Run the Jenkins pipeline:
       7.1 Trigger the Jenkins pipeline to start the CI/CD process for the Java application.
       7.2 Monitor the pipeline stages and fix any issues that arise.

This end-to-end Jenkins pipeline will automate the entire CI/CD process for a Java application, from code checkout to production deployment, using popular tools like SonarQube, Argo CD, Helm, and Kubernetes.
