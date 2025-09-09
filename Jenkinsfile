pipeline {
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

                    REM Clean old files
                    if exist site.zip del site.zip
                    if exist site rmdir /s /q site

                    REM Make new site folder
                    mkdir site

                    REM Copy only project files (avoid cyclic copy)
                    xcopy *.html site\\ /Y
                    xcopy *.css site\\ /Y
                    xcopy *.js site\\ /Y
                    xcopy assets site\\assets\\ /E /I /Y

                    REM Compress into zip
                    powershell -Command "Compress-Archive -Path site\\* -DestinationPath site.zip -Force"

                    echo 🚀 Deploying to Netlify...
                    curl -H "Authorization: Bearer %NETLIFY_AUTH_TOKEN%" ^
                         -H "Content-Type: application/zip" ^
                         --data-binary "@site.zip" ^
                         https://api.netlify.com/api/v1/sites/%SITE_ID%/deploys

                    echo ✅ Deployment Completed!
                '''
            }
        }
    }
}
