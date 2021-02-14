# <div align='center'> pattern Factory </div>


&nbsp;

* <p> Vous devez utiliser les usines lorsque vous voulez construire un objec t . C'est vrai - construire et non créer . Vous ne voulez pas avoir une usine juste pour créer un nouvel objet. Lorsque vous créez l'objet, vous le créez d'abord, puis vous l'initialisez. Habituellement, il nécessite d'effectuer plusieurs étapes et d'appliquer une certaine logique. Avec cela, il est logique d'avoir tout cela au même endroit et de le réutiliser chaque fois que vous avez besoin d'avoir un nouvel objet construit de la même manière. En gros, c'est le but du modèle d' usine .
</p>

* <p> C'est une bonne idée d'avoir une interface pour votre usine et que votre code dépende d'elle et non d'une usine concrète. Avec cela, vous pouvez facilement remplacer une usine par une autre chaque fois que vous en avez besoin. </p>

```php
interface FriendFactoryInterface { 
    fonction publique create (): Friend 
}
```
* Ensuite, nous implémentons notre interface d'usine avec la classe suivante:

```php 
La classe FriendFactory implémente FriendFactoryInterface {
    public function create (): Friend { 
        
        $ friend = new Friend ();
        // initialisez votre ami
        return $ ami; 
    } 
}
```
## C'est un modèle de conception assez simple et pourtant puissant!
