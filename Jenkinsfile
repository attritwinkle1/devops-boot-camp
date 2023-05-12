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
      stage ('Install sonarqube cli')
           sh 'wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip'
           sh 'unzip -o -q sonar-scanner.zip'
           sh 'sudo rm -rf /opt/sonar-scanner'
           sh 'sudo sh -c \'echo "#/bin/bash \nexport PATH=\\\"$PATH:/opt/sonar-scanner/bin\\\"" > /etc/profile.d/sonar-scanner.sh\''
           sh 'chmod +x /opt/sonar-scanner/bin/sonar-scanner'
           sh '. /etc/profile.d/sonar-scanner.sh'
               }
            }            
       stage ('Analyzing Code Quality') {
         steps {
           sh '/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=attritwinkle1_devops-boot-camp -Dsonar.organization=attritwinkle1 -Dsonar.qualitygate.wait=true -Dsonar.qualitygate.timeout=300 -Dsonar.sources=src/main/java/ -Dsonar.java.binaries=target/classes -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=117c53381d188e24519da84ec900bd2e7b1acbb3'
               }
             }
     stage ('Deploying Application Using Ansible') {
	      steps {
		sh 'export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook --private-key=/home/ubuntu/.ssh/vm-instance-key.pem -i host_inventory deploy-artifact.yml'
		}
	}
 }
}

        
