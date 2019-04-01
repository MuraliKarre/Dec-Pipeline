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
                sh 'scp /var/lib/jenkins/workspace/demo/webapp/target/webapp.war ubuntu@13.233.179.24:/opt/tomcat/webapps/qaenv.war'
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
                input message: 'Waiting for Delivery', submitter: 'admin'
                sh 'scp /var/lib/jenkins/workspace/demo/webapp/target/webapp.war ubuntu@13.233.179.24:/opt/tomcat/webapps/prod.war'
            }
            failure
        {
            mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'karremurali@gmail.com'
            
        }     
        }
        
        
     }
      
    
}
