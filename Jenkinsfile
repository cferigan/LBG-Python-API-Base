pipeline {

    agent any

    environment {

        GCR_CREDENTIALS_ID = 'gcp' // The ID you provided in Jenkins credentials

        IMAGE_NAME = 'connor-python-api'

        GCR_URL = 'gcr.io/lbg-mea-15'

    }

    stages {

        stage('Build and Push to GCR') {

    steps {

        script {

            withCredentials([file(credentialsId: GCR_CREDENTIALS_ID, variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {

                sh 'gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS'

            }


            sh 'gcloud auth configure-docker --quiet'


            sh "docker build -t ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER} ."

            sh "docker push ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER}"

        }

    }

        }

    }

}
        stage('Build') {
            steps {
                sh '''
                sh "setup.sh"
                '''
           }
        }
        stage('Deploy') {
            steps {
                sh '''
                
                '''
            }
        }
