pipeline {
     agent any
     stages {
          stage ("gitcheckout")
          {
            agent docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
          }
              steps {
                  git branch: 'feature-dev', credentialsId: 'alpha-github-access', url: 'https://github.com/jp-git1986/hello-world-greeting.git'
                  sh 'mvn clean verify -DskipITs=true';
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.war'
}
              }

          }
          
     }

