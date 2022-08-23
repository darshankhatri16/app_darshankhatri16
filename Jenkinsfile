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

   stage('Kubernetes deployment') {
      steps{
          withKubeConfig([credentialsId: 'kubernetes-config']) {
          sh 'gcloud auth activate-service-account khatridarshan16-gmail-com@nagp-devops-assignment-2022.iam.gserviceaccount.com --key-file=${HOME}/nagp-devops-assignment-2022-c9fe40268270.json --project=nagp-devops-assignment-2022'
          sh 'gcloud container clusters get-credentials jenkins-cd --zone us-east1-d'
          sh 'gcloud builds submit --tag us-east1-docker.pkg.dev/jenkins-cd/nagp-devops-home-assignment-2022/nagp-devops-home-assignment-2022-gke .'
          sh 'kubectl apply -f k8s/'
        }
      }
    }
  }
}
