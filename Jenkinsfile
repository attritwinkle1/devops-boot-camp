pipeline {
   agent { label "agentfarm" }
   stages {
     stage ('Installing maven') {
        steps {
           sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
           sh 'sudo apt-get install -y wget tree unzip maven'
              }
           }
      stage ('Compiling and running test cases') {
         steps {
           sh 'mvn clean'
           sh 'mvn compile'
           sh 'mvn test'
               }
           }
      stage ('Creating package') {
         steps {
           sh 'mvn package'
               }
           }
      stage ('Deploying Application') {
         steps {
           script{
             withenv(['JENKINS_NODE_COOKIE=dontkill']) {
                sh 'nohup java -jar ./target/springboot-bootcamp-0.0.1-SNAPSHOT.jar &'
                    }
              }
      }

   }
        
