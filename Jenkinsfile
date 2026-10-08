
pipeline {
    agent {
        label 'jenkins-agent'
    }

    environment {
        DOCKER_IMAGE = 'tanu011/hybrid-devops-app'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                echo 'Building the application with Maven'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
          steps {
              echo 'Running SonarQube code analysis'
              withSonarQubeEnv('SonarQube') {
             sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
            }
          }
       }
        stage('Docker Build') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} .'
            }
        }

        stage('Docker Push') {
            steps {
                echo 'Pushing Docker image to Docker Hub'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                            -u "$DOCKER_USERNAME" \
                            --password-stdin

                        docker push ${DOCKER_IMAGE}:${IMAGE_TAG}

                        docker logout
                    '''
                }
            }
        }

       stage('Deploy to EKS') {
       steps {
        echo 'Deploying application to Amazon EKS'

        sh '''
            export PATH=/usr/local/bin:/usr/local/aws-cli/v2/current/bin:$PATH
            
            kubectl apply -f k8s/deployment.yaml
            kubectl apply -f k8s/service.yaml
            kubectl apply -f k8s/ingress.yaml

            kubectl set image deployment/hybrid-devops-app \
              hybrid-devops-app=${DOCKER_IMAGE}:${IMAGE_TAG} \
              -n dev-ns

            kubectl rollout status deployment/hybrid-devops-app -n dev-ns
        '''
    }
}

    post {
        success {
            echo 'Hybrid DevOps CI/CD pipeline completed successfully'
        }

        failure {
            echo 'Pipeline failed. Check the Jenkins console output.'
        }
    }
}
