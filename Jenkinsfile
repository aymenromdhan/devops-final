pipeline {
    agent any
environment {
    		DOCKERHUB_CREDENTIALS=credentials('projet')
    	}
    stages {
        stage('Récupération du code de la branche') {
            steps {
                git branch: 'YoussefKLILA-5NIDS-G3',
                url: 'https://github.com/BahaEddineKsib/5NIDS2-G3-PROJECT2.git'
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
            sh "mvn sonar:sonar -Dsonar.login=e10380a5a72c7aa2d861f345638de9e85dee25ad"
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
                               sh 'docker build -t youssefklila-5nids2-g3 .'
                           }
               }        
                stage('DOCKERHUB') {
                          steps {
                              sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                              sh 'docker tag youssefklila-5nids2-g3 josefinne/youssef-5nids2-g3:1.0.0'
                              sh 'docker push josefinne/youssef-5nids2-g3:1.0.0'
                          }
                      }
               stage('Docker Compose') {
                                  steps {
                                      sh 'docker compose up -d'
                                  }
                      }
    }
}
