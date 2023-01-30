pipeline {
  agent any
  parameters {
        choice(name: 'CHOICE', choices: ['Dev', 'Stg', 'Prod'], description: 'Pick something')
}
  environment {
    registryUri = "registry.hub.docker.com/"
    registry = "viveksawant100/cloudethix-sample-nginx"
    registryCred = "dev_dockerhub_cred"  
  }
stages {
    stage ("build image and create project dir") {
       environment {
        registry_endpoint = 'https//' + "${env.registryUri}" + "${env.registry}"
        docker_image = "${env.registry}" + ":$GIT_COMMIT"
       }
       steps {
        script {
          def app = docker.build(docker_image)
           docker.withRegistry (registry_endpoint, registryCred) {
            app.push()
           }
        }
       }
       
  } 
}
}