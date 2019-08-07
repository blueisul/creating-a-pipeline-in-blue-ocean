pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2 -p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh 'mvn test'
      }
    }
    stage('Deliver') {
      steps {
        sh 'chmod 755 ./jenkins/scripts/deliver.sh'
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
      }
    }
  }
}