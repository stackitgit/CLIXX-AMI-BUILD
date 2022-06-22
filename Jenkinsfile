pipeline {
    agent any
    parameters {
  credentials credentialType: 'com.cloudbees.jenkins.plugins.awscredentials.AWSCredentialsImpl', defaultValue: '3bc3c0e2-3081-41ef-92ad-09195816a3f7', name: 'AWS_CREDS', required: false
}
    environment {
        PATH = "${PATH}:${getTerraformPath()}:${getAnsiblePath()}"
    }
    stages{

         stage('Initial AMI Deployment Approval') {
              steps {
                script {
                def userInput = input(id: 'confirm', message: 'Start Pipeline?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Start Pipeline', name: 'confirm'] ])
             }
           }
        }

         stage('terraform init'){
             steps {
                 sh "terraform init"
                 
         }
         }
         stage('Packer AMI Build'){
             steps {
                 sh "terraform plan -out=tfplan -input=false"
             }
         }
      
    }
}

 def getTerraformPath(){
        def tfHome= tool name: 'terraform-14', type: 'terraform'
        return tfHome
    }

 def getAnsiblePath(){
        def AnsibleHome= tool name: 'Ansible', type: 'org.jenkinsci.plugins.ansible.AnsibleInstallation'
        return AnsibleHome
    }