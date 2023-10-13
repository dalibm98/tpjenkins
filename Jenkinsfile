pipeline {
    agent any 
    tools { 
        maven 'maven'
        nodejs 'NodeJS'
    }
    stages {
        stage ("Clean up"){
            steps {
                deleteDir()
            }
        }
        stage ("Clone repo"){
            steps {
                sh "git clone https://github.com/dalibm98/tpjenkins.git"
            }
        }
        stage ("Generate backend image") {
              steps {
                   dir("tpjenkins/springboot/app"){
                       
                      sh "mvn clean install"
                      sh "docker build -t app ."
                  }                
              }
          }

       stage("Generate front image") {
            steps {
                dir("tpjenkins/angular-app") {
                    sh "npm install"
                    sh "npm run build"
                    sh "docker build -t frontapp ."
                }
            }
        }
        stage ("Run docker compose") {
            steps {
                 dir("tpjenkins"){
                    sh " docker compose up -d"
                }                
            }
        }
    }
}
