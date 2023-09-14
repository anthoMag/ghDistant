Mettre en place le mécanisme de partage du hook pre-commit :

Dans le répertoire ".git/hooks/"
- Ajouter un nouveau fichier nommé : "pre-commit"

- Ajoutez-y ce code entre les lignes
___________________________________

#!/bin/bash

info_file = "suivi/commitinfo.txt"

read -p "Souhaitez-vous enregistrer la date et l'heure du commit (y/n) ? " yn < /dev/tty
yn=${yn:n}

if ["$yn" == "y"]; then
	if [! -e "$info_file"]; then
		touch "$info_file"
	fi
	
	commit_date = $(git log -1 --format="%ci")

	echo "Commit vérifié le : $commit_date" >> "$info_file"

	git add "$info_file"

fi

exit 0
____________________________________


- Faire le commande "chmod +x pre-commit" dans le répertoire ".git/hooks" (va rendre le fichier exécutable)

- Créer le répertoire ".git/hooks/suivi/" (pour accueillir le nouveau fichier de suivi de commit)