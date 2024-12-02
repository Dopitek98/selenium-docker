pipeline{
agent any

stages{
    stage('Build jar'){
        steps{
            bat "mvn clean package -DskipTests"
        }
    }

    stage('Build image'){
        steps{
            bat "docker build -t=dopitek2012/selenium:latest ."
        }
    }

    stage('Push image'){
        environment{
        DOCKER_HUB = credentials('docker-hub-credentials')
        }
        steps{
            bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
            bat 'docker push dopitek2012/selenium:latest'
            bat "docker tag dopitek2012/selenium:latest dopitek2012/selenium:${env.BUILD_NUMBER}"
            bat "docker push dopitek2012/selenium:${env.BUILD_NUMBER}"
        }
    }
}

post{
    always{
        bat "docker logout"
    }
}
}