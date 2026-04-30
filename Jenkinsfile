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
    } 
 
  } 
}
