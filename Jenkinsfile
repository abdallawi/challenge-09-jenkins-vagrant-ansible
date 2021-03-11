pipeline {
    agent any
    
    tools  {
        maven "my-maven"
    }

    stages {
      // Clone from Git
        stage("Clone App from Git"){
            steps{
                echo "====++++  Clone App from Git ++++===="
                git branch:"master", url: "https://github.com/mromdhani/09-jenkins-cicd-pipeline-maven-04-vagrant-ansible.git"
            }          
        }
        // Build and Unit Test (Maven/JUnit)
        stage("Build and Package"){
            steps{
                echo "====++++  Build and Unit Test (Maven/JUnit) ++++===="
                sh "mvn clean package"
            }           
        }        
         // Deploiement du WAR sur le server-staging avec Ansible
        stage("Deploy WAR on staging using Ansible"){
            steps{
                
                echo "====++++  Deploy WAR on staging using Ansible ++++===="
       
               ansiblePlaybook   credentialsId: 'ssh_on_server_staging', 
                      //extras: '-e version=${VERSION}', 
                      //inventory: 'development', 
                      playbook: 'playbook-deploy-tomcat.yaml'             
            } 
        }        
    }
}
