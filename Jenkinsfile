pipeline {
    options { 
        buildDiscarder(logRotator(numToKeepStr: '5'))
        //discard old builds to reduce disk usage
    }
    agent any
    tools { 
        maven '3.8.6'
    }

    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}