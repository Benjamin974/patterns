# <div align="center"> Patterns Decorator </div>

* Il est utilisé lorsque vous souhaitez ajuster le comportement d'un objet au moment de l'exécution, et avec cela, réduire les héritages redondants et le nombre de classes.Vous pourriez vous demander pourquoi ai-je besoin de cela? Eh bien, cela pourrait être mieux expliqué avec des exemples.
* Disons que nous avons des classes Window et Door, et qu'elles implémentent toutes les deux OpenerInterface .

```php
interface OpenerInterface {
    public function open() : void;
}
class Door implements OpenerInterface {
    public function open() : void {
        // opens the door
    }
}
class Window implements OpenerInterface {
    public function open() : void {
        // opens the window
    }
}
```

* Les fenêtres et les portes ont le même comportement pour s'ouvrir . Maintenant, nous avons besoin d'autres portes et fenêtres avec des fonctionnalités supplémentaires qui indiqueront aux utilisateurs la température extérieure lorsqu'ils ouvrent les portes ou les fenêtres . Nous pouvons résoudre ce problème avec l'héritage comme ceci:

```php
class SmartOpener implements OpenerInterface  {
    
    private $opener;
    public function __construct(OpenerInterface $opener) {
        $this->opener = $opener;
    }
    
    public function open() : void {
        $this->opener->open();
        $this->temperature();
    }
}
$door = new Door();
$window = new Window();
$smartDoor = new SmartOpener($door);
$smartWindow = new SmartOpener($window);
```

* Nous avons introduit un nouveau type d' ouvreur qui agit comme un proxy mais avec une fonctionnalité supplémentaire en plus. C'est ça qui fait l'affaire.