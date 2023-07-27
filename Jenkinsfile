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

        }
       }

