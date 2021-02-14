# <div align='center'> The Singleton Pattern </div>


&nbsp;

### <p> Le modèle Singleton est donc connu car il restreint l'instanciation d'une classe à un seul objet. Les singletons diffèrent des classes statiques car nous pouvons retarder leur initialisation. généralement parce qu'ils nécessitent des informations qui peuvent ne pas être disponibles pendant le temps d'initialisation. Pour le code qui ne connaît pas une référence précédente à eux, ils ne fournissent pas de méthode pour une récupération facile. Jetons un coup d'œil à la structure de singleton: </p>

```javascript
var singletonPattern = (function() {
  var instance;
  function init() {
    // Singleton
    function privateMethod() {
      console.log('privateMethod');
    }
    var privateVariable = 'this is private variable';
    var privateRandomNumber = Math.random();
    return {
      publicMethod: function() {
        console.log('publicMethod');
      },
      publicProperty: 'this is public property',
      getRandomNumber: function() {
        return privateRandomNumber;
      }
    };
  }

  return {
    // Get the singleton instance if one exists
    // or create if it doesn't
    getInstance: function() {
      if (!instance) {
        instance = init();
      }
      return instance;
    }
  };
})();

// Usage:
var single = singletonPattern.getInstance();
```