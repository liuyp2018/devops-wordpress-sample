pipeline{
    agent {
        node {
            label 'maven'
        }
    }

    environment{
        DOCKERHUB_CREDENTIAL_ID = 'dockerhub-id'
        KUBECONFIG_CREDENTIAL_ID = 'demo-kubeconfig'
    }

    stages{
        stage('deploy microcks'){
            steps{
                kubernetesDeploy(configs: 'deploy/devops-mysql/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
                kubernetesDeploy(configs: 'deploy/devops-wordpress/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
            }
        }
    }
}