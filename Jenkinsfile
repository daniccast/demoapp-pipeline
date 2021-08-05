pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
      }
    }

    stage('LINUX TEST') {
      parallel {
        stage('LINUX TEST') {
          steps {
            echo 'LINUX tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('WINDOWS TEST') {
          steps {
            echo 'Windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production? '
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'danielaccaso@gmail,com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}