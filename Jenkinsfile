pipeline {
    agent {
        dockerContainer {
            image 'xerksez/obraz:latest'
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
         stage('Run web server') {
            steps {
                // Skopiuj plik index.html do katalogu roboczego w kontenerze
                sh 'cp helloworld.html /app'

                // Uruchom prosty serwer HTTP do serwowania plików statycznych (index.html)
                script {
                    docker.image('node:latest').inside('-p 8080:8080') {
                        sh 'npx http-server -p 8080 /app'
                    }
                }
            }
        }
    }
}

