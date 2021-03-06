pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_NAME', defaultValue: 'calculadora-java', description: 'Name for the image') 
    }
    
    stages {
        /*
        stage ('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        */
        
        stage ('Build Docker Image') {
            steps {
                sh 'docker build -t "${IMAGE_NAME}" .'
            }
        }

        stage ('Copy Image to Nexus') {
            steps {
                //sh 'docker login -u admin -p henrique localhost:8082'
                sh 'docker tag ${IMAGE_NAME} localhost:8082/${IMAGE_NAME}'
                sh 'docker push localhost:8082/${IMAGE_NAME}'
                sh "curl -v --user 'admin:admin' --upload-file ./*.jar http://localhost:8081/repository/raw/arquivo.jar"
            }
        }
    }
}
