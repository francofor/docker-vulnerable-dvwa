pipeline {
 agent any
 
 stages {
   stage("Preparation") { 
     steps {
       git 'https://github.com/francofor/docker-vulnerable-dvwa'
     }
   }
   stage("First Code Analysis") {
       steps {
sh '''cd /home/franco/wap; java -jar wap.jar -a -s -all -p /var/lib/jenkins/workspace/pec4/dvwa/
'''
       }
   }
   stage("Second Code Analysis") {
       steps {
sh '''cd /home/franco/phpcs-security-audit-master; ./vendor/bin/phpcs --standard=example_base_ruleset.xml /var/lib/jenkins/workspace/pec4/dvwa/tmp.php
'''
       }
   }
   stage("Create App") {
       steps {
           sh "cd /var/lib/jenkins/workspace/pec4; docker build -t pec4Image ."
       }
   }
   stage("Start App") {
    steps {
      sh "docker run -d -p 8080:80 pec4Image"
    }
   }
 } 

 post {
    always {
        mail to: 'francofor69@gmail.com',
        subject: "Jenkins job executed: ${currentBuild.fullDisplayName}",
        body: "Executed, please check ${env.BUILD_URL}"
    }
 }
}
