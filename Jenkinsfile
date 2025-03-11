pipeline
  agent any

   stages {
    stage ('plan') {
        steps {
            echo 'i am doing project planning accroding to'
        }
    }
   }
   stage ('cloning') {
     steps {
        sh 'rm -rf pipeline'
        sh 'git clone -b main https://github.com/Sai-Munagoti/pipeline.git'
     }
   }
   stage ('package') {
    steps {
        dir ("pipeline") {
            sh 'ls -l'
            sh 'mvn package'
        }
    }
   }
   stage (permission) {
    steps {
        dir ("opt/apache-tomcat-9.0.100") {
            sh 'chown -R jenkins:jenkins /opt/apache-tomcat-9.0.100/webapps'
        }
    }
   }
   stage ('home-permission') {
    steps {
        dir ("/home/") {
            sh 'chmod 755 /home/jenkins'
        }
    }
   }
   stage ('deploy') {
    steps {
        dir ("pipeline/target") {
            sh 'mv *.war ${JOB_NAME}${BUILD_NUMBER}.war'
            sh 'cp *.war /opt/apache-tomcat-9.0.100/webapps'
        }
    }
   }
   stage ('delete') {
    steps {
        dir ("pipeline/target") {
            sh 'cp *.war /home/'
        }
    }
   }
   stage ('clean') {
    steps {
        dir ("pipeline") {
            sh 'ls -l'
            sh 'rm -rf pipeline'
        }
      }
   }
