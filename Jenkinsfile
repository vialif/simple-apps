pipeline {
    agent { label 'devops1-vialif'}
    tools {nodejs "NodeJS 18.16.0"}
    
    stages {
        stage ('Git Clone SCM'){
            steps {
                git branch: 'main', url: 'https://github.com/vialif/simple-apps.git'
            }
        }
        stage ('Unit Testing') {
            steps {
                sh '''
                npm install
                npm test'''
            }
        }
         stage('Code Review') {
            steps {
                sh '''
                sonar-scanner \
                -Dsonar.projectKey=simple-apps \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.23.7.21:9000 \
                -Dsonar.login=sqp_ce3c0e802a25bdf6d824d822259d7050c0b3c84d'''
            }
         }
         stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
        stage ('Push Image') {
            steps {
                sh '''
                docker build -t vialif37/simple-apps-pipeline-apps
                docker push viailf37/simple-apps-pipelines-apps
                docker images prune -a -f
                '''
        }
    }
}