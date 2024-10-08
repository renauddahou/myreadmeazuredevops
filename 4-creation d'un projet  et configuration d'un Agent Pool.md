## Créez un projet dans Azure Devops Organizations 

![Texte alternatif](./images/r17.png)

![Texte alternatif](./images/r23.png)

![Texte alternatif](./images/r24.png)

![Texte alternatif](./images/r25.png)

## Créer son token

![Texte alternatif](./images/r31.png)

![Texte alternatif](./images/r32.png)

![Texte alternatif](./images/r33.png)

![Texte alternatif](./images/r34.png)



## Créez un Agent pool 

#### Cet agent pool sera installer sur notre serveur CI  VMtraining

![Texte alternatif](./images/r26.png)

![Texte alternatif](./images/r27.png)

![Texte alternatif](./images/r28.png)

### ``Les commandes suivante son à executer sur votre serveur CI en fonction de l'Os``

#### Sous WINDOWNS

![Texte alternatif](./images/r29.png)

### ``Téléchargement du binaire``

``az login``

``$url = "https://vstsagentpackage.azureedge.net/agent/3.225.0/vsts-agent-win-x64-3.225.0.zip"``

``$outputPath = "C:\Users\ASUS STRIX\Downloads\vsts-agent-win-x64-3.225.0.zip"``

``Invoke-WebRequest -Uri $url -OutFile $outputPath``





### ``Création de l'agent``
``PS C:\> mkdir agent ; cd agent``

``PS C:\agent> Add-Type -AssemblyName System.IO.Compression.FileSystem ; [System.IO.Compression.ZipFile]::ExtractToDirectory("$HOME\Downloads\vsts-agent-win-x64-3.225.0.zip", "$PWD")
``
### ``Configuration de l'agent``

``PS C:\agent> .\config.cmd``

``Entrez URL serveur > https://dev.azure.com/jfave-project/``

``Entrez type d’authentification (appuyez sur Entrée pour PAT) >``


``Entrez jeton d'accès personnel > ***************************************************``

``Entrez pool d'agents (appuyez sur Entrée pour default) >``

``Entrez nom de l’agent (appuyez sur Entrée pour DESKTOP-FTU31JP) >``

``Entrez dossier de travail (appuyez sur Entrée pour _work) > # ce dossier de travail sera créer automatique lors du premier job``

``Entrez exécuter l’agent en tant que service ? (O/N) (appuyez sur Entrée pour N) >``

``Entrez configurer l’ouverture de session automatique et exécuter l’agent au démarrage ? (O/N) (appuyez sur Entrée pour N) >``

### ``Exécutez éventuellement l'agent de manière interactive``

``PS C:\agent> .\run.cmd``






#### Sous LINUX

![Texte alternatif](./images/r30.png)

### ``Connectez-vou en SSH sur VMtraining``


``~/$ wget https://vstsagentpackage.azureedge.net/agent/3.225.0/vsts-agent-linux-x64-3.225.0.tar.gz``
    
``~/$ mkdir myagent && cd myagent``

``~/myagent$ tar zxvf ~/Downloads/vsts-agent-linux-x64-3.225.0.tar.gz``

``~/myagent$ ./config.sh``

``~/myagent$ ./run.sh``

![Texte alternatif](./images/r36.png)


```python

```
