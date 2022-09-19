pipeline {

    agent {
        label "node2"
    }

    tools {
        maven 'Maven' 
    }
    parameters {
        string defaultValue: 'MuZakkir', description: 'This is first string', name: 'Name'

    }
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
            }
        }

        stage("Test"){

            steps{
                sh "mvn test"
                slackSend channel: 'devopslearning', message: 'Your job had been started'
            }
            
        }

        stage("Build"){

            steps{
                sh "mvn package"
                
            }
            
        }

        stage("Deploy on Test") {
            when {
                branch 'main'
            }

            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://65.2.168.134:8080')], contextPath: '/app', war: '**/*.war'
              
            } 
            
        }
        stage("Deploy on Prod"){
            when {
                branch 'prod'
            }
             input {
                message "Should we continue to deploy on Prod?"
                ok "Yes we Should"
            }
            
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://43.204.116.89:8080')], contextPath: '/app', war: '**/*.war'

            }
        }
    }
    
    post{
        always{
            echo "Always give you  the status of running"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'devopslearning', message: 'Your job runed Successfully'

        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}