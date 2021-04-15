pipeline{
        agent any
        environment {
                DB_PASSWORD = credentials("DB_PASSWORD")
        }
        stages{
                stage('Clone Directory'){
                steps{
                        sh "rm -rf chaperootodo_client"
                        sh "git clone https://gitlab.com/qacdevops/chaperootodo_client.git"
                }
            }
            stage('Install Docker and Docker-Compose'){
                steps{
                        sh "curl https://get.docker.com | sudo bash"
                        sh 'sudo curl -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                        sh "sudo chmod +x /usr/local/bin/docker-compose"
                }
            }
             stage('Deploy'){
                steps{
                        sh "cd chaperootodo_client && sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d"
                }
            }
        }
}
