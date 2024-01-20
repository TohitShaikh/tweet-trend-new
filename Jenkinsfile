pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    tools {
        // Define the Maven tool named 'Maven' in the Jenkins Global Tool Configuration
        maven 'Maven'
        // Define the JDK tool named 'JDK17' in the Jenkins Global Tool Configuration
        jdk 'JDK17'
    }

    stages {
        stage('Checkout-Code') {
            steps {
                git branch: 'main', url: 'https://github.com/TohitShaikh/tweet-trend-new.git'
            }
        }

        stage('Build-Stage') {
            steps {
                // Use the configured Maven and JDK tools
                script {
                    def mavenHome = tool 'Maven'
                    def jdkHome = tool 'JDK17'
                    sh "${mavenHome}/bin/mvn clean package"
                }
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonarqube-scanner'
            }
            steps {
                script {
                    def scannerHome = tool 'sonarqube-scanner'
                    withSonarQubeEnv('sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
