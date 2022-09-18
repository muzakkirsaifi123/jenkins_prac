pipeline {
    agent {
        label "node2"
    }
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                sh "mvn test"
                // slackSend channel: 'jenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://65.2.168.134:8080')], contextPath: '/app', war: '**/*.war'
              
            } 
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
                echo "passe please"
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            //  slackSend channel: 'jenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
            //  slackSend channel: 'jenkins', message: 'Job Failed'
        }
    }
}