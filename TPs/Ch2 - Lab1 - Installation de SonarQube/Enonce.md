# Installation de SonarQube
On va utiliser Sonarkube. Ca sous entend l'installation du serveur sonar et la configuration de l'agent Sonar

### Démarrage du serveur sonar conteneurisé :
Tapez la commande suivante : 

```
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
```

Il y aura téléchargement de l'image docker, ensuite lancement du conteneur. Il sera en écoute sur le port **9000** de l'IP machine.
![Launch SonarQube](Images/Lancement%20du%20conteneur%20SonarQube.png)
