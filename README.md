# Java maven project 
## Build Project
mvn clean
mvn package

## Build Custom Docker image 
Create custom image
1. build my image
    - docker build -t <tag_name> <path_to_dockerfile> --> docker build -t tomcat_1 .

2. Run 
    - docker run <image_name>
    - docker run -d <image_name>
        - docker run -d tomcat_1
    - docker run -d -p <local_port>:<container_port> <image_name>
     - we also run multiple container with same image 
        - docker run -dp 8000:8080 tomcat_1
        - docker run -dp 8001:8080 tomcat_1

3. login to container
    - docker exec -it <container_id> /bin/bash  

4. Docker Push and Pull Own Images
    - To Push into Docker hub,  login to docker with your docker credentials
        - docker login
        - docker image tag tomcat_1:latest seetha123/pac_tomcat:latest
        - docker image push seetha123/pac_tomcat:latest

    - Pull image from docker hub
        - docker pull seetha123/pac_tomcat
        - docker run -dp 8080:8080 seetha123/pac_tomcat 

## Jenkinsfile
    - Build tomcat application - custom docker image
    - Push into docker hub registry
    - SSH into Docker host 
        - pull latest tomcat custom image from docker hub registry
        - run the tomcat container 