pipeline {
    agent any

    environment {
        // Update this to wherever Tomcat is reachable from the Jenkins agent
        TOMCAT_URL   = 'http://localhost:8080'
        CONTEXT_PATH = '/petclinic'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'tomcat-manager',
                    usernameVariable: 'TOMCAT_USER',
                    passwordVariable: 'TOMCAT_PASS'
                )]) {
                    sh '''
                        WAR_FILE=$(ls target/*.war)
                        curl -f -u "$TOMCAT_USER:$TOMCAT_PASS" \
                             -T "$WAR_FILE" \
                             "$TOMCAT_URL/manager/text/deploy?path=$CONTEXT_PATH&update=true"
                    '''
                }
            }
        }
    }
}
