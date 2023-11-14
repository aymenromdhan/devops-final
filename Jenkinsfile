pipeline {
    agent any

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

         stage('mvn deploy'){
            steps {
                sh "mvn deploy"
            }
         }

    }
}
