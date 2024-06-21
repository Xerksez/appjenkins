pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pobranie kodu z repozytorium GitHub
                git 'https://github.com/Xerksez/appjenkins.git'
            }
        }

        stage('Build and Run') {
            environment {
                DOCKER_IMAGE = 'jenkins-blueocean:custom' // Nazwa twojego obrazu Dockera z Jenkinsem i zainstalowanymi narzędziami
            }
            steps {
                // Kompilacja (instalacja zależności) i uruchomienie aplikacji
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'npm install' // Instalacja zależności
                        sh 'npm start &' // Uruchomienie aplikacji w tle
                    }
                }
            }
        }

        stage('Unit Tests') {
            environment {
                DOCKER_IMAGE = 'jenkins-blueocean:custom'
            }
            steps {
                // Wykonanie testów jednostkowych wraz z raportowaniem
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'npm test' // Wykonanie testów jednostkowych
                        junit '**/test-results/*.xml' // Raportowanie wyników testów
                    }
                }
            }
        }

        stage('ESLint Check') {
            environment {
                DOCKER_IMAGE = 'jenkins-blueocean:custom'
            }
            steps {
                // Sprawdzanie kodu za pomocą ESLint
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'npm run lint' // Uruchomienie ESLint
                    }
                }
            }
        }
    }
}
