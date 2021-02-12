pipeline {
     agent {label 'slave-1'}
     stages {
          stage ("printenv")
{
steps {
sh 'echo env' }
}
          stage ("gitcheckout")
          {
            agent { docker {
            image 'maven:3-alpine'
            args '-v /home/automation/workspace/hello-world-dev-job_feature-dev@2/:/root/.m2'
          }
}
              steps {
                  git branch: 'feature-dev', credentialsId: 'alpha-github-access', url: 'https://github.com/jp-git1986/hello-world-greeting.git'
                  sh 'mvn clean verify -DskipITs=true';
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.war'
}
              }
         stage('Static Code Analysis'){
       agent { docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
          }
}
steps{
    sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://34.123.29.142:9000 -Dsonar.login=0308c497c6e118600ab06ce892caffef17c12c0e -Dsonar.projectName=hello-world-greetings -Dsonar.projectKey=hello-world-greetings -Dsonar.projectVersion=$BUILD_NUMBER';
}
}

          }
          
     }

