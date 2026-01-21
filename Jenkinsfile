pipeline{

    agent {
        //recuperer l'image docker officielle de playwright
        docker{
            //specifier l'image
            image 'playwright/chromium:playwright-1.56.1'
            //donner les droits root
            args '--user=root --entrypoint=""'
        }
    }
    stages{
        //clonner le projet
        stage('clonner le projet'){
            steps{
                //creer supprimer le repo
                sh 'apt-get update && apt-get install -y git'
                sh "rm -rf repo"
           
                //cloner le repo
                sh "git clone https://github.com/Maamar013/Playwright_jenkins.git repo"
            
            //verifier la version de nodejs et playwright
             dir('repo'){
                    //installer les dependances
                sh "npm install"
                sh "npx playwright test --project=chromium"
                }    
                sh "node --version"
                sh "npx playwright --version"
            
            
                //se positionner dans le dossier du projet
               
            }


            






        }
    }
}

    //git clone
    //npm install
    //npx playwright test



   /* pipeline {
    agent {
        docker {
            image 'playwright/chromium:playwright-1.56.1'
            args '--user=root'
        }
    }

    stages {
        stage('Setup & Tests') {
            steps {
                // Vérifier Node et npm
                sh 'node --version'
                sh 'npm --version'

                // Installer les dépendances (Playwright compris)
                sh 'npm install'
                sh 'npx playwright install'

                // Vérifier Playwright
                sh 'npx playwright --version'

                // Lancer les tests
                sh 'npx playwright test --project=chromium'
            }
        }
    }
}*/
