pipeline {
     agent any
     stages {
          stage ("printenv")
{
steps {
sh 'env'
sh 'pwd' }
}
          stage ("gitcheckout") {
              steps { 
sh 'cd /tmp'       
sh 'mvn clean validate;
                  junit '**/target/surefire-reports/TEST-*.xml'
                  archive 'target/*.war'
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
stage('buildimage'){
agent { docker {
 label 'slave-1'
 reuseNode true
 image 'docker:latest'
 args '-u root -v pwd:/tmp -v /var/run/docker.sock:/var/run/docker.sock'
}
}
steps{
script {
withDockerRegistry([credentialsId: 'dockerlogin', url: ""])
{
sh 'cd /tmp'
sh 'docker build -t hello-world-image:"$BUILD_NUMBER" .'
sh 'docker tag hello-world-image:"$BUILD_NUMBER" jayaprakashsaranya/helloworld:"$BUILD_NUMBER"'
sh 'docker push jayaprakashsaranya/helloworld:"$BUILD_NUMBER"'
}
          }
}
          
     }
}
}
