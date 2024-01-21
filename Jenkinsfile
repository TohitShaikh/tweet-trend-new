pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('Checkout-Code') {
            steps {
                git branch: 'main', url: 'https://github.com/TohitShaikh/tweet-trend-new.git'
            }
        }
        
        stage('Build-Stage') {
            steps {
                echo "-----------buildt-started-------------"
                sh 'mvn clean package -DskipTests'
                echo "-----------build-completed-------------"
            }
        }
        stage('Unit-Test-Cases') {
            steps {
             echo "-----------unit-test-started-------------"   
            sh 'mvn surefire-report:report'
            echo "-----------unit-test-completed-------------"
        }
        }
        
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonarqube-scanner'
            }
            steps {
                    withSonarQubeEnv('sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }

