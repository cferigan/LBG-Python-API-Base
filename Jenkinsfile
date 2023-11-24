pipeline {

    agent any

    environment {

        GCR_CREDENTIALS_ID = 'gcp' 

        IMAGE_NAME = 'connor-python-api'

        GCR_URL = 'gcr.io/lbg-mea-15'

        PROJECT_ID = 'lbg-mea-15'

        CLUSTER_NAME = 'connor-cluster'

        LOCATION = 'europe-west2-c'

        CREDENTIALS_ID = 'd830c937-605d-450d-94fb-66a44eb18fde'
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
 stage('Deploy to GKE') {

            steps {

                script {

                 

                    step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'kubernetes/deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])

                }

            }

        }

    }

}
}
