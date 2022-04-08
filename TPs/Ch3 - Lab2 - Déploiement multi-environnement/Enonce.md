# Déploiement  multi-environnement

L'idée ici est de créer une image docker de notre application et de lancer chaque environnement (dev, uat, pod) dans un conteneur dédié.
On peut le faire sur n'importe quelle machine qui comporte docker. Nous allons la faire sur notre VM AWS qui contient docker installé.

Il faudrait cloner notre repos git de travail. 

Sur la branche actuelle **m1ch3**, lancer le scan sonar

```
mvn sonar:sonar -s .m2/settings.xml -Dsonar.login=<token> 
```  
Est-ce OK pour vous ?

#### Conteneurisation de l'application java
Empaquetter l'application dans une image docker, on lui donnera comme nom  : **calculator-light:1.0.0**
```
docker build -t calculator-light:1.0.0 .
```  
#### Déploiement des différents environnements
A présent on peut tester la creation d'un container et le déploiement de nos environnements. Pour rappel : 
- DEV : **8090**
- UAT : **8091**
- PROD : **8092**
```  
docker run -d --name calculator-dev -p 8090:8090 --env SPRING_ACTIVE_PROFILES=dev  calculator-light:1.0.0
docker run -d --name calculator-uat -p 8091:8091 --env SPRING_ACTIVE_PROFILES=uat  calculator-light:1.0.0
docker run -d --name calculator-prod -p 8092:8092 --env SPRING_ACTIVE_PROFILES=prod  calculator-light:1.0.0
```  

