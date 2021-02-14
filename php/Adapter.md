# <div align='center'> Patterns Adapter </div>

* Il est utilisé pour transformer une interface étrangère en une interface commune. Supposons que dans le projet, vous récupérez les données d'un stockage en utilisant la classe suivante.

```php
classe Stockage {
    source $ privée ; 
    
    public function __constructor (AdapterInterface $source) { 
        $this->source = $source; 
    }
    public function getOne (int $id):? object { 
        return $this->source-> find ($id); 
    } 
    
    public function getAll (array $critères = []): Collection { 
        return $this->source-> findAll ($critères); 
    } 
}
```
* Notez que le stockage ne fonctionne pas directement avec la source mais à la place il fonctionne avec l'adaptateur de la source.

* De plus, le stockage ne sait rien des adaptateurs en béton. Il se réfère uniquement à l' interface de l' adaptateur . Ainsi, la mise en œuvre concrète de l'adaptateur fourni en est une boîte noire complète.

* Voici un exemple de l' interface de l' adaptateur

```php 
interface AdapterInterface { 
    public function find (int $id) :? object; 
    public function findAll (array $critères = []): Collection; 
}
```

* Maintenant, supposons que nous utilisons une bibliothèque pour accéder à la base de données MySQL. La bibliothèque dicte sa propre interface et elle ressemble à ceci:

```php 
$row = $mysql-> fetchRow (...); 
$data = $mysql-> fetchAll (...);
```

* Comme vous pouvez le voir, nous ne pouvons pas intégrer cette bibliothèque comme ça dans notre s torage . Nous devons créer un adaptateur pour cela comme ci-dessous:

```php 
class MySqlAdapter implements AdapterInterface {
    
     ...
     public function find(int $id) : ?object {
         
         $data = $this->mysql->fetchRow(['id' => $id]);
         // some data transformation
     }
     public function findAll(array $criteria = []) : Collection {
              
         $data = $this->mysql->fetchAll($criteria);
         // some data transformation
     }
   
     ...
}
```
* Après cela, nous pouvons l'injecter dans le storage comme ceci:

```php
$storage = new Storage(new MySqlAdapter($mysql));
```

### Si plus tard nous décidons d'utiliser une autre bibliothèque au lieu de celle-là, nous n'aurons qu'à créer un autre adaptateur pour cette bibliothèque, comme nous l'avons fait ci-dessus, puis injecter le nouvel adaptateur dans le stockage . Comme vous pouvez le voir, pour utiliser une bibliothèque différente pour obtenir les données de la base de données, nous n'avons pas besoin de toucher à un élément de la classe Storage . C'est la puissance du modèle de conception de l' adaptateur !