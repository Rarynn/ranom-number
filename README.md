# [ESGI] - Projet CI/CD

>- Léo STVENOT
>- Nathan PONCET

## Application : Random number
**Description de l'API Génératrice d'entier Aléatoire**

Cette API JavaScript est accessible depuis le port [3000](http://localhost:3000). 
Elle génère un entier aléatoire compris entre 1 et 100 et le renvoie au format JSON.

**Utilisation :**

- **Endpoint :** `http://localhost:3000`
- **Méthode :** `GET`

**Réponse :**
```json
{
  "min": 1,
  "max": 100,
  "random_number": 42
}
```

## Commandes
### Installation
```shell
npm install
```
### Lint
Lint du fchier [index.js](src/index.js)
```shell
npm run lient-index
```
Lint du fchier [test.js](test/test.js)
```shell
npm run lint-test
```
Lint du fichier [Dockerfile](Dockerfile)
```shell
hadolint Dockerfile
```
### Start
Démarre l'application sur le port [3000](http://localhost:3000)
```shell
npm run start
```
### Test
Test que le endpoint http://localhost:3000 renvoi bien un JSON ayant cette structure
```json
{
    "min": number,
    "max": number,
    "random_number": number
}
```
```shell
npm run test
```
## Docker
> Image : [youpidok/random-number](https://hub.docker.com/r/youpidok/random-number/tags)
### Build
```shell
docker build --rm -t random-number .
```
### Run
```shell
docker run --name random-number -p 3000:3000 -d random-number 
```
### Tag
```shell
docker tag random-number youpidok/random-number:tag
```
### Push
```shell
docker push youpidok/random-number:tag
```
## CI/CD
> Livrable : Image docker [youpidok/random-number](https://hub.docker.com/r/youpidok/random-number/tags)

> Github [Actions](https://github.com/YOUPIDOK/ranom-number/actions)

> Configuration du [workflow](.github/workflows/workflow.yml) 

### Intégration continu
Lors d'une **pull request**:
- Lint
- Test
- Build de l'image [youpidok/random-number](https://hub.docker.com/r/youpidok/random-number/tags)
### Déploiement Continu
Lors d'un **push/merge** sur la branch **main** :
- Lint
- Test
- Build l'image [youpidok/random-number](https://hub.docker.com/r/youpidok/random-number/tags)
- Push l'image [youpidok/random-number:latest](https://hub.docker.com/r/youpidok/random-number/tags) sur Docker Hub

### Livraison Continue
Lors d'un **push** de **tag** :
- Lint
- Test
- Build l'image [youpidok/random-number](https://hub.docker.com/r/youpidok/random-number/tags)
- Tag l'image [youpidok/random-number:tag](https://hub.docker.com/r/youpidok/random-number/tags)
- Push l'image [youpidok/random-number:tag](https://hub.docker.com/r/youpidok/random-number/tags) sur Docker Hub
- Génération des notes de [releases](https://github.com/YOUPIDOK/ranom-number/releases)