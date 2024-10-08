## Amelioration de l'application

### ``Connectez-vous en SSH sur le serveur CI``

### `` ssh -i trainingVM_key.pem azureuser@51.145.93.152``

``cd msdocs-python-flask-webapp-quickstart``

``nano requirements.txt``
```
flake8
yapf
```



``nano Dockerfile``

```
FROM python:3.9

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY app.py requirements.txt /app/
ADD templates /app/templates
ADD static /app/static

RUN chmod -R 777 /app

RUN pip install --no-cache-dir -r requirements.txt


EXPOSE 8000

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "app:app"]
```


``git add .``

``git commit -m "update app"``

``git push -u origin master``


```python

```
