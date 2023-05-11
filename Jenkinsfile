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
          // sh 'mvn test'
               }
           }
      stage ('Creating package') {
         steps {
           sh 'mvn package -DskipTests=true'
         }
      }
      stage ('Deploying Application using Ansible') {
         steps {
           sh ‘export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook --private-key=/home/ubuntu/.ssh/vm-instance-key.pem -i host_inventory deploy_artifact.yml’
                  }
             }
        }
      }

        
