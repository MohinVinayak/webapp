pipeline {
    agent {
        // Updated to your Windows slave where Maven/Java are configured
        label 'slave01' 
    }
    
    stages {
        stage('Build') {
            steps {
                // Cleans old builds and creates the new .jar file
                bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    // Publishes test results so you see them in Blue Ocean
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }

        stage('Sonar-Report') {
            steps {
                // Sends the analysis to your SonarQube server
                bat 'mvn sonar:sonar -Dsonar.host.url=http://172.16.213.111:9000 -Dsonar.login=sqa_bb9b8d3f4b6017c6dd851405efd12531e1380600'
            }
        }

        stage('Nexus-Upload') {
            steps {
                // Pushes the .jar to your Nexus on port 8082
                // Ensure your settings.xml on Slave-01 has the 'upes' credentials
                bat 'mvn deploy -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                // This triggers your deployment script on port 9999
                // Ensure C:\deployment\deploy.bat exists on Slave-01
                bat 'call C:\\deployment\\deploy.bat'
            }
        }
    }
}
