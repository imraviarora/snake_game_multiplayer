node ('ubuntu-app-agent'){  
    def app
    stage('Cloning Git') {
       checkout scm /* Let's make sure we have the repository cloned to our workspace */
    }  
    /*stage('SAST'){
        build 'SECURITY-SAST-SNYK'
    }*/
    stage('Build-and-Tag') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
       app = docker.build("ravikumar7206/snake")
    }
    stage('Post-to-dockerhub') {
       docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_cred') {
              app.push("latest")
        			              }
    }
  /*  stage('SECURITY-IMAGE-SCANNER'){
        build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
    } */
    stage('Pull-image-server') {
       sh "docker-compose down"
       sh "docker-compose up -d"
      }
    /*stage('DAST'){
        build 'SECURITY-DAST-OWASP_ZAP'
        }*/
}
