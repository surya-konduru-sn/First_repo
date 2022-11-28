def artifactname = "sp-boot-app.jar"
def repoName = "sp-boot-app-repo"
def pipelineName = "devops_vk_pipeline"
def semanticVersion = "${env.BUILD_NUMBER}.0.0"
def packageName = "spboot-package_${env.BUILD_NUMBER}"
def version = "${env.BUILD_NUMBER}.0"
def pkgName = "sp-boot-package"
def changeRequestId = "testId"
pipeline {
  agent any
  stages {
       stage('Build') {
           steps {
              snDevOpsStep()

           }
       }
       stage('Test') {
           steps {
              snDevOpsStep()
           }
       }
      stage('Deploy') {
           steps {
              snDevOpsStep()
              echo 'Deploying the change....$changeRequestId'
              echo "Deploying the change....${changeRequestId}"	      
              snDevOpsChange changeRequestDetails: '{ "attributes": { "short_description": "pkgName => ${pkgName}", "description": "changeRequestId => ${changeRequestId}"}}'
	      script {
	      	changeRequestId = snDevOpsGetChangeNumber()
                echo "Inside Script Block => Deploying the change....${changeRequestId}"
	      }
              echo "Deploying the change....${changeRequestId}, env.BUILD_NUMBER => ${env.BUILD_NUMBER}"
           }
      }
      stage('TestChange') {
      	steps {
		
	      script {
	      	changeRequestId = snDevOpsGetChangeNumber changeDetails: '{"pipeline_name":"surya-multibranch","build_number":"2","stage_name":"Deploy"}'
		echo "Inside Script Block => Test the change....with double quotes ${changeRequestId}"
	      }
              echo "Deploying the change....${changeRequestId}"
	}
      }

  }

}
