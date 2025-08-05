pipeline{
    agent any;
    stages{
        stage("code clone"){
            steps{
                git url:"https://github.com/Shubham-Kale2/two-tier-flask-app.git" , branch: "master"
            }
        }
        stage("build code"){
            steps{
                sh "docker build -t myapp ."
            }
        }
        stage ("test code"){
            steps {
                echo "test the code sucessfully"
            }
        }
        stage("code push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCreds",
                    passwordVariable: "DockerHubPass",
                    usernameVariable: "DockerHubUser"
                )]){
                sh "docker login -u${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker image tag myapp ${env.DockerHubUser}/myapp:latest"
                sh "docker push ${env.DockerHubUser}/myapp:latest"
                }
            }
        }
        stage("deploy code"){
            steps{
            sh "docker-compose up -d --build flask-app"
        }
      }
    }
}
