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
              sh "sed -i 's/nagp-devops-home-assignment-2022-gke:latest/nagp-devops-home-assignment-2022-gke:latest/g' k8s/deployment.yaml"
              step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
      }
    }
  }
}
