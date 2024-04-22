pipeline {
    agent { label 'agent' }

    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/jjh920/nodejs-app.git', branch: 'main'
            }
        }
        stage('docker build & deploy') {
            steps {
		sh 'IMAGE_NAME=jjh920/nodejsapp docker compose build'
            }
        }
	stage('docker hub push') {
            steps {
                sh '''
 		   docker login -u jjh920 -p wh017rlawh@@
                   docker push jjh920/nodejsapp
		'''
            }
        }
	stage('microk8s run pod') {
            steps {
                sh ' microk8s kubectl run app1 --image=jjh920/nodejsapp '
            }
        }
    }
}
