
node {
     ecrRegistry = "133607893927.dkr.ecr.ap-southeast-1.amazonaws.com"
     def app 
      
     stage('Git')
     { 
     git branch: 'master', url: 'https://github.com/AdheipSingh/weather-geo.git'
   } 

    stage('Pull latest changes repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
        sh 'pwd'
        sh 'rm  ~/.dockercfg || true'
        sh 'rm ~/.docker/config.json || true'
    }
     
     stage ('Docker  configuration') {
         sh 'aws ecr get-login --region ap-southeast-1 | xargs'
     }
     stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        docker.withRegistry("${ecrRegistry}") {
        app = docker.build("${ecrRegistry}:auth-servicev$BUILD_NUMBER")
        sh 'pwd'
    }

     stage('Push image') {
        /* Finally, we'll push the image */
       // docker.withRegistry('https://133607893927.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:aws_ecr')  
          
        app.push("${env.BUILD_NUMBER}")
            
        }
  }
  
}
