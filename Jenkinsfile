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
            sh "mvn clean install" //Example goal
			echo 'Completed Build stage'
			comment_issues(env.STAGE_NAME)
         }
      }
      stage('Deploy') {
         steps {
            git 'https://github.com/rsud79/HelloWorld.git'
            sh "mvn clean install"
			echo 'Completed Deploy stage'
			comment_issues(env.STAGE_NAME)
         }
      }
      stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
   }
}

@NonCPS
void comment_issues(stageName) {
    
    //Define pattern for JIRA IDs to be updated
    def issue_pattern = "LP-\\d+"
    
    //Retrieve the commit message and parse for the issue_pattern
    currentBuild.changeSets.each {changeSet ->
        changeSet.each { commit ->
            String msg = commit.getMsg()
            echo msg
            msg.findAll(issue_pattern).each {
                // Post the comment along with the stage name - the "site" parameter needs to be set up in Jenkins
                id -> jiraAddComment idOrKey: id, comment: msg+ ' in '+stageName, site: 'JIRA'
            }
        }
    }
}