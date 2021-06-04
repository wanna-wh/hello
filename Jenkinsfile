pipeline {
  environment {
    imageName = 'hello'
    containerName = 'hello'
  }
  agent {
    label 'hello'
  }
  stages {
    stage('Build Jar') {
      steps {
        tool 'jdk-11'
        sh './gradlew clean build -Dorg.gradle.java.home=/home/ubuntu/jenkins/tools/hudson.model.JDK/jdk-11'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build(imageName)
        }
      }
    }

    stage('Docker Run') {
      steps {
        sh """
          docker stop ${containerName} && docker rm ${containerName}
          docker run -d --name ${containerName} -p 8080:8080 ${imageName}
        """
      }
    }
  }
}
