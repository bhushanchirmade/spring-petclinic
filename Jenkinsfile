pipeline {
    options { 
        buildDiscarder(logRotator(numToKeepStr: '5'))
        //discard old builds to reduce disk usage
    }
    agent any
    tools { 
        maven 'maven-3.6.3'
    }

    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}