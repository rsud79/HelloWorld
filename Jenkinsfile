pipeline {
    agent any
    
    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    IMAGE = readMavenPom().getArtifactId()
    VERSION = readMavenPom().getVersion()
    }

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : "${VERSION}") {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : "${VERSION}") {
                    sh 'mvn test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                withMaven(maven : "${VERSION}") {
                    sh 'mvn deploy'
                }
            }
        }
    }
}