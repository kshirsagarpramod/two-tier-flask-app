pipeline{
    
    agent any;
    
    stages{
        stage("Code Clone"){
            steps{
               git url: "https://github.com/kshirsagarpramod/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build"){
            steps{
               sh "docker build -t my-two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "Developer/TEster test loha ke dega"
            }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                        
                )]){
                        
                    sh "docker login -u  ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag my-two-tier-flask-app ${env.dockerHUbUser}/my-two-tier-flask-app"
                    sh "docker push ${env.dockerHubUser}/my-two-tier-flask-app:latest"
            
                    }
                }
        }
        stage("Deploy"){
            steps{
              sh "docker compose up -d --build flask-app"
            }
        }
    }
}
