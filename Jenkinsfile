node {
              
    stage('Git clone') {
         
            git branch: 'master', credentialsId: 'jenkins', url: 'git@github.com:ghofranzaatouri/jenkines.git'
               //generate pair key jenkins private github public 
    }
       
    stage('Docker Build') {
       sh 'docker build -t asscmaster96/k8s-jenkins:NET-$BUILD_NUMBER .' 
        // sh 'docker build -t k8s-jenkins/odoo:latest .' 
        }   
    

    stage('Push') {
           withDockerRegistry([ credentialsId: "dockerHUB", url: "" ]) {   
         
         sh 'docker push asscmaster96/k8s-jenkins:NET-$BUILD_NUMBER'
         // sh 'docker push asscmaster96/odoo:latest'
        // token from docker hub
    }
    }
    stage('Deploy to K8S Master') {
       //admin.conf from k8s
          kubernetesDeploy configs: 'odoo-deployment.yaml', kubeConfig: [path: ''], kubeconfigId: 'kubernetes', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }    
          

    }    
           
