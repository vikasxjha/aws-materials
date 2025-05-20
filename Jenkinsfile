pipeline {
  agent any

  environment {
    TF_VAR_region = "us-east-1"
    AWS_DEFAULT_REGION = "us-east-1"
    AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
    AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
  }

  options {
    timestamps()
  }

  stages {
    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Terraform Init') {
      steps {
        dir('terraformTask') {
          sh 'terraform init'
        }
      }
    }

    stage('Terraform Format Check') {
      steps {
        dir('terraformTask') {
          sh 'terraform fmt -check -recursive'
        }
      }
    }

    stage('Terraform Validate') {
      steps {
        dir('terraformTask') {
          sh 'terraform validate'
        }
      }
    }

    stage('Terraform Plan') {
      steps {
        dir('terraformTask') {
          sh 'terraform plan -out=tfplan'
        }
      }
    }

    stage('Terraform Apply') {
      steps {
        input message: 'Approve Terraform Apply?'
        dir('terraformTask') {
          sh 'terraform apply tfplan'
        }
      }
    }
  }

  post {
    success {
      echo "✅ Terraform infrastructure deployed successfully."
    }
    failure {
      echo "❌ Terraform pipeline failed."
    }
  }
}
