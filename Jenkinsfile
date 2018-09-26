pipeline {
  agent {
    docker {
      args '-v /root/.m2:/root/.m2'
      image 'markhobson/maven-chrome'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'pwd'
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'ls -l'
            timeout(time: 60, activity: true) {
              sh 'mvn -X phantomjs:install jasmine:test'
            }

          }
        }
        stage('Code Quality') {
          steps {
            sh 'mvn sonar:sonar -Dsonar.projectKey=davidalice_testproject -Dsonar.organization=davidalice-github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=541cba0d06de055621efd0c35a78be50f5689d11'
          }
        }
      }
    }
  }
}