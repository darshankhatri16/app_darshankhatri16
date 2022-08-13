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

    stage('SonarQube Analysis') {
    steps {
       script {
       def scannerHome = tool 'SonarQubeScanner';
           withSonarQubeEnv("Test_Sonar") {
           sh "${tool("SonarQubeScanner")}/bin/sonar-scanner \
           -Dsonar.projectKey=sonar-darshankhatri16 \
           -Dsonar.sources=. \
           -Dsonar.host.url=http://localhost:9000 \
           -Dsonar.login=4d3899686a9ec7b0aef9fe5e79b6824b3d5fee21"
               }
           }
       }
   }
  }
}
