pipeline {

  agent any

  environment {

      GCR_CREDENTIALS_ID = 'gareth123' // The ID you provided in Jenkins credentials

      IMAGE_NAME = 'test-build-1'

      GCR_URL = 'gcr.io/lbg-mea-18/week-3-project-gc'

  }

  stages {

      stage('Build and Push to GCR') {

  steps {

      script {

          // Authenticate with Google Cloud

          withCredentials([file(credentialsId: GCR_CREDENTIALS_ID, variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {

              sh 'gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS'

          }

          // Configure Docker to use gcloud as a credential helper

          sh 'gcloud auth configure-docker --quiet'

          // Build the Docker image

          sh "docker build -t ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER} ."

          // Push the Docker image to GCR

          sh "docker push ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER}"

      }

  }

      }

  }

}
