#!/usr/bin/env groovy


pipeline {
  agent any
  environment {
    DEVELOPMENT_ENV = 'dev'
    STAGING_ENV = 'pre'
    PRODUCTION_ENV = 'prod'
  }
  parameters {
    choice(
      name: 'ENVIRONMENT',
      choices:"dev\npre\nprod",
      description: '''DEV: Desplegar en dev PRE Desplegar en pre PROD: Desplegar en prod'''
					 
						  
    )
    choice(
      name: 'EXECUTE',
      choices:"DEPLOY\nROLLBACK\nREGISTRY",
      description: '''DEPLOY: Se realiza deploy del servicio'''
										   
													
    )
  }
  stages {
    stage('Checkout') {
      steps {
        /*checkout scm*/
		echo 'make test-project0'
      }
    }

    stage('Tests') {
      steps {
        echo 'make test-project'
      }
    }

    /* #################### Development #################### */

    stage('Development Config') {
      when {
        allOf { environment name: 'CHANGE_ID', value: ''}
        expression { return params.ENVIRONMENT == DEVELOPMENT_ENV }
      }
      steps {
        /*
		script {
          config = fnSteps.configs(DEVELOPMENT_ENV)
        }
		*/
		echo 'Deploying'
      }
    }
    stage('Development') {
      parallel {
        stage('Deploy') {
          steps { script { echo "1" } }
        }
        stage('Rollback') {
          steps { script { echo "hola" } }
        }
        stage('ECR') {
           steps { script { echo "hola2" } }
        }
      }
    }

    /* #################### Staging #################### */

    stage ('Staging Config') {
    
      steps {
        input "Continue deployment to Staging?"
        script {
          echo "hola"
        }
      }
    }

  }
}
