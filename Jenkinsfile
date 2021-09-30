pipeline {
    agent {
        node {
            label 'node_main'
        }
    }
    stages {
        stage('Checkout code'){
            steps {
                 checkout scm
            }
       }
        stage('Build') {
            steps {
                sh '''
                cd spring_petclinic
                sudo chmod +x mvnw
                sudo ./mvnw package
                '''
                stash name: "artifact", includes: "spring_petclinic/target/*.jar"
            }
        }
        stage ('Delivery artifactory') {
                 steps {
                    node('node_artifactory'){
                        unstash name: "artifact" 
                    }
                 }
        }
    }
}
