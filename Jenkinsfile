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
         
        stage('test curl'){
            steps{  
                 script {
                    response = sh(
                      returnStdout: true, 
                      script: "curl http://wordpress.demo.example.cluster.local:32548/wp-admin/install.php"
                    );
                    def finder = (response =~ /(?s).*language11*/);
                    if (finder) {
                       echo "success";
                    } else {
                       error "curl failed";
                    }
                 }
            }
        }
    }
}
