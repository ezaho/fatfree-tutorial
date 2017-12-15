# fatfree-tutorial
Fatfree est un framework pour php.

Commencez par télécharger fat free à partir du site officiel:

 https://fatfreeframework.com

N'hesitez pas à consulter "user guide" sur ce site.

Assurez-vous que la version de votre php peut supporter fatfree: au-delà de php 5.3

Placez fatfree dans le repertoire où vous comptez l'utiliser.Précisément,mettez dans votre répertoire-projet tout le contenu de fatfree.

Votre fatfree devrait contenir des dossiers et fichiers suivants :

              |_ lib
              |_ ui 
              |_ composer.ini
              |_ config.ini
              |_ .htaccess
              |_ index.php
              |_ readme 

Premier pas : "hello world!"

A chaque utilisation du command : $f3 c' est le framework fatfree qui s'exécute.

On veut afficher "hello world !" dans localhost à partir du fichier index.php

### Un peu de mise au point:

Allez dans index.php,ne gardez que les lignes de code suivantes ;les autres lignes vous pouvez les effacer :

           <?php

             $f3=require('lib/base.php');
             $f3->set('DEBUG',3);
             $f3->route('GET /',
                              function($f3) {      }
                              );
              $f3->run;  
Explication de ('DEBUG',3): 3 c'est le nombre d'erreur à afficher;Ne le remplacer surtout pas par 0;c'est pour les non-developpeurs. 

Ajoutez : echo"hello world!" dans la fonction :

                <?php

             $f3=require('lib/base.php');
             $f3->set('DEBUG',3);
             $f3->route('GET /',
                              function($f3) { echo"hello world!"     }
                              );
              $f3->run;  

Allez voir dans localhost; normalement vous devriez voir s'afficher "hello world!".

### pour aller plus loin:

Ajouter dans votre répertoire-projet les dossiers 'app' et 'assets' qui eux vont contenir chacun des sous-dossiers.

Et la structure de votre projet ressemble à ceci:

             |_ app
                        |_ Model
                        |_ Vue
                        |_ Controller 
             |_assets
                        |_ CSS
                        |_ js
                        |_img
                        |_fonts
              |_ lib
              |_ ui 
              |_ composer.ini
              |_ config.ini
              |_ .htaccess
              |_ index.php
              |_ readme 
### les variables globales set et get :

       $f3->set('name','value') :c'est la paire clé-valeur.
       $f3->get() :pour obtenir la valeur de la clé 'name'.
       exemple:
              <?php
                 $f3=require('lib/base.php');
                 $f3->set('message','voici ton livre');
                 $f3->route('GET /',
                                function($f3){
                                         echo $f3 get('message');
                                         }
                                   );
                 $f3->run()
                  ?>

### Routing basé par classe

Cette section est super importante. C'est le point où vous pouvez passer de la programmation par fonction à la POO . Sans le routing basé sur la classe, nous ne serions pas en mesure de créer le projet MVC que vous verrez dans ce tutoriel.

On va changer la fonction de routing en classe de routing :

c'est à dire le 2ème argument dans $f3->route( , ) est à changer.

                 <?php
                 $f3=require('lib/base.php');
                 class Main {
                          function render (){
                                    echo"voici ton livre";
                                     }
                                }
                  $f3->route('GET /','Main->render');
                  $f3->run()
               ?>

Qu' avons nous fait ?Nous avons créé une classe appelée Main et dedans nous avons créé une methode appelée render .Et le 2ème argument de [$f3->route] à changer devient :'Main->render' .
