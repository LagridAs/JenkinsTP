pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        bat 'archiveArtifacts build/libs/*.jar'
        bat 'archiveArtifacts build/docs/javadoc'
        bat 'archiveArtifacts build/test-results/test'
      }
    }

  }
}