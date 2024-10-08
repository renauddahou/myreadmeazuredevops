### Création d'un App Service

![Texte alternatif](./images/r61.png)
![Texte alternatif](./images/r62.png)
![Texte alternatif](./images/r63.png)
![Texte alternatif](./images/r64.png)
![Texte alternatif](./images/r65.png)
![Texte alternatif](./images/r66.png)
![Texte alternatif](./images/r67.png)
![Texte alternatif](./images/r68.png)

### Amlioration de notre pipeline pour déployer en App Service

![Texte alternatif](./images/r69.png)
```
- task: CmdLine@2
      displayName: 'Run as Appservice'
      inputs:
        script: 'az webapp deploy --name $APP_SERVICE_NAME --resource-group $RESOURCE_GROUP_NAME --src-path $(Build.ArtifactStagingDirectory)/app.zip'
           
```


```python

```
