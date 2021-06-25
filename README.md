# Spring Cloud Config Server

**Purpose of the Project:**
This demo project is aimed to give some information about externalizing configuation in a distributed system. 

**What is config server:**
All external properties are located one central place with this approach.  It is working as client/server architecture. Basically, all properties files of microservices are stored in a repository which can be ```GIT```  ```SVN``` or a ```local storage```. Then, all microservices act as config clients and request corresponding configuation files while one server serves in a specific port. In addition to centralization of properties files, seperation of profiles including ```dev``` ```prod``` and ```test``` environments are also supported.
In the following figure you can see one diagram chart for explanation:
![image](https://user-images.githubusercontent.com/43840820/123430966-70115f80-d5d1-11eb-8d88-61847b1ed0db.png)
