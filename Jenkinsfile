cd ..
cat > Jenkinsfile << 'EOF'
pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { git url: 'https://github.com/your-org/liquibase-oracle-demo.git', credentialsId: 'git-creds' }
    }
    stage('Liquibase Update') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'oracle-yiptran', usernameVariable: 'DB_USER', passwordVariable: 'DB_PASS')]) {
          bat """
            cd %WORKSPACE%\\liquibase
            liquibase ^
              --driver=oracle.jdbc.OracleDriver ^
              --url="jdbc:oracle:thin:@45.114.142.57:1524/YIPDV" ^
              --changeLogFile=change.xml ^
              --username=%DB_USER% --password=%DB_PASS% ^
              update
          """
        }
      }
    }
  }
}
EOF