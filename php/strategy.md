# <div align='center'> Pattern Strategy </div>


&nbsp;

* <p> Il est utilisé pour masquer les détails d'implémentation des algorithmes nécessaires pour effectuer une opération. Ayant des stratégies, le client peut choisir l'algorithme nécessaire sans connaître la mise en œuvre réelle et l'appliquer pour effectuer l'opération. </p>
<p> Disons que nous devons créer une bibliothèque qui transfère les données d'une source de données à une autre. Par exemple, nous devons transférer les données de la base de données vers le fichier csv ou de la feuille de calcul vers le fichier json . Comment feriez-vous cela? </p>
<p> Tout d'abord, nous devons créer des stratégies respectives pour lire les données des stockages. Appelons-les lecteurs . Ensuite, nous devons créer des stratégies respectives pour écrire les données dans les stockages. Appelons-les /*écrivains*/ . </p>
<p>Par conséquent, nous aurons 2 lecteurs pour lire les données de la base de données ou de la feuille de calcul . En conséquence, nous aurons 2 Writers pour écrire les données soit dans le fichier csv , soit dans le fichier json .</p>
<p> <strong>Important</strong>: le client qui travaillera avec nos stratégies ne doit pas se soucier de leurs implémentations. Par conséquent, nous devons également définir des interfaces pour nos stratégies. De cette façon, le client ne connaîtra que les méthodes définies par les interfaces de stratégie et ne travaillera qu'avec elles, et ce qui se passe en coulisse n'est pas son problème.</p>
<p>Enfin, nous devons créer le client qui sélectionnera les stratégies nécessaires en fonction de l'endroit et de l'endroit où il doit transférer les données.</p>

* Voyons tout cela en action:

```php 
interface ReaderInterface { 
    fonction publique start (): void; 
    public function read (): tableau; 
    public function stop (): void; 
}
interface WriterInterface { 
   fonction publique start (): void; 
   public function write (array $ data): void; 
   public function stop (): void; 
}
La classe DatabaseReader implémente ReaderInterface { 
    ... 
}
class SpreadsheetReader implémente ReaderInterface { 
    ... 
}
la classe CsvWriter implémente WriterInterface { 
    ... 
}
la classe JsonWriter implémente WriterInterface { 
    ... 
}
classe Transformer { 
    
    ...
    public function transform (string $ from, string $ to): void { 
        $ reader = $ this-> findReader ($ from); 
        $ écrivain = $ this-> findWriter ($ to); 
        
        $ reader-> start (); 
        $ écrivain-> start ();
        try { 
            foreach ($ reader-> read () as $ row) { 
                $ writer-> write ($ row); 
            } 
         } enfin { 
             $ écrivain-> stop (); 
             $ lecteur-> stop (); 
         } 
     }
     ... 
}
```

### Comme vous pouvez le voir, le transformateur qui est le client de nos stratégies ne se soucie pas vraiment des implémentations avec lesquelles il fonctionne. Tout ce qui compte, ce sont les méthodes définies par nos interfaces de stratégie.