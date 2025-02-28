pipeline{
    agent{
        label "project-jenkins-slave"
    }
    environment{
        AWS_REGION = "ap-south-1"
        REGISTRY_PATH = "084375589021.dkr.ecr.ap-south-1.amazonaws.com"
        APP_ECR_REPO = "cicd-project-app"
        DB_ECR_REPO = "cicd-project-db"
        WEB_ECR_REPO = "cicd-project-web"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages{
        stage("fetch code"){
            steps{
                git branch: 'main', url: 'https://github.com/mohamed-r-abdelhafez/CICD-EKS.git'
            }
        }

        stage("Maven Build"){
            steps{
                sh 'mvn clean install -DskipTests'

            }
        }

        stage('Login to ECR'){
            steps{
                sh 'aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin ${REGISTRY_PATH}'
            }
        }

        stage("docker build and push"){
            steps{
                sh '''
                def app_image = "${REGISTRY_PATH}/${APP_ECR_REPO}:${IMAGE_TAG}"
                def db_image = "${REGISTRY_PATH}/${DB_ECR_REPO}:${IMAGE_TAG}"
                def web_image = "${REGISTRY_PATH}/${WEB_ECR_REPO}:${IMAGE_TAG}"

                sh "docker build -t ${app_image} ./Docker-files/app/"
                sh "docker build -t ${db_image} ./Docker-files/db/"
                sh "docker build -t ${web_image} ./Docker-files/web/"

                sh "docker push ${app_image}"
                sh "docker push ${db_image}"
                sh "docker push ${web_image}

                '''
            }
            post{
                success{
                    echo 'Build and Push Successful!'
                }
                failure{
                    echo 'Build and Push Failed!'
                }
            }

        }


    }

}