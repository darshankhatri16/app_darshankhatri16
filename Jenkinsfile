pipeline {
  agent any
    
  tools {nodejs "nodejs"}
    
  stages {
        
    stage('Git') {
      steps {
        git branch: 'develop', credentialsId: 'Git_Credentials', url: 'https://github.com/darshankhatri16/app_darshankhatri16'
      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

   stage('Test case execution') {
      steps {
         sh 'npm test'
      }
    }

    stage('Kubernetes deployment') {
      steps {
         withKubeConfig([credentialsId: 'kubernetes-config']) {
          sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
          sh 'chmod u+x ./kubectl'  
          sh './kubectl version'
      }
    }
    }
  }
}
