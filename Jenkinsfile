pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Run Build'
        sh 'echo Build && pwd && ls -la && cd ../ && ls -la && docker version'
      }
    }
    stage('Check code style') {
      parallel {
        stage('Check code style') {
          steps {
            echo 'Check code style'
          }
        }
        stage('Run Behat tests') {
          steps {
            echo 'Run Behat tests'
          }
        }
        stage('Run sass linter') {
          steps {
            echo 'Run SASS linter'
          }
        }
        stage('Run jslint') {
          steps {
            echo 'Run JSLint'
          }
        }
      }
    }
    stage('Reports') {
      steps {
        echo 'Create reports'
        sh 'echo Reports for build'
      }
    }
    stage('Send notification') {
      steps {
        echo 'Send to slack'
      }
    }
  }
}