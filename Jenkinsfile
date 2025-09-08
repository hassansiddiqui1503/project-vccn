pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        SITE_ID = 'pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        SITE_ID = 'ce29c8dc-6153-4408-9d15-9091f108ce99'
    }

    stages {
        stage('Deploy to Netlify') {
            steps {
                bat '''
                    echo 🚀 Preparing site for deployment...

                    REM Delete old files if exist
                    if exist site.zip del site.zip
                    if exist site rmdir /s /q site

                    REM Create folder
                    mkdir site

                    REM Copy all project files (HTML, CSS, JS)
                    copy *.html site\\
                    copy *.css site\\
                    copy *.js site\\

                    REM Compress files directly (no nested folder)
                    powershell Compress-Archive -Path site\\* -DestinationPath site.zip -Force

                    echo 🚀 Deploying to Netlify...
                    curl -H "Authorization: Bearer %NETLIFY_AUTH_TOKEN%" ^
                         -H "Content-Type: application/zip" ^
                         --data-binary "@site.zip" ^
                         https://api.netlify.com/api/v1/sites/%SITE_ID%/deploys
                '''
            }
        }
    }
}
'
    }

    stages {
        stage('Deploy to Netlify') {
            steps {
                bat '''
                    echo 🚀 Preparing site for deployment...

                    REM Delete old files if exist
                    if exist site.zip del site.zip
                    if exist site rmdir /s /q site

                    REM Create folder
                    mkdir site

                    REM Copy all project files (HTML, CSS, JS)
                    copy *.html site\\
                    copy *.css site\\
                    copy *.js site\\

                    REM Compress files directly (no nested folder)
                    powershell Compress-Archive -Path site\\* -DestinationPath site.zip -Force

                    echo 🚀 Deploying to Netlify...
                    curl -H "Authorization: Bearer %NETLIFY_AUTH_TOKEN%" ^
                         -H "Content-Type: application/zip" ^
                         --data-binary "@site.zip" ^
                         https://api.netlify.com/api/v1/sites/%SITE_ID%/deploys
                '''
            }
        }
    }
}
