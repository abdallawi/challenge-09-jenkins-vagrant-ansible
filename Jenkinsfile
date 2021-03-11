pipeline {
    agent any
    
    tools  {
        maven "my-maven"
    }

    stages {
        // Start Sonarqube server
        stage("Start Sonarqube server"){
            steps{
                echo "====++++  Start sonarqube server ++++===="
                sh 'sudo docker run -d  --name my-sonarqube -p 9000:9000 sonarqube:lts'
            }          
        }



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
                      playbook: 'ansible/playbook-deploy-staging.yaml'             
            } 
        }  

        // Deploiement du WAR sur le server-staging avec Ansible
        stage("Stop sonarqube server"){
            steps{
                
                echo "====++++  Stop sonarqube server ++++===="
                sh 'sudo docker stop my-sonarqube'
                sh 'sudo docker rm my-sonarqube'
       
                         
            } 
        }        
    }
}
