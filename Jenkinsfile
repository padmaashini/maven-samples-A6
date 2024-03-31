pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/padmaashini/maven-samples-A6.git', branch: 'master')
      }
    }
    stage('Check Java Version') {
      steps {
        sh 'java -version'
      }
    }
    stage('Print Effective POM') {
      steps {
        sh 'mvn help:effective-pom'
      }
    }
    stage('Build Modules') {
      steps {
        sh 'cd multi-module && mvn clean install'
        sh 'cd single-module && mvn clean install'
      }
    }
    stage('git bisect') {
      steps {
        sh 'git bisect start 198644632661c67b6c32f59e9047c11a70685e15 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
        sh 'git bisect run mvn clean test'
        sh 'git bisect reset'
      }
    }

  }
  tools {
    maven 'DHT_MVN'
    jdk 'DHT_SENSE'
  }
}
