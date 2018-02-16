pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Run Build'
        sh 'docker version'
        sh 'echo Build && pwd && ls -la && cd ../ && ls -la && docker run hello-world'
      }
    }
    stage('Check code style') {
      parallel {
        stage('Check code style') {
          steps {
            echo 'Check code style'
            sh 'path=$(pwd) && docker run --rm -v $path:/work ivoberz/sanoma:sniffer && pwd && echo \'Finish\''
            sh 'docker run hello-world'
            sh 'docker run -v $(pwd):/work ivoberz/sanoma:sniffer'
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