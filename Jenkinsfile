pipeline {
    agent 'any'
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }
      stages {
        stage('vcs') {
            steps{
                git branch: 'main',
                url: 'https://github.com/manohargatla/jenkins-k8s-deploy.git'
            }
            
        }
        stage('build image') {
            steps {
                sh 'docker image build -t nopcommerce:1.0 .'
                sh 'docker tag nopcommerce:1.0 manugatla/nopcommerce:1.0'
                sh 'docker push manugatla/nopcommerce:1.0'
            }
        }
        stage('deploying application') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl get po'
                sh 'kubectl get svc'
            }
        }
    }
}