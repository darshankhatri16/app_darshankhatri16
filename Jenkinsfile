pipeline {
  agent any

  environment {
        PROJECT_ID = 'nagp-workshop-kubernetes'
        CLUSTER_NAME = 'nagp-kuberetes-batch'
        LOCATION = 'us-central1'
        CREDENTIALS_ID = 'kubernetes-config'
    }
    
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
