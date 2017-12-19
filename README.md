# FatFree-tutorial
FatFree est un framework pour php.

Commencez par télécharger FatFree à partir du site officiel:

 https://fatfreeframework.com

N'hesitez pas à consulter "user guide" de fatfree :https://fatfreeframework.com/3.6/user-guide

Assurez-vous que la version de votre php peut supporter FatFree: au-delà de php 5.3

Placez FatFree dans le repertoire où vous comptez l'utiliser.Précisément,mettez dans votre répertoire-projet tout le contenu de fatfree.

Votre FatFree devrait contenir des dossiers et fichiers suivants :

              |_ lib
              |_ ui 
              |_ composer.ini
              |_ config.ini
              |_ .htaccess
              |_ index.php
              |_ readme 

Premier pas : "hello world!"

A chaque utilisation du command : $f3 c' est le framework FatFree qui s'exécute.

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
 
### Les méthodes 'beforeroute' et 'afterroute' :

Si vous ajoutez ces deux méthodes à votre classe ,fatfree les appellera automatiquement avant et après chaque appel de routing;il suffit de les utiliser telles quelles :'beforeroute' et 'afterroute'.

Ecrivez ce code et voyez dans localhost ce que ça donne:

               <?php
                      $f3=require ('lib/base.php');
                      $f3->set('DEBUG',3);
                      class maincontroller {   
                              function beforeroute (){
                                    echo"avant routing";
                                     }
                              function afterroute (){
                                    echo"après routing";
                                     }
                             function render (){
                                    echo"voici ton livre";

                                     }
                                }
                  $f3->route('GET /','maincontroller->render');
                  $f3->run();
               ?>

### Avançons vers la création d'un projet MVC

1-LA STRUCTURE DES DOSSIERS ET FICHIERS:

Comment créer un projet MVC avec FatFree ?

On aura une structure des dossiers et fichiers comme ceci:

                             |_ app
                                     |_ Model
                                                   |_
                                                   |_
                                                   |_
                                     |_ View
                                                  |_template.html
                                     |_ Controller
                                                  |_controller.php
                                                  |_maincontroller

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
                              |_route.ini

2-EXPLICATION:

Vous devriez créer les fichiers 'config.ini',route.ini' ,le dossier 'assets',et le dossier 'app' avec ses sous-dossiers 'model',view','controller' sans oublier leurs fichiers qui vont avec.

-'app' pour stocker le code source du projet.

-'index.php' est le fichier principal de notre application web.

-'routes.ini' est le fichier de configuration où nous stockons nos routes. Oui, nous déplaçons nos routes d'index.php à routes.ini .

-'config.ini' est le fichier où nous stockons nos variables config f3.

-'composer.json' est un fichier de configuration du gestionnaire de paquets PHP.

Le dossier 'controller' contient nos fichiers de contrôle,vos classes doivent résider dans un fichier dédié, une classe par fichier, où le nom du fichier et le nom de la classe sont exactement les mêmes.

3-LE CODE :

D'abord le 'C' ,comme controller de MVC, avec cet exemple de code que nous allons détailler après :

Avec cet exemple de code que nous allons détailler après :

               <?php
                    $f3=require ('lib/base.php');
                    $f3->set('DEBUG',3);
                    class controller{   
                              function beforeroute (){
                                    echo"avant routing";
                                     }
                              function afterroute (){
                                    echo"après routing";
                                     }
                     class maincontroller extends controller {
                                 function render(){
                                   echo"voici ton livre";
                                 }
                     class AboutController extends controller {
                                fonction render () {
                               echo 'Ceci est la page à propos de' ;
                                       }
                                      } 
                  $f3->route('GET /','maincontroller-> render' );
                  $f3->route('GET /about','AboutController->render');
                  $f3->run();
               ?>

Avec la classe controller, ce sera la classe parente de tous nos contrôleurs avec les mêmes méthodes beforeroute et afterroute.

Avec (class maincontroller extends controller) cela signifie que controller est la classe parente de maincontroller, c'est-à-dire que maincontroller héritera des méthodes et des variables de la classe controller.

AboutController sera notre controller ,un objet dans notre projet en MVC.

 4-D'autres codes des autres fichiers:

INDEX.php:

                      <? php
                             require_once ("vendor /autoload.php");

                             $f3 = Base :: instance ();

                             $f3->config('config.ini');
                             $f3->config('route.ini');

                        $f3->run(); 

Ce fichier contient l'inclusion de Composer autoload et l'initiation de l'instance f3.

Les lignes de code avec 'config.ini' et 'route.ini' indiquent à FatFree d'utiliser ces fichiers comme fichiers de configuration du système.C'est ainsi qu'on place les informations de configuration et de routage.

ROUTE.ini

                      [route]

                       GET / = maincontroller->render
                        GET / hello = maincontroller->sayhello

Ce fichier contient les définitions d'itinéraire. C'est la même information que nous avions l'habitude d'ajouter à nos fonctions $ f3-> route ().

le tag [routes] indique à FatFree que c'est la section où les routes sont définies. Ceci est important car vous ne pourriez avoir qu'un seul fichier pour tous vos besoins de configuration dans f3, dans ce cas vous sépareriez différentes sections de configuration avec des balises différentes. Vous verrez que notre config.ini commence par le tag [globals], car c'est là que nous définissons les variables globales.

CONFIG.ini

                                 [globals]
                                 DEBUG = 3
                                 UI = app/vues /
                                 AUTOLOAD = app/contrôleurs/ 

C'est le fichier de configuration des variables globales.

DEBUG spécifie le niveau de débogage de 0 à 3.

UI indique à f3 où rechercher les vues.C'est là que nous disons à f3 que nos vues résident sous notre répertoire app / views /

AUTOLOAD c'est ici que nous disons à f3 de trouver les classes de contrôleur sous app/controllers/ .

CONTROLLER.php 

                    <?php 
                    
                     class controller{
                          function beforeroute (){ 
                                echo"avant routing"; 
                                } 
                           function afterroute (){ 
                                echo"après routing";
                                }
                              }

La classe Controller est la superclasse de tous nos contrôleurs. Il implémente les fonctions beforeroute et afterroute. Ces fonctions seront disponibles dans tous les contrôleurs de l'application. 'beforeroute' est l'endroit idéal pour vérifier les informations de session.

MAINCONTROLLER.php

            <?php
               class maincontroller extends controller {
                  function render(){
                      $f3 -> set ('nom','monde');
                      $template = new Modèle ;
                          echo $template ->render ('template.htm');
                                 }
                           }

Ceci est notre classe de contrôleur principal. Sa classe parente est 'controller'. Nous avons déplacé les fonctions de 'index.php' d'avant dans cette classe.
'render' rendra la page principale.

Comment FatFree invoque-t-il ces fonctions de classe?

Tout commence dans index.php, où nous avons défini où trouver les fichiers de configuration. Les routes config pointent l'adresse '/' vers maincontroller-> render, donc f3 créera une instance de maincontroller et appellera la fonction render.

Comment f3 trouvera-t-il MainController? Basé sur l'entrée AUTOLOAD dans 'config.ini'.

Voyez omment ces fichiers et entrées sont liés.

Comment fonctionne le rendu visuel?

Nous avons défini une variable globale 'nom' pour avoir une valeur 'monde'. En utilisant des globales ,vous pouvez transmettre des variables qui seront utiliser dans des modèles .Nous passons une paire clé-valeur au modèle.

Ensuite, nous créons une instance de la classe Template de f3, qui fait partie du framework.

Ensuite, nous disons à f3 de rendre le modèle appelé 'template.htm'. f3 utilisera le réglage UI de l'interface utilisateur dans 'config.ini' pour trouver le modèle.

TEMPLATE.html

                 <!DOCTYPE html>
                 <html>
                 <head>
                      <title> page du tutoriel </title>
                 </head>
                 <body>
                        <p> Bonjour,!  </p>
                        <p> Ceci est rendu à partir du modèle </p>
                 </body>
                 </html> 

Si vous devez utiliser des variables fournies par les contrôleurs, vous devez ajouter vos variables en tant que variables globales dans le contrôleur et utiliser la syntaxe de modèle de f3 pour afficher ou utiliser ces valeurs. Vous pouvez transmettre tous les types de variables, ainsi que les tableaux et les objets aux modèles dans les variables globales. Vous devez utiliser des doubles accolades pour accéder aux globales. Les noms de variables doivent être précédés du symbole @ .Exemple {{ @nom }}.
