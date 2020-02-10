pipeline {
    agent any
    
    environment {
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    IMAGE = readMavenPom().getArtifactId()
    VERSION = readMavenPom().getVersion()
    //echo "IMAGE: ${IMAGE}"
    //echo "VERSION: ${VERSION}"
    }

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : "${VERSION}") {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Install Stage') {

            steps {
                withMaven(maven : "${VERSION}") {
                    sh 'mvn clean install'
                }
            }
        }
    }
}