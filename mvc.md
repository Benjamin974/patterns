# <div align="center"> MVC </div>

## <div align="center"> But du mvc </div>


&nbsp;

* ### Au commencement du développement d’une application, tout part d’un fichier central. Très rapidement, votre application grossit et vous devez incorporer plusieurs éléments à votre codebase. Vos multiples interfaces vont devoir s’adapter aux actions des utilisateurs, les fonctionnalités vont se multiplier ainsi que les requêtes pour faire évoluer les données stockés en base.

* ### Votre code source qui était simple et dans lequel vous vous retrouviez facilement devient un plat de spaghetti 🍝 ! Plus celui-ci grandit, plus il deviendra difficile d’ajouter une fonctionnalité sans créer un dysfonctionnement dans une autre déjà existante. C’est ce qu’on appelle une régression. Sans une organisation standard de votre codebase, débugger deviendra une tâche longue et pénible. Collaborer avec un autre développeur sur votre projet demandera une assistance constante de votre part.

* ### C’est pour éviter ces handicaps que le MVC a été mis en évidence et proposé comme un pattern d’architecture.


&nbsp;
## <div align="center"> Le pattern MVC est une façon d’organiser un code source autour de trois piliers: </div>  


&nbsp;

1. Le Model qui représente la structure des données. Leur définition ainsi que les fonctions qui leurs sont propres et qu’elles peuvent avoir. Ce module est complètement décoléré du code métier ou de l’affichage de telle sorte à ce que la modification de la logique ou de l’interface n’affecte pas la structure des données.

2. La View (ou les vues) représente l’interface graphique à livrer au client qui en fait la requête. Avoir le code lié à l’interface isolé de la logique métier ou des données permet de faire des modifications à l’interface graphique sans avoir à se soucier de casser du code métier ou la structure des données.

3. Le(s) Controller(s) sont au coeur de la logique metier de votre application. Ils se situent entre les vues et le model. Les requêtes qu’un client va faire depuis l’interface graphique, la view, va être dirigée vers un controller qui sera en charge de manipuler les données dont il a besoin avec la brique Model, la traiter suivant le besoin métier, puis ordonner à la view de répondre au client avec les bons éléments.