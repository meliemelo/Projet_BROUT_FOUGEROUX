Guide d'installation et d'utilisation du script Python
Ce document explique comment configurer, exécuter et interpréter le script Python pour traiter vos données, générer des graphiques et des fichiers de synthèse.

Étape 1 : Pré-requis
1.	Installation de Python :
Assurez-vous que Python (version 3.13 ou supérieure) est installé sur votre ordinateur.
Téléchargez-le depuis le site officiel : python.org.
2.	Installation des bibliothèques nécessaires :
Le script utilise les bibliothèques suivantes :
o	matplotlib : Pour générer les graphiques.
o	pandas : Pour manipuler et analyser les données.
o	os : Pour gérer les fichiers et dossiers.
o	math : Pour les calculs mathématiques.
Installez les bibliothèques avec la commande suivante dans un terminal ou un invite de commande :
pip install matplotlib pandas

Étape 2 : Organisation des fichiers
1.	Structure du projet :
Créez un dossier principal pour organiser votre projet avec la structure suivante :
/votre_projet
├── main.py             # Le script Python
├── input/              # Contiendra votre fichier de données d'entrée
├── output/             # Contiendra les fichiers générés par le script
├── images/             # Contiendra les graphiques générés
2.	Ajout du fichier d'entrée :
Placez votre fichier CSV contenant les données dans le dossier input.
Par exemple : input/data_real.csv.

Étape 3 : Exécution du script
1.	Lancer le script :
Ouvrez un terminal ou un invite de commande, accédez au dossier où se trouve le fichier main.py et exécutez la commande suivante :
python main.py
2.	Résultats générés :
Une fois le script exécuté :
•	Les fichiers nettoyés et les statistiques seront disponibles dans le dossier output.
•	Les graphiques seront enregistrés dans le dossier images.

Étape 4 : Emplacement des résultats et des fichiers générés
1. Graphiques générés :
Vos graphiques seront enregistrés dans le dossier images avec les noms suivants :
•	images/fecal_live_bacteria_line_chart.png : Graphique en courbes des données fécales.
•	images/graph_cecal.png : Graphique en violon des données cæcales.
•	images/graph_ileal.png : Graphique en violon des données iléales.
2. Statistiques descriptives :
Les statistiques descriptives ne sont pas explicitement sauvegardées sous forme de fichier dans le code actuel. Cependant, vous pouvez les calculer manuellement avec les outils intégrés de Pandas après avoir chargé les données :
•	Exemple pour obtenir les statistiques de synthèse dans un tableau Pandas 
# Calculer les statistiques de synthèse groupées
summary = df.groupby(["treatment", "sample_type"]).agg(
    moyenne=('counts_live_bacteria_per_wet_g', 'mean'),
    ecart_type=('counts_live_bacteria_per_wet_g', 'std'),
    minimum=('counts_live_bacteria_per_wet_g', 'min'),
    maximum=('counts_live_bacteria_per_wet_g', 'max'),
    compte=('counts_live_bacteria_per_wet_g', 'count')
)
print(summary)

•	Si vous avez besoin des résultats pour un rapport ou une analyse manuelle, exécutez ce code dans un environnement interactif comme Jupyter Notebook ou un terminal Python.
3. Dossier de travail :
•	Votre script principal est à la racine du projet.
•	Les données d'entrée doivent être placées dans un dossier input.
•	Les graphiques générés seront enregistrés automatiquement dans le dossier images.

Étape 5 : Résolution des problèmes
•	Problème : Erreur lors de la lecture du fichier CSV.
Vérifiez que le fichier dans le dossier input est bien au format CSV et que les colonnes ont les noms attendus :
o	sample_type
o	mouse_ID
o	treatment
o	experimental_day
o	counts_live_bacteria_per_wet_g
•	Problème : Les graphiques ne s'affichent pas.
Vérifiez que les données sont suffisantes et contiennent des valeurs valides. Si les colonnes sont vides ou incorrectes, le script ignorera ces lignes.
•	Problème : Une bibliothèque est manquante.
Réinstallez les bibliothèques nécessaires avec :
pip install matplotlib pandas

Conclusion
Ce guide vous permet de mettre en place et d'exécuter facilement le script pour analyser vos données. Si vous suivez les étapes décrites, vous pourrez automatiser efficacement la génération de graphiques et de fichiers de synthèse à partir de vos données expérimentales.

Explication et analyse des graphiques 
	Le but de cette expérience est de traiter des groupes de souris avec un cocktail d’antibiotiques au début de leur vie et de voir l’impact que cela a sur le taux de bactérie au niveau du microbiote intestinale. Ainsi l’objectif est de réduire le nombre absolu de microbes intestinaux afin d’ouvrir les niches intestinales et d’augmenter l’efficacité de la colonisation intestinale de souris avec des communautés microbiennes définies, composées de microbes isolés et d’échantillon de sel.
Le déroulé de l’expérience est le suivant : Pendant leurs deux premières semaines de vie, les souris boivent de l’eau. En suite deux groupes se distinguent, le premier subira le traitement d’antibiotiques ABX et le deuxième groupe aura un placebo et sera donc le contrôle négatif afin de faire la comparaison. Les traitements commenceront à partir du 14ème jour de vie. Le traitement est donné jusqu’au 21ème jour, donc il a été donné pendant 7 jours et c’est à ce moment là que commence la phase de rinçage, phase où les traitements ne sont plus donnés. Tout au long du processus, des échantillons ont été prélevés à différents endroits. Par exemple, il y a eu des échantillons provenant de la matière fécale, provenant de l’iléal et du cæcum, qui sont respectivement la troisième partie de l’intestin grêle et la première partie du gros intestin. On a en suite illustré les résultats à travers 3 graphiques différents et d'un tableau.

On observe sur la figure 1, un graphique représentant la concentration de bactéries en fonction du temps pendant et avant le nettoyage. Ce graphique est une analyse de la matière fécale où vient les bactéries. On peut voir sur le graphique que pour le traitement ABX, lors du début de lise en place da traitement, il y a une diminution de la concentration en bactéries. Plus le traitement avance, plus la concentration en bactéries diminue. Durant la semaine de traitement, la concentration diminue en passant de 10 e10 bactéries/g de selle à 5,5 e10 bactéries/g de selle mouillée. Lors de la fin du traitement, la concentration en bactérie augmente passant de 5,5 e10 bactéries/g de selle mouillée à 9,5 e10 bactéries/g de selle mouillée. Cette concentration augmente pendant les deux premiers jours de nettoyage puis la concentration restée stable à partir Du 2ème jour de nettoyage.
Dans le cadre du traitement placebo, il y a une légère augmentation de la concentration en bactéries. Au début du traitement on passe de 9 bactéries/g de selle mouillée à 11 bactéries/g de selle mouillée. Puis après la concentration reste fixe et stable pendent la fin du traitement et le début du nettoyage.
On en déduit que le traitement antibiotique a un impact sur la concentration en bactéries, celui-ci détruit l’ensemble des bactéries et lorsque que la matière fécale n'est plus en présence d’antibiotiques, elle retourne à une concentration normale et stable ressemblant au contrôle négatif du placebo.

Dans figure 2, on observe un graphique représentant les bactéries vivant dans l’iléal. Ce graphique représente la concentration en bactéries par g en fonction du traitement. Le traitement au ABX montre une très faible quantité de bactéries environ 6 e10 bactéries/g alors que le traitement au placebo montre une quantité de bactéries peu stable, celle-ci est composé entre 6,5 e10 bactéries par gramme. En condition normale, l’iléal possède en moyenne moins de bactéries que la matière fécale. Les bactéries ne sont donc pas présente en grande quantité dans l’intestin grêle.

Dans la figure 3, on observe la concentration e bactéries dans le caecum en fonction du traitement. Pour le traitement ABX, la concentration en bactéries est faibles, environ 6 e10 bactéries par gramme.
Pour le traitement placebo, la concentration en bactéries est environ à 10,5 e10 bactéries par gramme 
Le caecum est donc constitué de beaucoup de bactéries.

Ainsi, l’ensemble de ces prélèvements ont permis de déduire que le traitement ABX permet la destruction partielle des bactéries du microbiote intestinal. La concentration de bactéries diminue environ de moitié à cause du traitement. La présence de bactéries la plus importante est dans le gros intestin au niveau du caecum.
Cette quantité de bactéries est transmise à la matière fécale qui possède une quantité de bactéries identique à celle du cæcum. Quant à l’intestin grêle, il possède moins de bactéries. Ainsi le cycle de décomposition En fonction du microbiote intestinal augmente la quantité de bactéries. Le traitement permet bien de réduire le nombre de microbes intestinaux par rapport au contrôle négatif à l’aide du placebo.
Il y a donc une augmentation de l’efficacité de la colonisation intestinale des souris grâce à l’ouverture des niches intestinales dû à la réduction des microbes intestinaux 
