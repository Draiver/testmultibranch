#!/usr/bin/env groovy

pipeline {
    agent any
    
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
        
        stages {
        
        stage('Read data from AWS Batch') {
          steps {
              script {
                  sh 'printenv'
                  scmVars = checkout scm
                  echo "${scmVars.GIT_BRANCH}"
                  echo "${scmVars.GIT_BRANCH}"
                  def job_name = sh returnStdout: true, script: 'aws batch describe-job-queues --job-queues --region us-east-1'
                  env.job_name = job_name
                  def job_def = sh returnStdout: true, script: 'aws batch describe-job-definitions | jq -r \'.jobDefinitions[] | select(.status=="ACTIVE") | .jobDefinitionArn\''
                  env.job_def = job_def
                }
            }
        }
    }
}
