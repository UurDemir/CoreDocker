pipeline 
{
    agent any

    options 
    {
        disableConcurrentBuilds()
    }

    parameters 
    {
        booleanParam(defaultValue: true, description: '', name: 'Build')
        booleanParam(defaultValue: true, description: '', name: 'Publish')
    }

    triggers 
    {
        githubPush()
    }

    stages 
    {
       stage('Build') 
       {
        steps
        {
              script
              {
                if(params.Build)
                {
                    dir('CoreDocker')
                    {
                        sh label: 'Project Building', script: 'dotnet build CoreDocker.sln'
                    }
                }
              }
            
        }
       }
       stage('Publish') 
       {
        steps
        {
                script
                {
                    if(params.Publish)
                    {
                        dir('CoreDocker/CoreDocker')
                        {
                            sh label: 'Docker Publishing', script: 'docker-compose up -d'
                        }
                    }
                }
            }
        
        }
    }
}