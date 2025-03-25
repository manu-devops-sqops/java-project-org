pipeline {
    agent any  // Runs on any available agent

    // environment {
    //     SONAR_URL = 'http://your-sonar-server'  // Update with your SonarQube URL
    //     SONAR_TOKEN = credentials('sonar-token')  // SonarQube authentication token stored in Jenkins credentials
    //     SONAR_PROJECT_KEY = 'java-project'  // Your SonarQube project key
    // }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Cloning the repository..."
                git branch: 'main', url: 'https://github.com/manu-devops-sqops/java-project.git'
            }
        }
    
        stage('Clean') {
            steps {
                echo "Running mvn clean..."
                sh 'mvn clean'
            }
        }

        stage('Compile') {
            steps {
                echo "Compiling source code..."
                sh 'mvn compile'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                sh 'mvn test'
            }
        }
        stage('Verify') {
            steps {
                echo "Running mvn verify..."
                sh 'mvn verify'
            }
        }

        // stage('SonarQube Analysis') {
        //     steps {
        //         echo "Running SonarQube analysis..."
        //         sh '''
        //             mvn sonar:sonar \
        //             -Dsonar.projectKey=$SONAR_PROJECT_KEY \
        //             -Dsonar.host.url=$SONAR_URL \
        //             -Dsonar.login=$SONAR_TOKEN
        //         '''
        //     }
        // }

        // stage('Check SonarQube Quality Gate') {
        //     steps {
        //         script {
        //             echo "Waiting for SonarQube analysis to complete..."
        //             sleep(time: 30, unit: 'SECONDS') // Give Sonar some time to process

        //             def response = sh(script: """
        //                 curl -s -u $SONAR_TOKEN: $SONAR_URL/api/issues/search?componentKeys=$SONAR_PROJECT_KEY&severities=CRITICAL&resolved=false
        //             """, returnStdout: true).trim()

        //             def criticalIssues = response.count('"key"')  // Counting occurrences of "key" in the JSON response
        //             echo "Critical vulnerabilities found: ${criticalIssues}"

        //             if (criticalIssues > 5) {
        //                 error "Pipeline failed: More than 5 critical vulnerabilities found!"
        //             }
        //         }
        //     }
        // }
    }

    post {
        always {
            echo "Pipeline execution completed!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
