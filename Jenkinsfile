pipeline {
    agent any

properties([disableConcurrentBuilds(), parameters([booleanParam(defaultValue: true, description: '', name: 'Build'), booleanParam(defaultValue: true, description: '', name: 'Publish')]), pipelineTriggers([githubPush()])])
stages {
   stage('Build') {
   if(params.Build)
   {
      sh label: 'Project Building', script: 'dotnet build'
   }
   }
   stage('Publish') {
      if(params.Publish)
      {
      sh label: 'Docker Publishing', script: 'docker-compose up -d'
      }
   }
}
}