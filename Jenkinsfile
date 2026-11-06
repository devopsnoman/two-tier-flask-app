pipeline{
    agent { label 'dev' };
    stages{
        stage('code clone'){
            steps{
                git url:"https://github.com/devopsnoman/two-tier-flask-app.git", branch: "master"
            }
        }
        stage('build'){
            steps{
                sh "docker build -t nomandevops1/two-tier-flask-app ."
            }
        }
        stage('test'){
            steps{
                echo ".."
            }
        }
        stage('docker hub push'){
            steps{
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                        )
                    ]){
                        sh ' echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    }
            }
        }
        
        stage('deploy'){
            steps{
                sh "docker compose up -d --build"
            }
        }
    }
}
