

Project overview:

This project is focusing on building a catog-service application using Java files and using spring boot with gradle to build and kubernetes to deploy the application.

The first step is to create our Java files and build them using spring intilizer and gradle, for this project I have chosen to use IntelliJ as my IDE. *Java and Gradle must be downloaded and installed locally. (I am using Java 17 and Gadle 8.3) 

 CatalogServiceApplication.java
package com.polarbookshop.catalogservice;


import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;


@SpringBootApplication
public class CatalogServiceApplication {


   public static void main(String[] args) {
       SpringApplication.run(CatalogServiceApplication.class, args);
   }


}

This is the application that will be deployed.

HomeController.java
package com.polarbookshop.catalogservice;


import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class HomeController {


   @GetMapping("/")
   public String getGreeting() {


       return "Welcome to the book catalog!";
   }
}

This Rest controller will determine a endpoint and will return the greeting “Welcome to the book catalog!” when the root URL is accessed. 

Open Docker Desktop (v4.24.2) now we can run the bootBuildImage command either within the CLI or on the GUI Via the catalog-service>build>bootBuildImage


Verify the container is running and you can access the URL 


Load the docker image into minikube using the command:
$ minikube image load catalog-service:0.0.1-SNAPSHOT

Create deployment using the command:
$ kubectl create deployment catalog-service --image=catalog-service:0.0.1-SNAPSHOT

Expose Deployment using the command:
	$ kubectl expose deployment catalog-service --name=catalog-service --port=8080




Verify the creation using the command:
	$ kubectl get service catalog-service


 Now we can forward the traffic from a local port on our computer (8000) to the port being used by the cluster (8080) using the following command:
$ kubectl port-forward service/catalog-service 8000:8080



Verify that you can access the URL with the port 8000 and you get the expected results


We have a working Java application that is deployed kubernetes, we are able to access the URL: http://localhost:8000 and get the intended response.


The code for this project can be found at the following URL - 

GitHub: https://github.com/Halen0Jacobsen/catalog-service
