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
        steps{
            bat "docker push dopitek2012/selenium"
        }
    }
}

}