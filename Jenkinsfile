node{
     
    stage('SCM Checkout'){
        git url: 'https://github.com/MithunTechnologiesDevOps/java-web-app-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t ouusssamaaa/java-web-app .'
    }
    
    stage('Push Docker Image'){
    
        withCredentials([usernamePassword(credentialsId: 'Docker_Hub_Pwd', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
             sh ''' docker login -u ${USERNAME} -p ${PASSWORD}
                    docker push ouusssamaaa/java-web-app
              '''
        }
        
     }
     
      stage('Run Docker Image In Dev Server'){
        
          sh' docker run  -d -p 8080:8080 --name java-web-app ouusssamaaa/java-web-app'
       
       }
     
}
