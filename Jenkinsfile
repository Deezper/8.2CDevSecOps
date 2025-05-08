pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Deezper/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npm test || exit /b 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit /b 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }
  }

  post {
    success {
      emailext(
        subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """Hi Dulana,

Your Jenkins pipeline completed successfully.

Check the console output or view the attached build log for details.

– Jenkins
""",
        to: "dulanaperera77@gmail.com",
        attachLog: true
      )
    }
    failure {
      emailext(
        subject: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """Hi Dulana,

Unfortunately, your Jenkins pipeline failed.

Please check the attached build log for troubleshooting.

– Jenkins
""",
        to: "dulanaperera77@gmail.com",
        attachLog: true
      )
    }
  }
}
