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
    stage('Test') {
      parallel {
        stage('Check code style') {
          steps {
            echo 'Check code style'
            sh 'docker run --rm -v $(pwd):/work ivoberz/sanoma:sniffer phpcs --standard=Drupal --report=junit .'
            sh 'ls -la && cat drupal.txt'
          }
        }
        stage('Run Behat tests') {
          steps {
            echo 'Run Behat tests'
            sh 'echo $(env)'
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
    post {
        always {
            archiveArtifacts artifacts: './*.jar', fingerprint: true
            junit './*.xml'
        }
    }
    stage('Send notification') {
      steps {
        echo 'Send to slack'
      }
    }
  }
}
