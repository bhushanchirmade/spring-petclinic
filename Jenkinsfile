pipeline {
    options { 
        buildDiscarder(logRotator(numToKeepStr: '5'))
        //discard old builds to reduce disk usage
    }

    stages {
        stage('Checkout SCM') {
            steps {
                //this step runs on the default jnlp agent, which has git installed:
                //docker run --rm -i -t jenkins/jnlp-slave:alpine git
                git branch: 'main', url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
        stage('Build and Test with Maven') { //in "spot agents" pool
            steps {
                //this step runs in a different container using the raw yaml above,
                //and the workspace is shared with the default jnlp agent
                container('maven') {
                    sh 'unset MAVEN_CONFIG && ./mvnw package'
                    //note that the master branch of an active project
                    //may not always build successfully..
                    archiveArtifacts 'target/*.jar'
                    //download the artifact from the UI and run it:
                    //'java -jar <artifactName>.jar' then visit http://localhost:8080
                }
            }
        }
        stage ('Deploy') {
            steps {
                container('aws-cli') {
                    sh 'aws --version'
                }
            }
        }
    }
}