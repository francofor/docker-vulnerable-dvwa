pipeline {
 agent any

 stages {
   stage("Preparation") { 
     steps {
       git 'https://github.com/francofor/docker-vulnerable-dvwa'
//       sleep 1
     }
   }
   stage("First Code analysis") {
       steps {
sh '''cd /home/franco/wap; java -jar wap.jar -a -s -all -p /var/lib/jenkins/workspace/pec4/dvwa/
'''
       }
   }
   stage("Second Code analysis") {
       steps {
sh '''cd /home/franco/phpcs-security-audit-master; ./vendor/bin/phpcs --standard=example_base_ruleset.xml /var/lib/jenkins/workspace/pec4/dvwa/
'''
       }
   }
   stage("Create app") {
       steps {
//           sh "cd /var/lib/jenkins/workspace/pec4_2; docker build ."
           sleep 1
       }
   }
//   me da Successfully built b69a246add29
   stage("Start app") {
    steps {
//   sh "docker run -d -p 8080:80 b69a246add29"
      sleep 1
    }
   }
 } 

 post {
    always {
       sleep 5
    }
 }
}
