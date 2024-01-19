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
                sh 'mvn clean package'
            }
        }
    }
}
