pipeline {
  agent any
  parameters {
        choice(name: 'CHOICE', choices: ['Dev', 'Stg', 'Prod'], description: 'Pick something')
}
  environment {
    registryUri = "registry.hub.docker.com/"
    dev_registry = "viveksawant100/cloudethix-sample-nginx"
    dev_registryCred = "dev_dockerhub_cred"  
    qa_registryCred = "qa_dockerhub_cred" 
  }
stages {
    stage ("build image and create project dir") {
       environment {
        registry_endpoint = 'https://' + "${env.registryUri}" + "${env.dev_registry}"
        docker_image = "${env.dev_registry}" + ":$GIT_COMMIT"
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
  post {
  always {
       sh 'echo Cleaning docker Images from Jenkins.'
       sh "docker rmi ${env.dev_image}"
  }
 }

}
}