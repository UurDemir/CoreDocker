pipeline 
{
    agent any

    options 
    {
        disableConcurrentBuilds()
    }

    parameters 
    {
        booleanParam(defaultValue: true, description: '', name: 'Sonarqube')
        booleanParam(defaultValue: true, description: '', name: 'Build')
        booleanParam(defaultValue: true, description: '', name: 'Publish')
    }

    triggers 
    {
        githubPush()
    }

    stages 
    {
       stage('Sonarqube Begin') 
       {
        steps
        {
              script
              {
                if(params.Sonarqube)
                {
                    dir('CoreDocker')
                    {
                        sh label: 'Clean Sonarqube Folder' , script: 'rm -r .sonarqube || true'
                        sh label: 'Sonarqube Analyze Begin', script: 'dotnet sonarscanner begin /k:"CoreDockerProject" /d:sonar.host.url="http://144.91.102.128:9000" /d:sonar.login="5cfbf8a47ece0542af6b520a8cabb4658da000b9"'
                    }
                }
              }
            
        }
       }
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
       stage('Sonarqube End') 
       {
        steps
        {
              script
              {
                if(params.Sonarqube)
                {
                    dir('CoreDocker')
                    {
                        sh label: 'Sonarqube Analyze End', script: 'dotnet sonarscanner end /d:sonar.login="5cfbf8a47ece0542af6b520a8cabb4658da000b9"'
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