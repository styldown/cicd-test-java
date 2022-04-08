# Création d'un pipeline

### Multi-branch pipeline

Entrer l'url de votre projet GIT
Laisser les autres configurations par défaut

Enregistrer.
Le pipepline va échouer car aucun fichier Jenkinsfile n'existe dans notre projet.


###  Ecriture du pipeline 

!!! -- PENSER à remplacer main par master et ready par develop

SE DEPLACER SUR LA BRANCHE **m2ch4_OK** afin d'obserer le jenkinsfile.
```
git checkout m2ch4_OK
```

Le pipeline s'appuit sur des branches **master** et **develop**, et d'autres branch. On va donc les créer à partir de la branche m2ch4_OK

```
git checkout master
git checkout develop
```
Vérifier les noms des serveurs renseignés dans le jenkinsfile s'ils sont cohérents avec ceu déclarés dans la conf jenkins
- serveur sonnar : **localhost_sonarqube** dans le jenkinsfile (au lieu de sonarServer)
  - On le trouve dans "Manage Jenkins" ==> "Configuration globale des outils" ==> "Maven|Docker"
- mavenLatest au lieu de MavenLatest
- dockerlatest au lieu de DockerLatest
  - On le trouve dans "Manage Jenkins" ==> "Configure system" ==> "SonarQube servers"

Référence des variables Jenkins: https://opensource.triology.de/jenkins/pipeline-syntax/globals


### Fusioner la branche m2ch4 avec la branche develop

git checkout develop

git pull -r

git checkout m2ch4

git rebase develop

git checkout develop

git merge --no-ff m2ch4

