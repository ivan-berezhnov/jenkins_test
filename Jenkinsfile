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
            sh 'docker run --rm -v $(pwd):/work ivoberz/sanoma:sniffer phpcs --standard=Drupal --report-file=drupal.txt --report-summary . && ls -la && cat drupal.txt'
          }
        }
        stage('Run Behat tests') {
          steps {
            echo 'Run Behat tests'
            sh '''sh \'env > env.txt\'
for (String i : readFile(\'env.txt\').split("\\r?\\n")) {
println i
}'''
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