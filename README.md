# Projet-27
Le but du programme est, dans le cadre du développement de réseaux de chaleur, de pouvoir tracer un réseau à partir de bâtiments donnés, et d’afficher les valeurs nécessaires au dimensionnement de ce réseau (débit, diamètre des canalisations)

Le programme du projet permet d'afficher la carte interactive avec pour chaque nœud (et donc la route en amont), le débit la puissance et le diamètre de canalisations requis. Il prend en argument une ville, des adresses que l'on veut rajouter sur le réseau, et les coordonnées de la source. On peut également rajouter les bâtiments en indiquant leurs coordonnées ainsi que directement le débit nécessaire.

Les modules sont OSNMX pour analyser OpenStreetMap, pandas pour traiter les fichiers CSV de données, wkt pour pouvoir traduire les données encodées en WKT, et folium pour pouvoir afficher notre réseau sur une carte.

Certaines hypothèses sont faites : vitesse de l'eau dans les canalisations égale à 2 m/s (représente la limite haute), différence de température extérieur/intérieur de 26 degrés (correspond au "pire cas"), différence de température de l'eau au début et à la fin du réseau de 60 degrés.

Attention : les données importées de la BDNB au début du programme sont exclusives au département 93, pour tout changement de département, il faut importer les données de la BDNB de ce département.

Pour compléter les données manquantes, on utilise les données de l’arrêté DPE qui nous permettent de déduire des coefficients de transmission thermique en fonction de la période de construction et du type de chauffage du bâtiment.

Le modèle physique nous permettant de calculer le débit nécessaire pour chaque bâtiment est statique, ce qui est contraire à la réalité qui serait plus décrite par un modèle dynamique.

Pour construire le réseau, on associe d’abord chaque adresse au nœud du graphe de OpenStreetMap le plus proche de lui, puis on trace le réseau entre ces nœuds avec Dijkstra. On se débarrasse des nœuds sans intérêt du réseau et à partir du débit nécessaire de chaque adresse, par récursivité, on obtient le débit nécessaire à chaque nœud et donc le diamètre de la canalisation en amont du nœud sur le réseau.

Pistes d’amélioration : « automatiser » encore plus le process, on est ici obligé de retélécharger des donnés si on veut changer de département, et on peut parfaire le tracé du réseau qui a certains endroits, n’est pas très conforme à ce qui est fait en réalité : le tracé du réseau pour un nœud ne prend pas en compte le tracé du réseau pour les autres nœuds.
