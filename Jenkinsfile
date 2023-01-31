pipeline {
  agent any
  parameters {
        choice(name: 'CHOICE', choices: ['Dev', 'Stg', 'Prod'], description: 'Pick something')
}
  environment {
    registryUri = "registry.hub.docker.com/"
    registry = "viveksawant100/cloudethix-sample-nginx"
    dev_registryCred = "dev_dockerhub_cred"  
  }
stages {
    stage ("build image and create project dir") {
       environment {
        registry_endpoint = 'https://' + "${env.registryUri}" + "${env.registry}"
        docker_image = "${env.registry}" + ":$GIT_COMMIT"
       }
       steps {
        script {
          def app = docker.build(docker_image)
           docker.withRegistry (registry_endpoint, dev_registryCred) {
            app.push()
           }
        }
     }
           
  } 
   stage ("Remove Unused Docker image"){
      sh "docker rmi ${env.registry}" + ":$GIT_COMMIT"
   } 
}
}