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
        
        stage('printYaml'){
            steps{
                script{
                
                    println "this is yaml step"
                    Map filee = readYaml file:'config.yml'
                    println filee
                    println "printing java version"
                    def javaHome = tool 'jdk8'
                    println 'javaHome is given by ${javaHome}'
                     println javaHome 
                }
            }
        }

        stage('test'){
            steps{
                bat 'mvn test'
            }
            post{
                always{ 
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('publish'){
            steps{
                bat 'mvn package'
            }
            post{
                    success{
                      //  echo "we are successfull"
                        archiveArtifacts 'target/*.jar'
                    }
            }
        }

        stage('get jar path'){
            steps{
                script{
                    def file = findFiles(glob : '**/target/*.jar')
                    println(file[0].path)
                }
            }
        }
    }
}
