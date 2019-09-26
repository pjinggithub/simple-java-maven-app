pipeline {
    agent {
        any {}
    }
    stages {
       def mvnHome
       stage('Preparation') { 
          // Get the Maven tool.
          // ** NOTE: This 'M3' Maven tool must be configured
          // **       in the global configuration.           
          mvnHome = tool 'M3'
       }

        stage('Build') {
            steps {
                sh ' "$mvnHome/bin/mvn" -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh '"$mvnHome/bin/mvn" test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
