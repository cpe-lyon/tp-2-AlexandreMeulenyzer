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
 ![image](https://user-images.githubusercontent.com/113101795/190340275-3bf30d3d-b372-4a4d-b5ab-81f6efcdd934.png)  
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