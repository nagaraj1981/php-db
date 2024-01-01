pipeline{
    agent any
    environment{
       IMAGE_NAME='nagaraj1981/dockrepo2018:php$BUILD_NUMBER'
       DEV_SERVER_IP='ec2-user@65.2.4.211'
       DEPLOY_SERVER_IP='ec2-user@3.110.44.153'

    }
    stages{
        stage("Build the docker image for PHP and push to prviate registry"){
            steps{
            script{
                sshagent(['build-server']){
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
                sh "ssh -o strictHostKeyChecking=no -r devserverconfig  ${DEV_SERVER_IP}:/home/ec2-user"
                sh "ssh -o strictHostKeyChecking=no ${DEV_SERVER_IP} 'bash ~/devserverconfig/docker-script.sh"
                sh "ssh  ${DEV_SERVER_IP} sudo docker build -t ${IMAGE_NAME} ~/devserverconfig"
                sh "ssh  ${DEV_SERVER_IP} sudo docker login -u  ${USERNAME} -p ${PASSWORD}"
                sh "ssh  ${DEV_SERVER_IP} sudo docker push ${IMAGE_NAME}"
                }
            }
            }

            }
    }
        // stage("Deploy the microsvc app"){
        //     script{

        //     }


        // }
    }

}