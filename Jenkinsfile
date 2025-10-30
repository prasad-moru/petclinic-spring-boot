pipeline {
  agent any

  options {
    timestamps()
  }

  stages {
    stage('build') {
      steps {
        echo "Building demo app..."
        sleep 1
      }
    }

    stage('test: integration-&-quality') {
      parallel {
        stage('integration') {
          steps {
            echo "Running integration tests..."
            sleep 2
          }
        }
        stage('quality') {
          steps {
            echo "Running code quality checks..."
            sleep 1
          }
        }
      }
    }

    stage('test: functional') {
      steps {
        echo "Running functional tests..."
        sleep 1
      }
    }

    stage('test: load-&-security') {
      parallel {
        stage('load') {
          steps {
            echo "Running load tests..."
            sleep 2
          }
        }
        stage('security') {
          steps {
            echo "Running security scans..."
            // Randomly fail this stage to demo red tile
            script {
              def fail = new Random().nextBoolean()
              if (fail) {
                error "Security scan failed!"
              } else {
                echo "Security scan passed!"
              }
            }
          }
        }
      }
    }

    stage('approval') {
      steps {
        script {
          echo "Waiting for manual approval..."
          input(message: 'Approve deployment to prod?', ok: 'Approve')
        }
      }
    }

    stage('deploy: prod') {
      steps {
        echo "Deploying demo app..."
        sleep 1
      }
    }
  }

  post {
    always {
      echo "Pipeline finished!"
    }
  }
}
