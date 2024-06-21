pipeline {
    agent {
        dockerContainer {
            image 'xerksez/obraz:latest'
            args '-u root' 
             args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Pobieranie kodu') {
            steps {
                git 'https://github.com/xerksez/appjenkinsgit'
            }
        }
        stage('Instalacja i uruchomienie aplikacji') {
            steps {

                sh 'npm install'
                sh 'npm start'
            }
        }
        stage('Testy jednostkowe') {
            steps {
                sh 'npm test'
                junit 'results/**/*.xml'
            }
        }
        stage('ESLint') {
            steps {
                sh 'eslint .'
            }
        }
    }
}
