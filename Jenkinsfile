pipeline {
    agent any
    tools {
        maven "M3"
    }

    environment {
        app_name = 'trading_app'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
                echo "app_name is ${env.app_name} "
                archiveArtifacts 'target/*zip'
            }
        }
        stage('Deploy_dev') {
            when { branch 'development' }
            steps {
                echo "Current Branch is: ${env.GIT_BRANCH}"
                sh "bash ./scripts/eb_deploy.sh trading_app TradingApp-env"
            }
        }
        stage('Deploy_prod') {
            when { branch 'master' }
            steps {
                echo "Current Branch is: ${env.GIT_BRANCH}"
                sh "./scripts/eb_deploy.sh trading_app TradingApp-prod"
            }
        }
    }
}
