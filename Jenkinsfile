pipeline {
    agent any
environment {
    		DOCKERHUB_CREDENTIALS=credentials('projet')
    	}
    stages {
        stage('Récupération du code de la branche') {
            steps {
                git branch: 'aymen',
                url: 'https://github.com/aymenromdhan/devops-final.git'
            }
        }
   
    
      stage('Nettoyage et compilation avec Maven') {
            steps {
                // Étape de nettoyage du projet
                sh "mvn clean"

                // Étape de compilation du projet
                sh "mvn compile"
                // Etape de sonar
            }
        }
        stage('MVN SONARQUBE'){
        steps {
            sh "mvn sonar:sonar -Dsonar.login=sqa_5bf75a8250ef31838fae8ee495ebc48dffe8c2c1"
        }
        }
stage("mockito"){
            steps {
                sh 'mvn -Dtest=KaddemApplicationTests test'
            }
        }
         stage('mvn deploy'){
            steps {
                sh "mvn deploy"
            }
         }
        stage('Docker Image') {
                           steps {
                               sh 'docker build -t aymen-5nids2-g0 .'
                           }
               }        
                stage('DOCKERHUB') {
                          steps {
                              sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                              sh 'docker tag aymen-5nids2-g0 aymen002/ay-5nids2-g0:1.0.0'
                              sh 'docker push aymen002/ay-5nids2-g0:1.0.0'
                          }
                      }
               stage('Docker Compose') {
                                  steps {
                                      sh 'docker compose up -d'
                                  }
                      }

    }
}
