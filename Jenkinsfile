pipeline { 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: ' https://github.com/malfahemi/8.2CDevSecOps.git' 
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
        stage('SonarCloud Analysis') {
  steps {
    withCredentials([string(credentialsId: '8.1C', variable: 'SONAR_TOKEN')]) {
      bat '''
        set "SCANNER_HOME=C:\\Users\\malfa\\SIT\\sonar-scanner-7.2.0.5079-windows-x64\"
        set "PATH=%SCANNER_HOME%\\bin;%PATH%"
        sonar-scanner -D"sonar.token=%SONAR_TOKEN%"
      '''
    }
  }
}
}
}