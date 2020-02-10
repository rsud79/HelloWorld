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
      stage('JIRA') {
          steps {
              comment_issues()
          }
      }
   }
}

void comment_issues() {
    def issue_pattern = "LP-\\d+"

    // Find all relevant commit ids
    currentBuild.changeSets.each {changeSet ->
        changeSet.each { commit ->
            String msg = commit.getMsg()
            echo msg
            msg.findAll(issue_pattern).each {
                // Actually post a comment
                id -> jiraAddComment idOrKey: id, comment: 'Hi there!', site: 'http://localhost:8080/'
            }
        }
    }
}