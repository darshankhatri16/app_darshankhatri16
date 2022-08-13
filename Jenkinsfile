pipeline {
  agent any
    
  tools {nodejs "node"}
    
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
  }
}
