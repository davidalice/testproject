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
        sh 'pwd'
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'ifconfig'
            sh 'pwd'
            sh 'sudo apt-get update -y'
            sh '''
sudo apt-get upgrade -y'''
            sh 'sudo shutdown -r now'
            sh 'sudo apt-get install build-essential chrpath libssl-dev libxft-dev libfreetype6-dev libfreetype6 libfontconfig1-dev libfontconfig1 -y'
            sh 'sudo wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2'
            sh 'sudo tar xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2 -C /usr/local/share/'
            sh '''sudo ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/
'''
            sh 'phantomjs --version'
            sh 'whereis phantomjs'
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