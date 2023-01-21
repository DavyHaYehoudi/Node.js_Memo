![middleware](/images/middleware.png)  


![middleware](/images/middleware2.png)  

5 catégories principales :  
1. Le Middleware d'application
C'est le plus courant. Il est relié directement à l'instance d'express grâce à la méthode `use()`

![cat1](/images/cat1.png)

2. Le Middleware du routeur  
Il n'est pas relié directement à l'instance d'express mais à l'instance d' `express.Router()`

3. Le Middleware de traitements d'erreurs  
![cat3](/images/cat3.png)  

Il doit prendre 4 arguments pour être identifié comme un middleware de traitements d'erreurs. Si l'on passe 3 arguments, Express considère qu'il s'agit d'un simple middleware et ne peut pas gérer les erreurs.  

4. Le Middleware intégré  
Historiquement, il existait quelques middlewares directement intégrés à Express un peu comme les modules déjà présents dans Node.js  
Depuis la version 4 d'Expres, il n'y a plus qu'un seul et unique middleware encore intégré à Express, il s'agit de `express.static()`.  
Ce middleware a comme responsabilité de servir des documents statiques depuis une API REST comme des images ou un PDF.  
Les autres middlewares auparavant intégrés dans Express sont toujours utilisables et maintenus par l'équipe derrière Express mais ils sont disponibles sous la forme de modules extérieurs qu'il faut installer.

5. Les Middlewares tiers  
Il s'agit de tous les middlewares disponibles sous la forme d'une dépendance extérieure. Ce sont des modules JS qu'il faut installer dans le dossier `node_modules` comme n'importe quelle autre dépendance de notre projet.

---

Pour récupérer les url de chaque requête Http, il existe un middleware qui s'appelle morgan. Très utile pour le deboggage :  
`npm install morgan --save-dev`  
```js
const morgan = require("morgan")
app.use(morgan("dev"))
```
Dans la console du terminal on peut voir :  

![morgan](/images/morgan.png)

---
Tous les middlewares sont interconnectés et communiquent entre eux. Pour cela, chaque requête de notre API REST est transmise au 1er midlleware de la chaîne puis celui-ci transmet la requête au middleware suivant et ainsi de suite jusqu'au point de terminaison de notre API REST. Ensuite, le mécanisme est identique pour la réponse Http mais dans le sens inverse.  
Les middlewares communiquent donc entre eux en se transmettant leurs paramètres respectifs.  

![comm](/images/comMiddlewares.png)