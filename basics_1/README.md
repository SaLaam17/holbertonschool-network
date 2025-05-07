README.md pour le projet Networking basics #1.
📌 L'intérêt de l'exercice "Change Your Home IP"
Cet exercice a plusieurs objectifs pédagogiques et pratiques liés aux réseaux et à la gestion des noms de domaine sur un serveur Ubuntu. 🚀

📌 1️⃣ Comprendre la résolution des noms avec /etc/hosts
✅ localhost et facebook.com sont des noms de domaine → habituellement résolus via DNS. ✅ Le fichier /etc/hosts permet de forcer la résolution locale, sans passer par un serveur DNS. ✅ Modifier /etc/hosts peut être utilisé pour : 🔹 Rediriger un domaine vers une adresse IP différente. 🔹 Simuler un serveur spécifique pour le développement. 🔹 Tester une configuration réseau sans toucher aux DNS globaux.

👉 Dans cet exercice, tu modifies localhost pour qu'il pointe vers 127.0.0.2 au lieu de 127.0.0.1. 👉 Tu rediriges également facebook.com vers 8.8.8.8, qui est l'IP d'un serveur DNS de Google.

📌 2️⃣ Apprendre à manipuler les fichiers système sur Linux
✅ Le fichier /etc/hosts est un fichier système protégé, donc le script doit être exécuté avec sudo. ✅ En modifiant /etc/hosts, tu pratiques les permissions et la gestion des fichiers critiques. ✅ Cela permet de mieux comprendre l’organisation des fichiers réseaux sur Linux.

📌 3️⃣ Contrôler la résolution des noms pour le test et le développement
💡 Pourquoi modifier facebook.com vers 8.8.8.8 ? ✅ Simuler un autre serveur en testant la redirection d’une URL vers une autre IP. ✅ Vérifier comment une application réagit si le DNS renvoie une adresse différente. ✅ Bloquer un domaine en le redirigeant vers une IP locale (127.0.0.1 peut être utilisé pour ça).

📌 4️⃣ Maîtriser les scripts Bash pour l’automatisation
✅ Tu écris un script qui applique ces modifications automatiquement. ✅ Cela t'apprend à manipuler les fichiers système via un script (au lieu de modifier /etc/hosts manuellement). ✅ Tu peux réutiliser ce principe pour d’autres scripts réseau (changer les DNS, configurer un proxy, etc.).

📌 5️⃣ Conséquences et précautions
💡 Attention : Modifier localhost peut casser certaines fonctionnalités. ✅ Certains services s’attendent à ce que localhost pointe toujours vers 127.0.0.1. ✅ Si un problème apparaît, tu devras restaurer /etc/hosts pour revenir à 127.0.0.1.

💡 Vérifier la modification avec ping :

bash
ping localhost
ping facebook.com
💡 Annuler la modification si besoin :

bash
sudo nano /etc/hosts
👉 Supprime ou modifie les lignes ajoutées, puis vide le cache DNS :

bash
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
🎯 Résumé rapide
✔️ Tu apprends à gérer la résolution des noms avec /etc/hosts. ✔️ Tu pratiques la manipulation des fichiers système sous Linux. ✔️ Tu simules une redirection d’IP pour des tests en développement réseau. ✔️ Tu automatise ces tâches avec un script Bash. ✔️ Tu apprends à anticiper les risques liés à la modification des fichiers réseau.


📌 L’intérêt de l’exercice "Show Attached IPs"
Cet exercice a plusieurs objectifs pédagogiques et pratiques en lien avec la configuration réseau et l'utilisation de scripts Bash. 🚀🔥

📌 1️⃣ Comprendre les adresses IP attachées à une machine
✅ Chaque machine connectée à un réseau possède une ou plusieurs adresses IP. ✅ Ces adresses peuvent être : 🔹 Locales (ex: 127.0.0.1 → loopback / localhost). 🔹 Privées (ex: 192.168.x.x ou 10.x.x.x → réseau interne). 🔹 Publiques (ex: l’IP attribuée par ton fournisseur d’accès). ✅ L’objectif de l’exercice est d’afficher uniquement les adresses IPv4 actives sur la machine.

📌 2️⃣ Apprendre à récupérer les informations réseau sous Linux
💡 Un serveur ou un ordinateur peut avoir plusieurs interfaces réseau (eth0, wlan0, lo, etc.). ✅ Ce script permet de récupérer les adresses IP associées à ces interfaces. ✅ Il enseigne comment manipuler les commandes réseau en Bash (ip, ifconfig, grep, etc.).

📌 3️⃣ Automatisation et administration système
✅ Plutôt que de taper manuellement une commande, le script automatise cette recherche. ✅ Cela permet à un administrateur de récupérer rapidement toutes les IPs actives sans devoir filtrer manuellement. ✅ Ce type de script peut être utile pour : 🔹 Surveiller un serveur et connaître ses IPs. 🔹 Faire des vérifications de configuration réseau. 🔹 Lister les IPs utilisées dans un environnement multi-interface.

📌 4️⃣ Tester sur différentes machines et comprendre les résultats
✅ Le résultat du script varie selon la machine sur laquelle il est exécuté. ✅ Exemple d’exécution sur un serveur avec plusieurs interfaces :

bash
192.168.1.45   # Adresse IP privée du réseau interne
10.0.0.8       # Adresse IP utilisée dans un VPN
127.0.0.1      # Adresse loopback (localhost)
✅ Exécution sur un PC simple connecté à un Wi-Fi :

bash
192.168.1.101  # IP privée attribuée par le routeur
127.0.0.1      # Loopback
💡 Chaque machine aura des IPs différentes selon son type de connexion !

📌 5️⃣ Maîtriser les outils Bash et réseau
🔥 Cet exercice te permet de découvrir et manipuler plusieurs commandes réseau utiles : ✅ hostname -I → Affiche les IPs associées à la machine. ✅ ip addr show → Affiche les interfaces réseau et leurs IPs. ✅ ifconfig (Ancienne méthode, toujours utilisée). ✅ Filtrage avec grep et awk → Extraire uniquement les adresses IPv4.

🎯 Résumé rapide
✔️ Afficher les adresses IPv4 actives sur une machine. ✔️ Comprendre la gestion des IPs et des interfaces réseau sous Linux. ✔️ Automatiser la récupération d’informations réseau avec Bash. ✔️ Tester sur différentes machines et analyser les résultats. ✔️ Améliorer ses compétences en administration système et en scripting Bash.


📌 L’intérêt de l’exercice "Port Listening on Localhost"
Cet exercice te permet de créer un serveur simple en Bash qui écoute sur le port 98, et d’utiliser telnet pour envoyer des messages à ce port. 🚀🔥

📌 1️⃣ Pourquoi apprendre à écouter un port ?
✅ Comprendre comment un programme écoute et accepte des connexions. ✅ Simuler un serveur TCP simple et recevoir des données. ✅ Tester les connexions réseau et le fonctionnement des sockets. ✅ Debugger des applications utilisant des ports spécifiques.

💡 Ce principe est utilisé dans de nombreux cas : 🔹 Serveurs web qui écoutent sur le port 80 (HTTP) ou 443 (HTTPS). 🔹 Services SSH qui écoutent sur le port 22. 🔹 Bases de données qui écoutent sur 5432 (PostgreSQL) ou 3306 (MySQL). 🔹 Applications réseau en développement pour tester la communication entre clients et serveurs.

📌 2️⃣ Comment réaliser l’exercice ?
💡 Créer un script Bash qui ouvre un serveur écoutant sur le port 98.

✅ 1. Crée le fichier 2-port_listening_on_localhost :

bash
touch 2-port_listening_on_localhost
chmod +x 2-port_listening_on_localhost
✅ 2. Écrire le script

bash
#!/usr/bin/env bash
# Script to listen on port 98 on localhost using netcat (nc)

echo "Listening on port 98..."
nc -l 98
✅ Explication du script :

nc -l 98 → nc (Netcat) ouvre un serveur qui écoute les connexions sur le port 98.

Il attend et affiche tout message reçu.

📌 3️⃣ Tester le script
✅ Dans un terminal (Terminal 0), démarre l'écoute sur le port :

bash
sudo ./2-port_listening_on_localhost
✅ Dans un autre terminal (Terminal 1), connecte-toi avec telnet et envoie un message :

bash
telnet localhost 98
👉 Tape un message (Hello world par exemple) et appuie sur Entrée.

✅ Retour dans Terminal 0, tu verras le message reçu :

bash
Hello world
📌 4️⃣ Alternative avec nc -lk pour écoute continue
💡 Le script de base ferme l’écoute après un seul message. Pour écouter en boucle :

bash
#!/usr/bin/env bash
echo "Listening on port 98..."
while true; do nc -l 98; done
✅ Avec cette version, le serveur restera actif après chaque message.

📌 5️⃣ Tester avec une connexion distante
🔥 Si tu veux tester entre deux machines sur un réseau : ✅ Sur le serveur (Machine A) :

bash
nc -l 98
✅ Sur le client (Machine B) :

bash
nc <IP_du_serveur> 98
👉 Tape un message et observe la communication réseau en temps réel ! 🎯
