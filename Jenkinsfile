pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        SITE_ID = '9664e49a-5d63-4e18-8e82-4c51502ed9f6'
    }

    stages {
        stage('Checkout Repo') {
            steps {
                checkout scm
            }
        }

        stage('Deploy index.html to Netlify') {
            steps {
                bat '''
                    echo 🚀 Deploying index.html directly to Netlify...

                    REM Use Netlify CLI for correct deploy
                    npm install -g netlify-cli

                    netlify deploy --prod ^
                        --dir=. ^
                        --site=%SITE_ID% ^
                        --auth=%NETLIFY_AUTH_TOKEN%

                    echo ✅ Deployment completed.
                '''
            }
        }
    }
}
