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
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails', path: '', url: 'http://192.168.0.108:9090')], contextPath: '/app12', war: '**/*.war'

            }

        }

        stage("Deploy on Prod"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails', path: '', url: 'http://192.168.0.108:9090')], contextPath: '/app13', war: '**/*.war'

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
