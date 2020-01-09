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
		
	   stage('deploy'){
               steps{
                 kubernetesDeploy(configs: 'deploy/devops-mysql/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
                 kubernetesDeploy(configs: 'deploy/devops-wordpress/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")}
               }
	    }
         
           stage('test curl'){
               steps{  
                 script {
                    response = sh(
                      returnStdout: true, 
                      script: "curl http://wordpress.demo.example.cluster.local:32548/wp-admin/install.php"
                    );
                    def finder = (response =~ /(?s).*language*/);
                    if (finder) {
                       echo "success";
                    } else {
                       error "curl failed";
                    }
                 }
               }
            }
		
	   stage('update'){
               steps{
                 kubernetesDeploy(configs: 'deploy/devops-mysql/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
                 kubernetesDeploy(configs: 'deploy/devops-wordpress/**', enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")}
                }
	     }
		
	   stage('test curl'){
               steps{  
                 script {
                    response = sh(
                      returnStdout: true, 
                      script: "curl http://wordpress.demo.example.cluster.local:32548/wp-admin/install.php"
                    );
                    def finder = (response =~ /(?s).*language*/);
                    if (finder) {
                       echo "success";
                    } else {
                       error "curl failed";
                    }
                 }
               }
            }
		
	   stage('delete'){
               steps{
                 kubernetesDeploy(configs: 'deploy/devops-mysql/**', deleteResource: true, enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")
                 kubernetesDeploy(configs: 'deploy/devops-wordpress/**', deleteResource: true, enableConfigSubstitution : true, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID")}
               }
            }
     }
}
