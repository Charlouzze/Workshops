# Workshop 3 - API GraphQL avec Prisma2

Dans ce workshop, nous allons voir comment créer des API GraphQL à l'aide de [Prisma2](https://www.prisma.io/), Nexus-Prisma et Apollo

## Step 0: initialisation

Toutes les informations requises pour installer les dépendances du workshop sont disponibles dans [SETUP.md](./SETUP.md)

## Step 1: Récupérer les utilisateurs

Créez à présent une fonction `getUsers`:
- Elle ne prend pas de paramètres
- Elle renvoie la liste de tous les utilisateurs de la base de données

*À vous de trouver comment...*  
> Indice #1: nodejs gère très bien l'affichage d'objets en console.  
> Indice #2: la variable `prisma` est un objet.  

## Step 2: Create - Read - Update - Delete

Vous avez vu comment fonctionnait à peu près la récupération de données avec prisma, à présent, vous allez mettre en place des fonctions classique de CRUD.

Créez la fonction `getPostsByUsers`:
- Elle prend en paramètres `authorId`, l'id de l'utilisateur dont on veut  récuperer les posts
- Elle renvoie la liste des posts de l'utilisateur demandé

Créez la fonction `addPost`:
- Elle prend en paramètres `title`, le titre du post et `email`, l'email de l'utilisateur qui sera l'auteur du post
- Elle ajoute le post dans la base de données
- Elle renvoie le post crée

Créez la fonction `removeUser`:
- Elle prend en paramètres `authorId`, l'id de l'utilisateur qui sera supprimé
  - Elle renvoie l'utilisateur qui a été supprimé

Créez la fonction `removePost`:
- Elle prend en paramètres `authorId`, l'email de l'utilisateur auteur du post et `postId`, l'id du post qui sera supprimé
- Elle renvoie le post qui a été supprimé

## Step 3: Apollo Server et Nexus

Prisma nous permet de récuperer des données dans la base de données, mais il nous faut par la suite permettre à un utilisateur de récuperer ces données. Nous utiliserons pour cela [GraphQL Nexus](https://nexus.js.org/) et [Apollo server](https://www.apollographql.com/docs/apollo-server/)


Il faut installer de nouveaux modules pour faire cela:

<Details><Summary><strong>Étapes d'installations de Apollo et Nexus</strong></Summary>

```sh
npm install graphql nexus-prisma apollo-server @nexus/schema
sudo npm install -g nodemon
```

Ensuite:
- copiez le dossier [src](./src) présent dans le repo dans votre dossier starter
- Changer dans votre `package.json` la ligne `"dev": "node ./script.js"` en `"dev": "nodemon ./src/server.js"` pour changer le fichier exécuté par la commande `npm run dev`

</Details>

Si par la suite vous lancez `npm run dev`, vous aurez une erreur, ce qui est normal. Pour que le server se lance correctement, dans `schema.js`, vous devez ajouter un `objectType` qui défini la tabe `Post`.  
Un exemple de la table `User` est présent dans le fichier

> [lien vers la documentation Nexus concernant les modèles](https://www.nexusjs.org/#/plugins/prisma?id=tmodel)

## Step 4: Mise en place du CRUD avec Nexus

Maintenant que vos modèles sont bien définits, vous pouvez mettre en place les manipulations de données vues à la Step 2, mais cette fois ci avec Nexus.

> [lien vers la documentation Nexus concernant le CRUD](https://www.nexusjs.org/#/plugins/prisma?id=tcrud)  
> Pour les différents champs requis, basez vous sur ce que vous voyez dans `schema.prisma`

Pour tester les query/mutations que vous allez mettre en place, vous pouvez vous rendre sur http://localhost:4000/ afin d'avoir un playground pour tester votre server

Créez les query suivantes:
- `getUsers`: renvoie la liste de tous les utilisateurs
- `getPosts`: renvoie la liste de tous les posts
- `getPostsByUser`: renvoie la liste des posts d'un utilisateur grâce à son `authorId`
- `getPublishedPosts`: renvoie la liste de tous les posts qui sont publiés

Créez les mutations suivantes:
- `signUp`: crée un utilisateur en précisant son `email` et son `name`
- `writeDraft`: crée un post avec un `title`, un `content` et l'`authorId` de son auteur. Par défaut il n'est pas publié.
- `publishDraft`: publie un post dont l'`id` est précisé
- `deletePost`: supprime un post dont l'`id` est précisé


## Authors
- [Paul Monnery](https://github.com/PaulMonnery/)
- [Naoufesse Berrada](https://github.com/nowlow/)
- [Cyril de Lajudie](https://github.com/Axoloot/)