pipeline {
    agent any
    stages {
        stage('COMPILE') {
            steps {
                sh 'mvn clean compile -DskipTests=true'
            }
        }
    }
}