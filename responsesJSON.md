```js
// On retourne la liste des pokémons au format JSON, avec un message :
app.get("/api/pokemons", (req, res) => {
  const message = "La liste des pokémons a bien été récupérée.";
  res.json(success(message, pokemons));
});

app.get("/api/pokemons/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const pokemon = pokemons.find((pokemon) => pokemon.id === id);
  const message = "Un pokémon a bien été trouvé.";
  res.json(success(message, pokemon));
});

//Ajouter un élément :
app.post("/api/pokemons", (req, res) => {
  const id = getUniqueId(pokemons);
  const pokemonCreated = { ...req.body, ...{ id, created: new Date() } };
  const message = `Le pokemon  ${pokemonCreated.name} a bien été créé `;
  res.json(success(message, pokemonCreated));
});

//Modifier un élément :
app.put("/api/pokemons/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const pokemonUpdated = { ...req.body, id };
  pokemons = pokemons.map((pokemon) => {
    return pokemon.id === id ? pokemonUpdated : pokemon;
  });
  const message = `Le pokemon ${pokemonUpdated.name} a bien été modifié `;
  res.json(success(message, pokemonUpdated));
});

//Supprimer un élément :
app.delete("/api/pokemons/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const pokemonDeleted = pokemons.find((pokemon) => pokemon.id === id);
  pokemons = pokemons.filter((pokemon) => pokemon.id !== id);
  const message = `Le pokémon ${pokemonDeleted.name} a bien été supprimé `;
  res.json(success(message, pokemonDeleted));
});
```

---

![schema](/images/respJSON.png)

Pour la réponse HTTP, il faut retourner les données au format JSON (et pas simplement des String).  
Le type MIME est nécessaire quand on utilise le protocle HTTP. On doit informer qu'on renvoie le format JSON. On ajoute dans une entête HTTP le type MIME.  
Pour info, quand on demande une page Web depuis le navigateur, le type MIME est également ajouté.  
Dans le cas du JSON, le type MIME est :  
`Content-Type : application/json`  
Dans le cas d'une simple page Web c'est :  
`Content-Type : text/html`  
Le code de statut enfin, il n'est pas présent dans la requête Http mais uniquement dans la réponse.

---

`Express` met à notre disposition de quoi convertir en JSON et renseigner le type MIME grâce à cette méthode :  
`res.json()`  
A noter donc que la méthode `json()` remplace la méthode `send()`

---

L'affichage de la réponse sur la page du navigateur (côté serveur) n'est pas très lisible :  
![respJson1](/images/respNav2.png)

Pour le rendre plus agréable, on peut utiliser une extension chrome dont la plus populaire est [Json Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) :  
 ![respJson2](/images/respNav1.png)

---

On utilise le CommonJS "success" du fichier helper.js :

```js
Fichier helper.js

exports.success = (message, data) => {
 return { message, data };
};
```

```js
Fichier app.js

const pokemon = pokemons.find(pokemon=>pokemon.id === id)
const message = "Un pokémon a bien été trouvé"
res.json(success(message,pokemon))
```

---
