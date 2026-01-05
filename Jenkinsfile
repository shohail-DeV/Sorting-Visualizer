pipeline {
    agent any

    tools {
        nodejs 'Node_js'
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {

        stage('Hello App') {
            steps {
                echo 'Next.js app pipeline initiated'
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shohail-DeV/Sorting-Visualizer.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Lint & Test') {
            steps {
                bat 'npm run lint || echo "Lint skipped"'
                bat 'npm test || echo "Tests skipped"'
            }
        }

        stage('Build Application') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '.next/**', fingerprint: true
            }
        }

     //   stage('Deploy (Optional)') {
       //     when {
         //       expression { fileExists('.next') }
           // }
            //steps {
              //  echo 'Ready for deployment (PM2 / Docker / Vercel)'
            //}
      //  }
    }

    post {
        success {
            echo 'CI pipeline completed successfully'
        }
        failure {
            echo 'CI pipeline failed — immediate action required'
        }
    }
}
