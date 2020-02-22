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
                        sh label: 'Project Building', script: 'sudo dotnet build CoreDocker.sln'
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
                        dir('CoreDocker')
                        {
                            sh label: 'Docker Publishing', script: 'sudo docker-compose up -d'
                        }
                    }
                }
            }
        
        }
    }
}