#  Exercice 1 : Variable d’environnement :
![image](https://user-images.githubusercontent.com/113101795/190332813-687deb7d-8d1e-456c-918e-cfc3a07cb04e.png)

1/ Les commandes tapées par l’utilisateurs sont stockées sur : /home/User/.bash_history  
  
2/ La variable $HOME  
  
3/  
$LANG est la variable qui stocke la langue courante.  
$PWD est la variable qui contient le chemin courant.  
$OLDPWD l'ancien chemin courant.  
$SHELL le chemin vers la commande shell.  
$_. contient tous les noms de fichier absolu du shell ou du script qui a été exécuter.  
  
4/  
`variable=test  `  
`set | grep variable  `  
` variable=test  `  
  
5/  La commande bash créer un fil au terminal, vue que variable n'est pas une variable global, elle n'est pas transféré.  
  
6/export variable=test  

7/  ![image](https://user-images.githubusercontent.com/113101795/190334656-3e578f53-e50e-4dd9-9cda-d76e5d5d842c.png)  
  
8/  ![image](https://user-images.githubusercontent.com/113101795/190335004-408100cb-b1d0-4fbe-9026-5068eb72fd37.png)  
  
9/	La commande unset détruit la variable  
  
10/![image](https://user-images.githubusercontent.com/113101795/190335206-a1e19a00-acf6-4257-bdd8-f44bcd9bd015.png)  
  
# Exercice 2 : Contrôle de mot de passe :
Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au
contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par
l’utilisateur ne doit pas s’afficher.  
```bash
#!/bin/bash

mdp='123+aze'

echo -n "mdp"
echo -e ""
read -s mdpentre

if [ "$mdpentre" = "$mdp" ]; then
        echo -e "mdp bon"
else
        echo -e "not good sussy boy"

fi
```
Dans le cas d'un mdp exact :  
![image](https://user-images.githubusercontent.com/113101795/190340369-a1c638da-33e1-48ac-aff3-e8b8ba5c3637.png)  
Dans le cas d'un mauvais mdp :  
![image](https://user-images.githubusercontent.com/113101795/190340935-53d6fddd-6d03-4133-8c9a-4590502f2243.png)  
  
#  Exercice 3 : Expressions rationnelles :
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètre
est un nombre réel : 

```bash
function is_number() 
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1  
    else 
        return 0 
    fi 
}
```

Il affichera un message d’erreur dans le cas contraire.
```bash
#!/bin/bash

if [ "$1" == "" ]; then
        echo "Saisir quelque chose:"
        exit 1
fi


function is_number()
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $1 =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

is_number $1

if [ $? != "1" ]; then
        echo "C'est un nombre"
else
        echo "Ce n'est pas un nombre"
fi
```
![image](https://user-images.githubusercontent.com/113101795/190352544-b509b482-4b5b-4117-b951-2203e3de8daf.png)

# Exercice 4. Contrôle d’utilisateur  
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le
script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”,
où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre
script, le message doit changer automatiquement)  

```bash
#!/bin/bash
read -p "Veuillez entrer votre nom d'utilisateur ici : ? " new_user
id -u "$new_user"> /dev/null 2>&1
if [ "$?" == "0" ]; then
    echo "utilisateur valide"
else
    echo "votre nom d'utilisateur n'est pas valide."
fi
```

# Exercice 5. Factorielle
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que
l’utilisateur saisit toujours un entier naturel).

```bash
#!/bin/sh 
#fonction factoriel
 
fact() { 
        n=$1
         if [ $n -eq 0 ]; then 
                echo 1 
         else 
                echo $(( n * `fact $(( n - 1 ))` )) 
         fi     

}
echo `fact $1`
```  
# Exercice 6. Le juste prix  
Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner.
Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).  
```bash
#!/bin/bash
chiffre=$(((RANDOM % 1000) +1))
read proposition
tentative=0


while test "$proposition" != "$chiffre"

        do
                if [[ $proposition =~ ^[0-9]+$ ]]
                        then
                                if test $chiffre -gt $proposition 
                                  then
                                  ((tentative++))
                                  echo "C'est plus"
                                elif test $chiffre -lt $proposition 
                                  then
                                  ((tentative++))
                                  echo "C'est moins"
                                elif test $proposition -eq $proposition
                                        then
                                        ((tentative++))
                                        echo "Mettre un chiffre"
                                else 
                                        echo "Mettre un chiffre"
                                fi
                        read proposition
                        else 
                                echo "Mettre un chiffre"
                                read proposition
                fi
        done

if test $chiffre -eq $proposition
        then
        echo "Bravo vous avez trouvé en $tentative essaies"
fi
```
```
root@localhost:/home/User# ./justeprix.sh 
40
C'est plus
0
C'est plus
Mange tes morts, mets un chiffre
14
C'est plus
50
C'est plus
600
C'est moins
400
C'est moins
200
C'est plus
300
C'est plus
350
C'est moins
310
C'est plus
325
C'est plus
335
C'est moins
333
C'est plus
334
Bravo vous avez trouvé en 13 essaies
root@localhost:/home/User# 
```
# Exercice 7. Statistiques
1. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max
et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres
sont bien des entiers.
```bash
#!/bin/bash

if [ $# -ne 3 ]; then
        echo -e "veuillez rentré 3 chiffre/nombre\n"
        exit 1
fi

function is_number() 
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1  
    else 
        return 0 
    fi 
}

moyenne=0
max=0
min=0
i=1

for var in "$@"; do
        is_number $var
        if [ $? == "1" ]; then
                echo $var "n'est pas un nombre"
                exit 1
        else
                if [ $i -eq 1 ]; then
                        min=$var
                        max=$var
                        moyenne=$((moyenne + $var))
                else
                        if [ $var -lt $min ]; then
                                min=$var
                        elif [ $var -gt $max ]; then
                                max=$var
                        fi
                                moyenne=$((moyenne + $var))

                fi
        fi
                i=$((i + 1))
done

i=$((i - 1))
moyenne=$((moyenne / $i))

echo min : $min
echo max : $max
echo moyenne : $moyenne                        
```