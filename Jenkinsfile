pipeline {
     agent any
     stages {
          stage ("gitcheckout")
          {
              agent {label 'build-slave'}
              steps {
                  git branch: 'feature-dev', credentialsId: 'alpha-github-access', url: 'https://github.com/jp-git1986/project-alpha.git'
                  sh 'mvn clean verify -DskipITs=true';
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.jar'
}
              }

          }
          
     }

