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
            step('ASP.NET Core Building')
            {
              script
              {
                if(params.Build)
                {
                    sh label: 'Project Building', script: 'dotnet build'
                }
              }
            }
        }
       }
       stage('Publish') 
       {
        steps
        {
            step('ASP.NET Core Building')
            {
                script
                {
                    if(params.Publish)
                    {
                        sh label: 'Docker Publishing', script: 'docker-compose up -d'
                    }
                }
            }
        }
        }
    }
}