pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean install'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }
        stage('Deploy to Tomcat'){
        steps {
        sh 'cp -r /root/.jenkins/workspace/mavendecleration/target/* /opt/apache-tomcat-8.5.32/webapps/'
        }
        }


        
    }
}
