pipeline{
    agent any
    tools {
        maven 'Maven'
    }
    stages{

        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                slackSend channel: 'jenkins-pipeline', message: 'Job started.'

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
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.0.108:9090')], contextPath: '/app12', war: '**/*.war'

            }

        }

        stage("Deploy on Prod"){
            
            input {
                message "Should we deploy this project on production server?"
                ok "Sure"
            }
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.0.108:9090')], contextPath: '/app13', war: '**/*.war'

            }

        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend channel: 'jenkins-pipeline', message: 'Job executed successfully'
        }
        failure{
            echo "========pipeline execution failed========"
            slackSend channel: 'jenkins-pipeline', message: 'Job Failed.'
        }
    }
}
