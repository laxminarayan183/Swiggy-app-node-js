# Swiggy App deploying 
tools - Aws
      - Terraform
      - Github
      - docker
      - trivy
      - Jenkins
      - sonarqube

### step 1 
Create a IAM user with access key & id to perform terraform,Coonect with cmd
- to configure aws 
 ```
  aws configure
 ```
### step 2
- Install Terraform
- To run terraform
```
terraform init
terraform plan
terraform apply
```

### step 3
- now check tools installed
```
java --version
docker --version
jenkins --version
```
### step 4 install plugins in jenkins
- SonarQube Scanner 
- Eclipse Temurin installer 
- Pipeline Stage View
- Node.js
- OWASP dependency check
- docker - commans,pipeline,api,build step

### step 5 configure tools
- Jenkins Dashboard ---> Manage Jenkins ---> Tools ---> Add JDK ---> Name: jdk17, 'Check' install automatically, Select 'Install from adoptium.net' from dropdown, Version: select jdk-17.0.11+9 ---> Click on 'Add SonarQube Scanner', Name: sonar, 'Check' install automatically, Click on 'Add NodeJs' ---> Name: node23,version:node23, 'Check' install automatically, click on docker installation,adddocker,name:docker,'Check' install automatically,Add installer:download from docker.com ,Dependency check installatio,add dependency, name:DP-Check,'Check' install automatically,add installer:install from github.com ---> Apply ---> Save

### Step 6
- Lets configure the SonarQube server; Goto SonarQube console --- Click on 'Administration' --- Click on 'Security' --- Select 'Users' --- You can see 'Tokens' --- Click on 3 dashes icon --- A New dialogue --- Name: token, Expires in: 90days --- Generate --- You can see token in green colour. Copy it.

Token: squ_983573f5ed8baca362ba501ad6e04b3e70c23093

- Manage Jenkins --- Security --- Credentials --- Click on 'global' --- Click on 'Add Credentials' --- Kind: Secret text, Scope: Global, Secret: , ID: sonar-token, Description: sonar-token --- Create

- cerate webhook for sonarqube - sonarqube dashboard->administration->configuration->webhooks->create->
  name - jenkins
  url - pulbic_ip:8080/sonarqube/webhook
  create

- Manage Jenkins --- System --- Scroll down to 'SonarQube servers' --- Click on 'Add SonarQube' --- Name: sonar --- ServerURL: :9000 --- Server Authentication Token: select 'sonar-token' --- Apply --- Save

- Similarly configure dockerhub credentials with id as "dockerhub-token" with kind as "username with password"

### step 7 create pipeline