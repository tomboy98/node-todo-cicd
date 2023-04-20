pipeline{
agent { label 'dev-agent'}
stages{
    stage('Code'){
        steps{
            git url:'https://github.com/tomboy98/node-todo-cicd.git',branch:'master'
        }
    }
    stage('Build and Test'){
        steps{
           sh 'docker build . -t ashwathy/node-todo-app-cicd:latest'
        }
    }
    stage('Login and push image'){
        steps{
           echo "Logging in to docker hub and pushing image"
           withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')])
           { sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}" 
             sh "docker push ashwathy/node-todo-app-cicd:latest"
           }
        }
    }
    stage('Deploy'){
        steps{
            sh 'docker-compose down && docker-compose up -d'
        }
    }
    
}
}
