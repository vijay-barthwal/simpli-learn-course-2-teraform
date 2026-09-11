pipeline {
    agent any

    tools {
        // Task 3 & 5 requirement: Links Jenkins to the Maven tool installed on the system
        maven 'Maven3' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Task 6 & 7 requirement: Checks out the code pushed to your GitHub repository
                checkout scm
            }
        }

        stage('Build Artifact') {
            steps {
                // Task 3 requirement: Packages the PetClinic project using the Maven wrapper or Maven CLI
                // Switch between './mvnw' or 'mvn' based on your repository setup
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Local Tomcat') {
            steps {
                // Task 8 requirement: Deploys the application directly to the local Tomcat webapps directory
                // Changes ownership/permissions might be needed depending on your EC2 setups
                sh 'sudo cp target/*.war /var/lib/tomcat9/webapps/petclinic.war'
            }
        }
    }
}
