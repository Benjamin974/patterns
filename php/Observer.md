# <div align="center"> Patterns Observer </div>

* Il est utilisé pour informer le reste du système de certains événements à un certain endroit. Pour mieux comprendre les avantages de ce modèle, passons en revue deux solutions du même problème.
* Disons que nous devons créer du théâtre pour montrer des films aux critiques. Nous définissons la classe Théâtre avec la méthode présente. Avant de présenter le film, nous voulons envoyer des messages sur les téléphones portables des critiques. Ensuite, au milieu du film, nous voulons arrêter le film pendant 5 minutes pour permettre aux critiques de faire une pause. Enfin, après la fin du film, nous voulons demander aux critiques de laisser leurs commentaires.
* Voyons à quoi cela ressemblerait dans le code:

```php
class Theater {
   
    public function present(Movie $movie) : void {
       
        $critics = $movie->getCritics();
        $this->messenger->send($critics, '...');

        $movie->play();

        $movie->pause(5);
        $this->progress->break($critics)
        $movie->finish();

        $this->feedback->request($critics);
    }
}
```

* Cela a l'air propre et prometteur.
* Maintenant, après un certain temps, le patron nous a dit qu'avant de commencer le film, nous voulions également éteindre les lumières. De plus, au milieu du film quand il s'arrête, nous voulons montrer la publicité. Enfin, lorsque le film se termine, nous voulons lancer le nettoyage automatique de la pièce.
* Eh bien, l'un des problèmes ici est que pour y parvenir, nous devons modifier notre classe de théâtre , et cela enfreint les principes SOLIDES . En particulier, il rompt le principe ouvert / fermé . De plus, cette approche fera dépendre la classe de théâtre de plusieurs services supplémentaires, ce qui n'est pas non plus bon.
* Et si on retournait les choses. Au lieu d'ajouter de plus en plus de complexité et de dépendances à la classe de théâtre , nous répartirons la complexité à travers le système, et avec cela, réduirons les dépendances de la classe de théâtre en prime.
* Voici à quoi cela ressemblera en action:

```php
class Theater {
    
    public function present(Movie $movie) : void {
        
        $this->getEventManager()
            ->notify(new Event(Event::START, $movie));
        $movie->play();

        $movie->pause(5);
        $this->getEventManager()
            ->notify(new Event(Event::PAUSE, $movie));
        $movie->finish();

        $this->getEventManager()
            ->notify(new Event(Event::END, $movie));
    }
}
$theater = new Theater();
$theater
    ->getEventManager()
    ->listen(Event::START, new MessagesListener())
    ->listen(Event::START, new LightsListener())
    ->listen(Event::PAUSE, new BreakListener())    
    ->listen(Event::PAUSE, new AdvertisementListener())
    ->listen(Event::END, new FeedbackListener())
    ->listen(Event::END, new CleaningListener());
$theater->present($movie);
```

* Comme vous pouvez le voir, la présente méthode devient extrêmement simple. Il ne se soucie pas de ce qui se passe en dehors de la classe. Il fait simplement ce qu'il est censé faire et informe le reste du système des faits. Tout ce qui s'intéresse à ces faits peut écouter les événements respectifs, en être informé et faire ce qu'il a à faire.
* Avec cette approche, il devient également assez facile d'ajouter de la complexité supplémentaire. Tout ce que vous avez à faire est de créer un nouvel auditeur et d'y mettre la logique nécessaire.
* J'espère que vous avez trouvé le modèle Observer utile.

