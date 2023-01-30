pipeline {
  agent any
  parameters {
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
}
  stages {
    stage ("Printing Choice") {
       steps {
        echo "Choice: ${params.CHOICE}"
       } 
    }
       
  } 
}
