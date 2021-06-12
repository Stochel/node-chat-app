pipeline {

    agent any
    	tools {nodejs "NodeJS"}
	
    stages {
        stage('Test') {
            steps {
                echo 'Testing!"
		 sh 'npm install'
                sh 'npm run test'
            }
        }
    }
    
    post {
        always {
            echo "Finished!"
        }
        success {
            echo 'Success!"
        }
        failure {
            echo 'Failure!'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                to: 'stochel.sebastian@gmail.com',
                subject: "Building or testsing failed - please check the logs"
        }
    }
}

