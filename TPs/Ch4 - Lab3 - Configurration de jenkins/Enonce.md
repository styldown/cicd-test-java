# Configuration de Jenkins

Jenkins étant installé, nous allons le configurer.

#### Credentials Github et Dockerhub
```mermaid
graph LR
      A[Manage jenkins] ---> B[Manage credentials] ---> C[Global]---> Token
```
##### Github
![manage_jenkins_server](images/manage_jenkins.png)
![global](images/global.png)
![add_credentials](images/add_credentials.png)
![add_github_credentials](images/create_guthub_credentials.png)

##### Dockerhub
Repéter la meme opeation que celle faite pour github
![add_credentials](images/add_credentials.png)
![add_docker_credentials](images/create_dockerhub_credentials.png)


On a donc ceci : 
![credentials](images/credentials.png)

#### Configuration de Maven
![global_conf_tools](images/global_conf_tools.png)

![install_maven](images/install_maven.png)

#### Configuration de Maven

#### Docker
##### installation du plugin docker
![install_docker_plugin](images/install_docker_plugin.png)
![install_docker_plugin_2](images/install_docker_plugin_2.png)

On va en profiter pour installer d'autres plugin  : **SonarQube Scanner** par exemple
![install_docker_plugin_3](images/docker_and_sonnarQube_plugins.png)

Les plugins suivants seront aussi nécessaires : 
- **Email Extension Template**
  
##### Configuration  du plugin docker
Il faudrait à présent configurer le plugin docker: 
![global_conf_tools](images/global_conf_tools.png)
![docker_plugin_config](images/docker_plugin_config.png)

#### Configuration de Sonar
Rdv sur le serveur sonar à l'adresse suivante http://**<votre_ip>**:9000/documentation/analysis/jenkins/ et prendre connaissance de la configuration à mettre ne place.
![sonnar_doc](images/sonnar_doc.png)

- Dans sonnar, générer un autre token pour jenkins. On l'applelara **jenkins**
![sonnar_jenkins_token](images/sonnar_jenkins_token.png)
- Rajouter une credential dans jekins de type *secret Text*, qui aura comme valeur le token nouvellement généré.
![sonnar_token](images/sonnar_token.png)
![sonnar_token_2](images/credentials_2.png)
- Configuer le serveur sonarQube dans jenkins. l'url sera **http://host.docker.internal:9000** car les deux container ne sont pas dans le même réseau bridge
![Configure_system](images/Configure_system.png)
![add_sonar_to_jenkins](images/add_sonnar_to_jenkins.png)
![add_sonar_to_jenkins_2](images/add_sonnar_to_jenkins_2.png)

- Configurer un webhook dans sonar
  - nom :  **JenkinsWebhook**
  - url : **https://host.docker.internal:8080/sonarqube-webhook/**
 ![add_sonar_webhook](images/sonar_webhook.png)
 Ensuite cliquer sur create et cféer un nouveau webhook
 ![create_sonar_webhook](images/create_sonnar_webhook.png)
 On aura donc ceci : 
 ![finish_create_sonar_webhook](images/webhook_create_finished.png)

 #### Configuration des mails
 On va configurer l'envoie des mail, via une boite mail google
 ![Configure_system](images/Configure_system.png)
 Ensuite on va à la section des notification par email et on configure le serveur smtp
 ![configure_mail](images/configure_mail.png)
 Dans le cas de l'utilisation de google, pensez à desactiver la sécurité à l'adresse **https://myaccount.google.com/security**
 ![disable_google](images/disable_secure_google.png)