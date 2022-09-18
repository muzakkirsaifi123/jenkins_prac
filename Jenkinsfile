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
            }
        }
    }
    
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}