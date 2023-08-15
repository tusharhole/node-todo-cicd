pipeline{
    agent{ label 'dev-agent'}
    
        stages{
            stage('code'){
                steps {
                    git url : 'https://github.com/tusharhole/node-todo-cicd.git', branch: 'master'
                    
            }
        }
           stage('build and test'){
                steps {
                   sh'docker build . -t tusharh/node-todo-app'
                    
            }
        }
        stage('login & Push image'){
                steps {
                   echo "login in dockerhub and pushing image"
                  withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'hole', usernameVariable: 'tushar')]) {
                        sh "docker login -u ${env.tushar} -p ${env.hole}"
                        sh "docker push tusharh/node-todo-app "
                }
                    
            }
        }
           stage('Deploy'){
                steps {
                   sh 'docker-compose down && docker-compose up -d'
                }   
            
        }
         
    }
}
