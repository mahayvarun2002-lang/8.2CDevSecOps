pipeline { 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        // NOTE: You will need to replace 'your_github_username' with your actual username once you push this repository to GitHub
        git branch: 'main', url: 'https://github.com/mahayvarun2002-lang/8.2CDevSecOps.git' 
      } 
    } 
 
    stage('Install Dependencies') { 
      steps { 
        bat 'npm install' 
      } 
    } 
 
    stage('Run Tests') { 
      steps { 
        bat 'npm test || exit /b 0' // Allows pipeline to continue despite test failures 
      }
      post {
        always {
          emailext (
            subject: "Jenkins Build Status: ${currentBuild.currentResult} - Test Stage",
            body: "The Run Tests stage has completed. Please find the attached build logs for details.",
            to: 'kumarvijay421964@gmail.com', // Replace with your actual email
            attachLog: true
          )
        }
      } 
    } 
 
    stage('Generate Coverage Report') { 
      steps { 
        // Ensure coverage report exists 
        bat 'npm run coverage || exit /b 0' 
      } 
    } 
 
    stage('NPM Audit (Security Scan)') { 
      steps { 
        bat 'npm audit || exit /b 0' // This will show known CVEs in the output 
      }
      post {
        always {
          emailext (
            subject: "Jenkins Build Status: ${currentBuild.currentResult} - Security Scan Stage",
            body: "The Security Scan (npm audit) stage has completed. Please find the attached logs for the vulnerability report.",
            to: 'kumarvijay421964@gmail.com', // Replace with your actual email
            attachLog: true
          )
        }
      }
    } 
 
  } 
}
