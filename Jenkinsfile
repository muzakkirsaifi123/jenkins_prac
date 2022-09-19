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

        stage("Test"){

            steps{
                sh "mvn test"
                slackSend channel: 'devopslearning', message: 'Your job had been started by ${Name}'
            }
            
        }

        stage("Build"){

            steps{
                sh "mvn package"
                
            }
            
        }

        stage("Deploy on Test") {

            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://65.2.168.134:8080')], contextPath: '/app', war: '**/*.war'
              
            } 
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                echo "passe please"
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://43.204.116.89:8080')], contextPath: '/app', war: '**/*.war'

            }
        }
    }
    
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'devopslearning', message: 'Your job runed by ${Name} successfully'

        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}