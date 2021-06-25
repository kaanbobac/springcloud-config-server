
# Spring Cloud Config Server

### Purpose of the Project:
This demo project is aimed to give some information about externalizing configuation in a distributed system. 

### What is config server:
All external properties are located one central place with this approach.  It is working as client/server architecture. Basically, all properties files of microservices are stored in a repository which can be ```GIT```  ```SVN``` or a ```local storage```. Then, all microservices act as config clients and request corresponding configuation files while one server serves in a specific port. In addition to centralization of properties files, seperation of profiles including ```dev``` ```prod``` and ```test``` environments are also supported.
In the following figure you can see one diagram chart for explanation:
![image](https://user-images.githubusercontent.com/43840820/123430966-70115f80-d5d1-11eb-8d88-61847b1ed0db.png)

### Prerequisites
* Git
* JDK 8 or later
* Maven 3.0 or later
* IDE, Eclipse, IntelliJ...
* Project Lombok Plugin for IDE
https://projectlombok.org/setup/overview

### Clone the project
Since this project aims to show more than one service using config server. It basically includes three main projects which are needed to be cloned:

1. Config Server Project:
This project acts as the config server. It mainl serves for properties files whic are requested by several microservices

You can simply clone this repository using git:
```
git@github.com:kaanbobac/springcloud-config-server.git
```
2. Config Client Project:
This project can be considered as any micro service. In this approach, all microservices can be considered as one config client

You can simply clone this repository using git:
```
git@github.com:kaanbobac/springcloud-config-client-service.git
```
3. File Repository:
https://github.com/kaanbobac/sprigcloud-file-server.git

This project is the central git repository where all property files are stored.

No need to clone this project since it is just acting as a storage.

### Configuration

 1. **Config Server Port:** It is set as 8888 in application properties. It can be configured by changing the following document:
 `server.port=8888`
***Note:** If you change this port, server setting in config clietn project should also be updated!*
 
 2. **File Server:** It is set as a github repository. Any repository can be set including SVN or local file folder.
 `spring.cloud.config.server.git.uri=https://github.com/kaanbobac/sprigcloud-file-server.git`

###  How to run

 1. Run `config-client-service` application, It will run on default 8080 port. If any other configuration is not changed
 2. Run `springcloud-config-server` application. It will run on 8888 port. If no configuation is changed.
 3. In the browser open the following URI:
`http://localhost:8080/getConfig` 


Response json should be as below:
 ```json
{
    {
      "value1": 2,
      "value2": 1,
    }
}

```

###  Explanation:

 - Once we run `config-client-service` application, it will require two configuratrion values whihc are set in `Config.java` file.
` config.client.configValue1`
 `config.client.configValue2`
 - In order to retrıeve values of these configuration values, Client Service will send request to Config Server which was configured in the following setting:
 `spring.config.import=optional:configserver:http://localhost:8888`
 - Then Config Server will check the file repository which are set in the Config Server Application Properties
 ` spring.cloud.config.server.git.uri=https://github.com/kaanbobac/sprigcloud-file-server.git `
 - Matching of the file and microservice directly handling with the service name in file repository:
 **Service Name** setting in `config-client-service` application properties:
 `spring.application.name=springcloud-config-client`
 
	 **Profile** setting in `config-client-service` application properties:
` spring.cloud.config.profile=test`

	**Name** of the configuration file now:
`springcloud-config-client-test.properties`

 - Based on the above naming rule, Config Server will check correct file in File Repository. After matches is completed, Config Server will return content of the properties file to Client
 
