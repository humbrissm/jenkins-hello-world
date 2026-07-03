pipeline {
  agent any
  stages {
    stage('Environment Check') {
      steps {
        sh 'sleep 120'
        sh 'mvn -version'
        sh 'java -version'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
        archiveArtifacts 'target/hello-demo-0.0.1-SNAPSHOT.jar'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Deploy') {
      steps {
        sh 'java -jar target/hello-demo-0.0.1-SNAPSHOT.jar &'
      }
    }

  }
  tools {
    maven 'M3915'
  }
  environment {
    JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-arm64'
    PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
  }
}