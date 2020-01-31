pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        bat 'gradle artifacts build/libs/*.jar'
      }
    }

  }
}