# Trabajo Practico 5 - Felipe Cañas

## 4- Pasos del TP

## 4.1. Crear una cuenta en Azure

![Logo](./images/img1.png)

## 4.2. Crear un recurso Web App en Azure Portal y navegar a la url provista

![Logo](./images/img2.png)

![Logo](./images/img3.png) 

![Logo](./images/img4.png)

![Logo](./images/img5.png)

## 4.3. Actualizar Pipeline de Build para que use tareas de DotNetCoreCLI@2 como en el pipeline clásico, luego crear un Pipeline de Release en Azure DevOps con CD habilitada

![Logo](./images/img6.png)

![Logo](./images/img7.png)

![Logo](./images/img8.png)

![Logo](./images/img9.png)

## 4.4. Optimizar Pipeline de Build

El pipiline de build se encuentra optimizado en el .yml del punto anterior.

## 4.5. Verificar el deploy en la url de la WebApp /weatherforecast

![Logo](./images/img10.png)

## 4.6. Realizar un cambio al código del controlador para que devuelva 7 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio

![Logo](./images/img11.png)

![Logo](./images/img12.png)

![Logo](./images/img13.png)

## 4.7. Clonar la Web App de QA para que contar con una WebApp de PROD a partir de un Template Deployment en Azure Portal y navegar a la url provista para la WebApp de PROD.

![Logo](./images/img14.png)

![Logo](./images/img15.png)

![Logo](./images/img16.png)

## 4.8. Agregar una etapa de Deploy a Prod en Azure Release Pipelines

![Logo](./images/img17.png)

![Logo](./images/img18.png)

## 4.9. Realizar un cambio al código del controlador para que devuelva 10 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast se muestra lo mismo.

![Logo](./images/img19.png)

![Logo](./images/img20.png)

**WEBAPP:**

![Logo](./images/img21.png)

**WEBAPP-PROD:**

![Logo](./images/img22.png)

## 4.10. Modificar pipeline de release para colocar una aprobación manual para el paso a Producción.

![Logo](./images/img23.png)

## 4.11. Realizar un cambio al código del controlador para que devuelva 5 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast aun se muestra la versión anterior.

![Logo](./images/img24.png)

![Logo](./images/img25.png)

**WEBAPP:**

![Logo](./images/img26.png)

**WEBAPP-PROD:**

![Logo](./images/img27.png)

## 4.12. Aprobar el pase ya sea desde el release o desde el mail recibido.

![Logo](./images/img28.png)

![Logo](./images/img29.png)

## 4.13. Esperar a la finalización de la etapa de Pase a Prod y luego corroborar que en la url de la webapp_prod/weatherforecast se muestra la nueva versión coinicidente con la de QA.

![Logo](./images/img30.png)

![Logo](./images/img31.png)

## 4.14. Realizar un pipeline (no release) que incluya el deploy a QA y a PROD con una aprobación manual. El pipeline debe estar construido en YAML sin utilizar el editor clásico de pipelines ni el editor clásico de pipelines de release.

Creamos el pipeline, posteriormente damos permisos al usuario Felipe Cañas para realiazar aprovasiones desde el Enviroment. Por ultimo aprovamos el "Deploy to Production".

![Logo](./images/img32.png)

![Logo](./images/img33.png)

![Logo](./images/img34.png)

![Logo](./images/img35.png)

![Logo](./images/img36.png)

![Logo](./images/img37.png)

![Logo](./images/img38.png)

**WEBAPP:**

![Logo](./images/img40.png)

**WEBAPP-PROD:**

![Logo](./images/img39.png)

**Yaml:**

```
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

variables:
  solution: 'SimpleWebAPI.sln'
  buildPlatform: 'Any CPU'
  buildConfiguration: 'Release'
  ConnectedServiceName: 'Azure subscription 1 (390e02d3-f091-4607-896a-27733bbdabf4)' # Subscription ID
  WebAppKind: 'webApp'
  DevWebAppName: 'MyWebApp1' # QA WebApp name
  ProdWebAppName: 'MyWebApp1-PROD' # Production WebApp name

stages:
- stage: Build
  displayName: 'Build Application'
  jobs:
  - job: Build
    displayName: 'Build Application'
    steps:
      - task: UseDotNet@2
        inputs:
          packageType: sdk
          version: '8.x'  # Use the correct version of .NET
          installationPath: $(Agent.ToolsDirectory)/dotnet

      - script: |
          echo "Current directory: $(Build.SourcesDirectory)"
          cd $(Build.SourcesDirectory)
          ls -l
          dotnet restore $(solution)
        displayName: 'Restore NuGet Packages'

      - script: |
          dotnet build $(solution) --configuration $(buildConfiguration)
        displayName: 'Build Project'

      - script: |
          dotnet test $(solution) --configuration $(buildConfiguration)
        displayName: 'Run Unit Tests'

      - script: |
          dotnet publish $(solution) --configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory) --no-build
        displayName: 'Publish Project'
      
      - task: PublishBuildArtifacts@1
        inputs:
          pathToPublish: '$(Build.ArtifactStagingDirectory)'
          artifactName: 'drop'
          publishLocation: 'Container'
        displayName: 'Publish Build Artifacts'

- stage: DeployToQA
  displayName: 'Deploy to QA'
  dependsOn: Build
  condition: succeeded()
  jobs:
  - job: DeployToQA
    displayName: 'Deploy to QA'
    steps:
      - task: DownloadPipelineArtifact@2
        displayName: 'Download Build Artifacts'
        inputs:
          buildType: 'current'
          artifactName: 'drop'
          targetPath: '$(Pipeline.Workspace)/drop'

      - script: ls -l "$(Pipeline.Workspace)/drop"
        displayName: 'List Pipeline Workspace Content (QA)'

      - task: AzureRmWebAppDeployment@4
        displayName: 'Deploy to Azure App Service (QA)'
        inputs:
          azureSubscription: '$(ConnectedServiceName)'
          appType: 'webApp'
          WebAppName: '$(DevWebAppName)'
          package: '$(Pipeline.Workspace)/drop'

- stage: DeployToProd
  displayName: 'Deploy to Production'
  dependsOn: DeployToQA
  condition: succeeded()
  jobs:
  - deployment: DeployToProd
    displayName: 'Deploy to Production'
    environment: 'Production'
    strategy:
      runOnce:
        deploy:
          steps:
            - task: DownloadPipelineArtifact@2
              displayName: 'Download Build Artifacts'
              inputs:
                buildType: 'current'
                artifactName: 'drop'
                targetPath: '$(Pipeline.Workspace)/drop'

            - script: ls -l "$(Pipeline.Workspace)/drop"
              displayName: 'List Pipeline Workspace Content (Production)'

            - task: AzureRmWebAppDeployment@4
              displayName: 'Deploy to Azure App Service (Production)'
              inputs:
                azureSubscription: '$(ConnectedServiceName)'
                appType: 'webApp'
                WebAppName: '$(ProdWebAppName)'
                package: '$(Pipeline.Workspace)/drop'
```