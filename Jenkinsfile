pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION    = 'ap-south-1'
    }
    
    stages {        
        stage('Terraform Init') {
            steps {
                script {
                    // Find all directories containing .tf files
                    def directories = sh(script: "find . -type f -name '*.tf' -exec dirname {} \\;", returnStdout: true).trim().split("\n")
                    
                    // Iterate over each directory
                    directories.each { directory ->
                        // Execute Terraform init in each directory
                        sh "cd ${directory} && terraform init"
                    }
                }
            }
        }
        
        stage('Terraform Plan') {
            steps {
                script {
                    // Find all directories containing .tf files
                    def directories = sh(script: "find . -type f -name '*.tf' -exec dirname {} \\;", returnStdout: true).trim().split("\n")
                    
                    // Iterate over each directory
                    directories.each { directory ->
                        // Execute Terraform plan in each directory
                        sh "cd ${directory} && terraform plan -out=tfplan"
                    }
                }
            }
        }
        
        stage('Terraform Apply') {
            steps {
                script {
                    // Find all directories containing .tf files
                    def directories = sh(script: "find . -type f -name '*.tf' -exec dirname {} \\;", returnStdout: true).trim().split("\n")
                    
                    // Iterate over each directory
                    directories.each { directory ->
                        // Execute Terraform apply in each directory with confirmation
                        sh "cd ${directory} && terraform apply -auto-approve tfplan"
                    }
                }
            }
        }

        stage('Terraform Destroy') {
            steps {
                script {
                    // Find all directories containing .tf files
                    def directories = sh(script: "find . -type f -name '*.tf' -exec dirname {} \\;", returnStdout: true).trim().split("\n")
                    
                    // Iterate over each directory
                    directories.each { directory ->
                        // Execute Terraform destroy in each directory with confirmation
                        sh "cd ${directory} && terraform destroy -auto-approve"
                    }
                }
            }
        }
    }
}
