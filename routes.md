Bonne pratique :  
Les url doivent toujours être écrites en minuscule et s'il s'agit de mots composés ils doivent être séparés par des traits d'union

---
Pour rendre dynamique un paramètre d'une url :

```js
app.get("/api/pokemon/:id", (req, res) => {
  const id = req.params.id;
  res.send(`Vous avez demandé le plémon n°${id}`);
});
```

Pour rendre dynamiques plusieurs paramètres d'une url :

```js
app.get("/api/pokemon/:id/:name", (req, res) => {
  const id = req.params.id;
  const name = req.params.name;
  res.send(`Le pokémon n°${id} est ${name}`);
});
```
Les paramètres de l'url sont systématiquement passés sous forme de String, donc si id = chiffre penser à utiliser `parseInt()` si l'id est de type Number dans la data.  
Avec Sequelize, inutile de s'en soucier notamment avec la méthode `findByPk` qui sait s'adapter.  

A ce niveau, on peut agir sur les ressources par un CRUD. Mais par rapport à la récupération des ressources c'est encore maigre puisqu'il n'y a que deux options :  
- Récupérer une unique ressource  
- Récupérer toute les ressources  

Pour une recherche avancée, par le nom, ou les 5 derniers ou triés par ordre alphabétique, il faut pousser Express plus loin.  
Grâce au protocole HTTP, il intervient un nouveau concept, il s'agit des QUERY PARAMS ou paramètres de requête.  
Concrètement, ce sont des paramètres que l'on peut ajouter à la fin de l'url de nos endpoints.  

![queryP](/images/queryP.png)

Pourquoi passer par des query params et non par des paramètres contenus dans l'url de la requête comme ci-dessous ?  

![queryUrl](/images/queryUrl.png)


La meilleure façon de structurer notre API REST est de respecter les deux règles suivantes :  

![queryOrparams](/images/queryOrparams.png)