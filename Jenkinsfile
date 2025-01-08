pipeline {
    agent any
	environment {
	    GIT_TOKEN = credentials('git-gcp-tf')
    }
    stages {
        stage('Git Checkout') {
            steps {
               git "https://github.com/datanlabs1/gcp-tf-jenkins.git"
            }
        }
        
        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                }
            }
        }
        
        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

	    stage('Manual Approval') {
            steps {
                input "Approve?"
            }
        }
	    
        stage('Terraform Apply') {
            steps {
                script {
                    sh 'terraform apply tfplan'
                }
            }
        }
    }
}