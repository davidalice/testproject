pipeline {
  agent {
    docker {
      args '-v /root/.m2:/root/.m2'
      image 'goyalzz/ubuntu-java-8-maven-docker-image'
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
            sh 'ifconfig'
            sh '''#apt-get install build-essential g++ libexpat1-dev libfontconfig1-dev libfreetype6-dev \\
                      libicu-dev libjpeg62-turbo-dev libpng12-dev libssl-dev zlib1g-dev'''
            sh 'mvn phantomjs:install jasmine:test'
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