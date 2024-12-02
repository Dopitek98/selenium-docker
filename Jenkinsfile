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
            bat "docker build -t=dopitek2012/selenium ."
        }
    }

    stage('Push image'){
        environment{
        DOCKER_HUB = credentials('docker-hub-credentials')
        }
        steps{
            bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
            bat "docker push dopitek2012/selenium"
        }
    }
}

post{
    always{
        bat "docker logout"
    }
}
}