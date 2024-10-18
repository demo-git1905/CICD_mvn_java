pipeline {
    agent any

    tools {
        // Install the JDK and Maven tools
        jdk 'JDK 8'  // Assuming you have a JDK tool named 'JDK 11' installed in Jenkins
        maven 'Maven 3.9.9'  // Assuming you have Maven installed in Jenkins
    }

    environment {
        // Define environment variables
        JAVA_HOME = tool name: 'JDK 8'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git 'https://github.com/DebaratiBiswas/CICD_mvn_java.git'
            }
        }

        stage('Build') {
            steps {
                // Execute Maven build command
                sh 'mvn clean install'
            }
        }
    }

    post {
        always {
            // Archive artifacts and test reports
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        success {
            // Send notification on successful build
            echo 'Build completed successfully'
        }
        failure {
            // Send notification on failed build
            echo 'Build failed'
        }
    }
}
