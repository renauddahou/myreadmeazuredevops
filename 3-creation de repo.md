### Créer un repo github

![Texte alternatif](./images/referentiel.JPG)

### Création de token github

![Texte alternatif](./images/token1.png)
![Texte alternatif](./images/token2.png)
![Texte alternatif](./images/token3.jpg)

### ``Connectez-vous en SSH sur le serveur CI``

### `` ssh -i trainingVM_key.pem azureuser@51.145.93.152``

### Clonage du référentiel Azure sample



``https://renauddahou:token@github.com/renauddahou/neosofttrain.git``

``git clone https://github.com/Azure-Samples/msdocs-python-flask-webapp-quickstart.git``


``rm -rf msdocs-python-flask-webapp-quickstart/.git && rm -rf msdocs-python-flask-webapp-quickstart/.github``

``mv msdocs-python-flask-webapp-quickstart/*  neosofttrain/``


``git add .``

``git commit -m "Initial commit"``


``git push -u origin main``


#### Testons notre applications

``sudo apt install python3-pip``

``pip3 install -r requirements.txt``

``nano app.py``

``app.run(host='0.0.0.0')``




### Avant de faire tourner notre application un petit tour sur notre group de securité pour ouvrir le port 5000 pour flask

![Texte alternatif](./images/nsg.png)
![Texte alternatif](./images/nsg3.png)

``python3 app.py``

http://51.145.93.152:5000


![Texte alternatif](./images/hello.png)
