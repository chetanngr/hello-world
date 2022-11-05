#!groovy

pipeline {

    agent any
    
    tools {
        maven 'Maven'
        jdk 'jdk'
    }

    environment {
    // Credentials - These are credential ID's stored in bitbucket, that map to actual username/password values held in Jenkins.
    
    //GIT_CREDENTIAL = 'b23b3e68-08fb-4364-9332-c39b3ab20391'
   // GIT_BRANCH='feature/new-aws-pipeline'
	 // Location of source directories, each component of the application will be under one of these directories
    CONTEXT_DIR_API = 'api'
    CONTEXT_DIR_UI = 'ui'
   // SOURCE_SECRET = 'bitbucket-scmsource-hook'


    APPLICATION_NAME = "aws-vehicle-order"
    //AWS_ACCOUNT_ID = "839649461993"
   // AWS_DEFAULT_REGION = "eu-central-1"
    API_IMAGE_REPO_NAME = "app-veh-order-uk-api-tint"  
    //ECR = "839649461993.dkr.ecr.eu-central-1.amazonaws.com"
	//PROXY_USER = credentials('aws_tec_user') //use credential type username + password
    http_proxy = "http://$PROXY_USER@proxy.muc:8080"
    HTTP_PROXY = "http://$PROXY_USER@proxy.muc:8080"
    https_proxy = "http://$PROXY_USER@proxy.muc:8080"
    HTTPS_PROXY = "http://$PROXY_USER@proxy.muc:8080"
    NO_PROXY="localhost,127.0.0.1,bmwgroup.net,cloud.bmw"
    no_proxy="localhost,127.0.0.1,bmwgroup.net,cloud.bmw"
	PYTHONBIN = "$HOME/python/bin"
    PATH = "$PATH:/tools/python/python-3.7.3/bin:$HOME/python/bin:/tools/kubectl"
    PYTHONPATH = "$HOME/python/lib/python3.7/site-packages"
    }
     stages {
        stage(' Environment Details') {
			steps 	{
				script {
				currentBuild.displayName = "#${env.BUILD_NUMBER} - ${env.GIT_BRANCH}"
				currentBuild.description = ""
						}
				echo "BRANCH_NAME: ${env.BRANCH_NAME}"
        		echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
        	//	checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chetanngr/hello-world.git']]])
        
			}
		}
	
	stage('Build') {
      steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chetanngr/hello-world.git']]])
          //sh "mvn -Dmaven.test.failure.ignoretrue clean package"
      }
	}
	stage('Packaging Stage') {
      steps {
          bat 'mvn package'
      }
	}
    }
}
