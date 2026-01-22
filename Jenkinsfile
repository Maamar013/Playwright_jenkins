pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            args '--user=root'
        }
    }

    parameters {
        choice(
            name: 'Navigateur',
            choices: ['chromium','webkit','firefox'],
            description: 'Sélectionner un navigateur pour le test'
        )
    }

    stages {

        stage('Préparation du projet') {
            steps {
                sh 'node -v'
                sh 'rm -rf repo'
                sh 'git clone https://github.com/QP16CAP/PlaywrightJENKINS.git repo'

                dir('repo') {
                    sh 'npm ci'
                    sh 'npx playwright --version'
                }
            }
        }

        stage('Exécution des tests SMOKE') {
            when {
                expression { params.Navigateur == 'chromium' }
            }
            steps {
                dir('repo') {
                    sh 'npx playwright test --project=chromium --grep @smoke --reporter=allure-playwright'
                }
            }
        }
    }

    post {
        always {
            dir('repo') {
                archiveArtifacts artifacts: 'allure-results/**', fingerprint: true
                allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
            }
        }
    }
}
