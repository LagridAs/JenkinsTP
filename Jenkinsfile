pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Test Jenkins', body: 'heloo', to: 'ga_lagrid@esi.dz', cc: 'ga_goumeida@esi.dz', replyTo: 'ga_lagrid@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            jacoco(classPattern: 'src/main/java/com/example/**/*.java', exclusionPattern: 'src/test/java/com/test/*.java', sourcePattern: 'src/**')
          }
        }

      }
    }

    stage('Deployement') {
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(channel: 'tpjenkins', message: 'heyoooo jenkins', sendAsText: true, notifyCommitters: true, replyBroadcast: true, token: 'TTLSJ5YJ3/BT8S57H3K/Vk9v7S1b7pyHZzIkixSMDfxw', baseUrl: 'https://hooks.slack.com/services', teamDomain: 'tpjenkins-groupe')
      }
    }

  }
}