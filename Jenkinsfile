pipeline{
    agent {
        node {
            label "devops-server"
            customWorkspace "/data/Workspace"
        }
    }
    environment {
        PROJECT_ID = 'devopsproject85'
        CLUSTER_NAME = 'lab-cluster'
        LOCATION = 'us-central1'
        CREDENTIALS_ID = 'gke-project'
        
    }

    stages{
        stage('checkout git'){
            steps{
                 git branch: 'main',
               url:'https://github.com/verman85/your-repo.git'
            }
           
        }

        stage('Build App'){
            steps{
                sh './mvnw clean package -Dmaven.test.skip=true'
            }
        }
       stage('Docker build'){
        steps{
            script{
                sh 'docker build -t verman85/petclinic:0.1 . '
            }
        }
       }
       stage('Docker login and push'){
        steps{
            withCredentials([string(credentialsId: 'dockerhubsecret', variable: 'dockerhubsecret')]) {
            sh 'docker login -u verman85 -p ${dockerhubsecret}'
            sh 'docker push verman85/petclinic:0.1'
        }

       }
       }


       stage('Deploy to kubernetes'){
        steps{
            
            step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'petclinic.yaml',manifestPattern: 'petclinic-svc.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: false])
		   echo "Deployment Finished ..."
        }
       }

    }
}

