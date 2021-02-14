# <div align="center"> Patterns Prototype </div>

* L'un des avantages de l'utilisation du modèle Prototype est que nous travaillons avec les atouts du prototype que JavaScript doit offrir de manière native plutôt que d'essayer d'imiter les fonctionnalités d'autres langages. Regardons l'exemple de modèle.

```javascript
var myCar = {
  name: 'bmw',
  drive: function() {
    console.log('I am driving!');
  },
  panic: function() {
    console.log('wait, how do you stop this thing?');
  }
};

//Usages:

var yourCar = Object.create(myCar);

console.log(yourCar.name); //'bmw'
```
