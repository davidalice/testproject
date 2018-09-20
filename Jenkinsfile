pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'mvn clean test'
          }
        }
        stage('Code Quality') {
          steps {
            sh 'mvn sonar:sonar -Dsonar.projectKey=davidalice_testproject -Dsonar.organization=davidalice-github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=541cba0d06de055621efd0c35a78be50f5689d11'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'mvn jasmine:bdd'
      }
    }
  }
}
