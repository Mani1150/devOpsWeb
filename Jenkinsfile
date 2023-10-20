pipeline {
    agent any
    
    tools {
        maven 'localMaven'
    }

stages{

        stage ('Unit Test'){
            steps {
                echo "Unit Test"
            }
        }
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Email triggered"
                }
            }
        }

        stage ('Deploy'){
            parallel{
                stage ("Deploy to Staging Server1"){
                    steps {
                        deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://13.233.106.164:8080/')], contextPath: null, war: '**/*.war'
                    }
                }
                stage ('Deploy to staging Server2'){
                    steps{
                        echo "Deploy to server2!"
                    }
                }
            }
        }
    }
}
