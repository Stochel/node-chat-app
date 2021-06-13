pipeline {
    agent any 
    
    tools {nodejs "NodeJS"}
    
    stages {
        stage('Build') { 
            steps {
                echo 'Building!'
                sh 'git pull origin master'
                sh 'npm install'
                
            }
            post {
        	failure {
        		echo 'Build failed!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Build failed - please check logs"
        	}
        	success {
            		echo 'Build finished successfully!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Latest build finished successfully!"
        	}
    		}
        }

    
    
    
        stage('Test') { 
            steps {
                echo 'Testing!'
                sh 'npm run test'
            }
            post {
        	failure {
        		echo 'Build failed!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Test failed - please check logs"
        	}
        	success {
            		echo 'Testing finished successfully!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Latest testing finished successfully!"
        	}
    		}
        }
        
        
        
        
        stage('Deploy') { 
            steps {
                echo 'Deploying!'
                sh 'docker build -t deployed-app -f Dockerfile_deployer .'
            }
            post {
        	failure {
        		echo 'Deployment failed!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Deployment failed - please check logs"
        	}
        	success {
            		echo 'Deployment finished successfully!'
            		emailext attachLog: true,
                	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                	to: 'stochel.sebastian@gmail.com',
                	subject: "Latest deployment finished successfully!"
        	}
    		}
        }
        
        
    }

    
}
