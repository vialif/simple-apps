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

    }
}