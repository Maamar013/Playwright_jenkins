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
                sh "rm -rf repo"
            }
            steps{
                //cloner le repo
                sh "git clone https://github.com/Maamar013/Playwright_jenkins.git repo"
            }
            //verifier la version de nodejs et playwright
            steps{
                sh "node --version"
                sh "npx playwright --version"
            }
            steps{
                //se positionner dans le dossier du projet
                dir('repo'){
                    //installer les dependances
                    sh "npm install"
                    sh "npx playwright test --project=chromium"
                }
            }


            






        }
    }
}

    //git clone
    //npm install
    //npx playwright test