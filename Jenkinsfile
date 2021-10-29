pipeline {
    agent any
tools { 
        maven 'Maven 3.8.3' 
        jdk 'jdk8' 
    }
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/Lovnish10/JavaMavenJenkinsBuild.git'
              //  sh './mvnw clean compile'
               echo "M2_HOME = ${M2_HOME}"
               bat "mvn  clean compile"
            }
        }

        stage('test'){
            steps{
                bat 'mvn test'
            }
            post{
                always{
                    
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
