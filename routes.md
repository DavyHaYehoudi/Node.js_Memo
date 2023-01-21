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