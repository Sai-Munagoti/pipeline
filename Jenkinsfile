pipeline {
    agent any

    stages {
        stage('plan') {
            steps {
                echo 'I am doing project planning according to the requirements.'
            }
        }

        stage('cloning') {
            steps {
                sh 'rm -rf pipeline'
                sh 'git clone -b main https://github.com/Sai-Munagoti/pipeline.git'
            }
        }

        stage('package') {
            steps {
                dir('pipeline') {
                    sh 'ls -l'
                    sh 'mvn package'
                }
            }
        }

        stage('deploy') {
            steps {
                dir('pipeline/target') {
                    sh 'mv *.war ${JOB_NAME}${BUILD_NUMBER}.war'
                    sh 'cp *.war /opt/apache-tomcat-9.0.100/webapps'
                }
            }
        }

        stage('backup') {
            steps {
                dir('pipeline/target') {
                    sh 'cp *.war /home/'
                }
            }
        }

        stage('clean') {
            steps {
                dir('pipeline') {
                    sh 'ls -l'
                    sh 'rm -rf pipeline'
                }
            }
        }
    }
}
