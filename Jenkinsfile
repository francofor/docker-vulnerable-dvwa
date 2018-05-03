pipeline {
 agent any
 
 stages {
   stage("Preparation") { 
     steps {
       sleep 1
     }
   }
   stage("First Code Analysis") {
       steps {
sh '''cd /home/franco/wap; java -jar wap.jar -a -s -all -p ${WORKSPACE}
'''
       }
   }
   stage("Second Code Analysis") {
       steps {
sh '''cd /home/franco/phpcs-security-audit-master; ./vendor/bin/phpcs --standard=example_base_ruleset.xml ${WORKSPACE}
'''
       }
   }
   stage("Create App") {
       steps {
           sh "cd /var/lib/jenkins/workspace/pec4; docker build -t pec4image ."
       }
   }
   stage("Start App") {
    steps {
      sh "docker run -d -p 8080:80 pec4image"
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
