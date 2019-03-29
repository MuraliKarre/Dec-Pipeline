pipeline {
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/MuraliKarre/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn clean package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/demo/webapp/target/webapp.war ubuntu@13.233.93.49:/opt/tomcat/webapps/qaenv.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/MuraliKarre/FunctionalTesting.git'
                sh 'java -jar  /var/lib/jenkins/workspace/demo/testing.jar'
            }
        }
    
            stage('ContDelivary')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/demo/webapp/target/webapp.war ubuntu@13.233.93.49:/opt/tomcat/webapps/qaenv.war'
            }
        }
 
        
     }
      
    
}
