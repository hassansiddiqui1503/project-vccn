pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')  
        SITE_ID = 'ce29c8dc-6153-4408-9d15-9091f108ce99'
    }

    stages {
        stage('Checkout Repo') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Deployment') {
            steps {
                bat '''
                    echo 🚀 Preparing deployment zip...

                    REM Delete old zip if exists
                    if exist site.zip del site.zip

                    REM Compress ONLY public folder (where index.html is)
                    powershell -Command "Compress-Archive -Path public\\* -DestinationPath site.zip -Force"

                    echo ✅ Deployment package ready
                '''
            }
        }

        stage('Deploy to Netlify') {
            steps {
                bat '''
                    echo 🚀 Deploying site.zip to Netlify...

                    curl -k -H "Authorization: Bearer %NETLIFY_AUTH_TOKEN%" ^
                         -H "Content-Type: application/zip" ^
                         --data-binary "@site.zip" ^
                         https://api.netlify.com/api/v1/sites/%SITE_ID%/deploys

                    echo ✅ Deployment completed.
                '''
            }
        }
    }
}
