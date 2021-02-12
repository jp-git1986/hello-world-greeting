pipeline {
     agent {label 'slave-1'}
     stages {
          stage ("printenv")
{
steps {
sh 'env'
sh 'pwd' }
}
          stage ("gitcheckout")
          {
            agent { docker {
            image 'maven:3-alpine'
            args '-u root -v pwd:/tmp' 
          }
}
              steps {
lock ('slave-1') {
                 //git branch: 'feature-dev', credentialsId: 'alpha-github-access', url: 'https://github.com/jp-git1986/hello-world-greeting.git'
sh 'cd /tmp'       
sh 'mvn clean verify -DskipITs=true';
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.war'
}
}
              }

         stage('Static Code Analysis'){
       agent { docker {
            image 'maven:3-alpine'
            args '-u root -v pwd:/tmp'
          }
}
steps{
lock ('slave-1') {
    sh 'cd /tmp'
    sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://34.123.29.142:9000 -Dsonar.login=0308c497c6e118600ab06ce892caffef17c12c0e -Dsonar.projectName=hello-world-greetings -Dsonar.projectKey=hello-world-greetings -Dsonar.projectVersion=$BUILD_NUMBER';
}
}
}

          }
          
     }

