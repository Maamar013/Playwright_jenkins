pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            // 'playwright/chromium:playwright-1.56.1'
            args '--user=root --entrypoint=""'
        }
    }
    parameters{
        choice(name: 'Navigateur', choices: ['chromium','webkit', 'firefox'], description: ('selectionner un navigateur pour le test'))
    }

    stages {
        stage('Préparation du projet') {
            steps {
                sh 'node -v'
                

                // Installer git
                //sh 'apt-get update && apt-get install -y git'

                // Supprimer l'ancien repo si présent
                sh 'rm -rf repo'

                // Cloner le repo
                sh 'git clone https://github.com/QP16CAP/PlaywrightJENKINS.git repo'

                // Installer les dépendances et navigateurs Playwright
                dir('repo') {
                    //sh 'npm install'
                    //sh 'npx playwright install'
                    sh 'npm ci'
                    sh 'npx playwright --version'

                    sh'npx playwright --reporter=allure-playwright'
                }
            }
        }

        stage('Exécution des tests Playwright') {
            steps {
                dir('repo') {
                    script { if (params.Navigateur == 'chromium')
                    {//sh 'npx playwright test --project=chromium --grep @smoke'
                    sh'npx playwright test --project=chromium --grep @smoke --reporter=allure-playwright'
                    stash name: 'allure-results', includes: 'allure-results/*'
                   
                    }
                    else {echo 'veuillez choisir le bon navigateur'}}
                }
            }
        }



         stage('Lancer jenkinsfile2') {
            when {
                expression {
                    currentBuild.currentResult == 'SUCCESS'
                }
            }
            steps {
                sh 'rm -rf allure-results/*'
                unstash 'allure-results'
                archiveArtifacts 'allure-results/*'
                allure includeProperties: false, jdk: '', results: [[path: 'allure-results/']]
                //build job: 'Jenkinsfile2', wait: true
            }
        }
        
    }
}

//lancer allure report
//npx playwright test --project=chromium --grep @smoke --reporter=list,allure-playwright
