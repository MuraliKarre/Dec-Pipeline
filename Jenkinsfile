pipeline
{
    agent any
    stages
    {
        stage('ContDownloadd')
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
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/Demo/webapp/target/webapp.war ubuntu@13.233.179.24:/opt/tomcat/webapps/qaenv.war'
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
    }
    post
    {
        success
        {
            input message: 'Waiting for approval from DM', submitter: 'admin'
    sh 'scp /var/lib/jenkins/workspace/Declarative_Pipeline/webapp/target/webapp.war ubuntu@13.233.179.24:/opt/tomcat/webapps//prodenv.war'
        }
        failure
        {
            mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'karremurali@gmail.com'
            
        }
        
     }
      
    
}
