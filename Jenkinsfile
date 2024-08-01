pipeline {
  agent any
  // agent {
    // node {
    //   label 'my-label'
    // }
  // }
  stages {
    stage('Checkout source code') {
      steps {
        git branch: 'master',
        credentialsId: 'my_cred_id',
        url: 'https://github.com/HoangPhu98/react-for-demo.git'
        sh "ls -la"
      }
    }

    stage ('Install dependencies') {
      steps {
        nodejs(nodeJSInstallationName: 'nodejs 8.9.4') {
          sh 'echo "Installing..."'
          sh 'npm install'
          sh 'echo "Install dependencies successfully."'
          sh 'ls -al'
        }
      }
    }
    
    stage ('Test') {
      steps {
        nodejs(nodeJSInstallationName: 'nodejs 8.9.4') {
          sh 'echo "Run unit test..."'
          sh 'npm test'
          sh 'echo "Run unit test successfully."'
          sh 'ls -al'
        }
      }
    }

    stage ('Build') {
      steps {
        nodejs(nodeJSInstallationName: 'nodejs 8.9.4') {
          sh 'echo "Build application..."'
          sh 'npm run build'
          sh 'echo "Build application successfully."'
          sh 'ls -al'
        }
        script {
          stash includes: 'build/', name: 'build'
        }
      }
    }

    stage ('Create docker images') {
      agent any
      steps {
        script {
          unstash 'build'
        }
        sh '''
          ls -al
          echo "Starting to build docker image"
          docker build -t pick-color:v1 -f docker/Dockerfile.no_build .

        '''
      }
    }
  }
}