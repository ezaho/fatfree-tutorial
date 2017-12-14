# fatfree-tutorial
Fatfree est un framework pour php

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

## pour aller plus loin:

Ajouter dans votrerépertoire-projet les dossiers 'app' et 'assets' qui eux vont contenir chacun des sous-dossiers.

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

