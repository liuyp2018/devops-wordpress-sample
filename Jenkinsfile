pipeline{
    agent {
        node {
            label 'maven'
        }
    }

    environment{
        KUBECONFIG_CREDENTIAL_ID = 'demo-kubeconfig'
    }

    stages {
        stage ('checkout scm') {
            steps {
                checkout(scm)
            }
        }
    
    stages{
        stage('deploy mysql'){
            steps{
                kubernetesDeploy(configs: 'deploy/devops-mysql/**', deleteResource: true, enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
               }
        }
    }
                
    stages{
        stage('deploy mysql'){
            steps{
                kubernetesDeploy(configs: 'deploy/devops-wordpress/**', deleteResource: true, enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
            }
        }
    }
}
