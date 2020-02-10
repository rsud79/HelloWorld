pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "Default"
   }

   stages {
      stage('Build') {
         steps {
            git 'https://github.com/rsud79/HelloWorld.git'
            sh "mvn clean install"
			echo 'Completed Build stage'
         }
      }
      stage('Deploy') {
         steps {
            git 'https://github.com/rsud79/HelloWorld.git'
            sh "mvn clean install"
			echo 'Completed Deploy stage'
         }
      }
   }
}