pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
//         stage('Sonar-Report') {
//             steps {
//             sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=jenkins_project \
//   -Dsonar.host.url=http://localhost:9000 \
//   -Dsonar.login=5f09ded7e5db4d0ea0dcfd937c181af706e60475'
//             }
//         }
        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
stage('Sonar-Report') {
    steps {
        // Use 'bat' for your Windows slave01
        // Paste your token exactly as it appeared after clicking Generate
        bat 'mvn sonar:sonar -Dsonar.host.url=http://172.16.213.111:9000 -Dsonar.login=sqa_bb9b8d3f4b6017c6dd851405efd12531e1380600'
    }
}
    }
}
