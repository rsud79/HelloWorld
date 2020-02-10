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
			script {
			    last_started = env.STAGE_NAME
			    echo last_started
			}

			comment_issues(last_started)
         }
      }
      stage('Deploy') {
         steps {
            git 'https://github.com/rsud79/HelloWorld.git'
            sh "mvn clean install"
			echo 'Completed Deploy stage'
			script {
			    last_started = env.STAGE_NAME
			    echo last_started
			    
			}
			comment_issues(last_started)
         }
      }
   }
}

@NonCPS
void comment_issues(stageName) {
    def issue_pattern = "LP-\\d+"

    // Find all relevant commit ids
    currentBuild.changeSets.each {changeSet ->
        changeSet.each { commit ->
            String msg = commit.getMsg()
            echo msg
            msg.findAll(issue_pattern).each {
                // Actually post a comment
                id -> jiraAddComment idOrKey: id, comment: msg+ ' in '+stageName, site: 'JIRA'
            }
        }
    }
}