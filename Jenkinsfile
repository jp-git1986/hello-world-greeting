pipeline {
     agent any
     stages {
          stage ("gitcheckout")
          {
              agent any
              steps {
                  git branch: 'feature-dev', credentialsId: 'alpha-github-access', url: 'https://github.com/jp-git1986/project-alpha.git'
                  sh 'mvn clean validate
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.jar'
}
              }

          }
          
     }

