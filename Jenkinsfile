
node {
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

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        sh 'whoami'
        app = docker.build("133607893927.dkr.ecr.ap-southeast-1.amazonaws.com/istio:auth-servicev$BUILD_NUMBER")
        sh 'pwd'
    }

     stage('Push image') {
        /* Finally, we'll push the image */
        docker.withRegistry('https://133607893927.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:aws_ecr')    {
        app.push("${env.BUILD_NUMBER}")
            
        }
  }
  
}
