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
            label 'slave-1'
            image 'maven:3-alpine'
            args '-u root -v pwd:/tmp' 
          }
}
              steps {
lock ('slave-1') {
sh 'cd /tmp'       
sh 'mvn clean verify -DskipITs=true';
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.war'
}
}
              }

         stage('Static Code Analysis'){
       agent { docker {
            label 'slave-1'
            reuseNode true
            image 'maven:3-alpine'
            args '-u root -v pwd:/tmp'
          }}
options { skipDefaultCheckout() }
steps{
    sh 'cd /tmp'
    sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://104.197.208.234:9000 -Dsonar.login=0308c497c6e118600ab06ce892caffef17c12c0e -Dsonar.projectName=hello-world-greetings -Dsonar.projectKey=hello-world-greetings -Dsonar.projectVersion=$BUILD_NUMBER';

}
}

          }
          
     }

