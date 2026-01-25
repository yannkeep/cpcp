# **Rapport d'Audit Technique et Proposition d'Architecture : Refonte de l'Écosystème Numérique du CPCP vers un Intranet Sémantique Statique**

## **Résumé Exécutif**

Le présent rapport dresse un audit exhaustif de l'infrastructure web actuelle du *Centre Permanent pour la Citoyenneté et la Participation* (CPCP) et formule une proposition détaillée pour la création d'un nouvel intranet basé sur une architecture web statique ("Pure Web"). Dans un contexte où la souveraineté numérique et la pérennité de l'information deviennent des enjeux cruciaux pour les acteurs de l'éducation permanente, la dépendance actuelle aux systèmes de gestion de contenu dynamiques (WordPress) présente des risques croissants en termes de sécurité, de performance et de visibilité sémantique.

Notre analyse démontre que le corpus riche et interconnecté du CPCP — traitant de thématiques complexes telles que la violence institutionnelle, le droit au logement et la sobriété numérique — est actuellement sous-exploité par une structure technique rigide. Le passage à une architecture statique, hébergée sur GitHub Pages et propulsée par des technologies purement client-side (HTML5, CSS3, JavaScript Vanilla), offre une opportunité unique de transformer ce corpus en un "Knowledge Graph" (Graphe de Connaissances) vivant.

Cette transition permettra non seulement d'optimiser radicalement les performances web (Core Web Vitals) et la sécurité, mais surtout de positionner le CPCP comme une source d'autorité incontournable pour les nouveaux moteurs de recherche génératifs (GEO) et l'IA, garantissant ainsi que ses analyses politiques continuent d'éclairer le débat public dans les décennies à venir.

## ---

**Partie I : Audit Approfondi de l'Infrastructure et du Corpus Existant**

### **1.1 Analyse de la Dette Technologique et de l'Architecture WordPress**

L'infrastructure actuelle du site [cpcp.be](https://www.cpcp.be/) repose sur le CMS WordPress, une solution monolithique qui, bien que populaire, introduit une complexité technique disproportionnée par rapport aux besoins de publication d'un centre d'études. L'examen des marqueurs techniques révèle une architecture classique LAMP (Linux, Apache, MySQL, PHP) dont les limites structurelles freinent la diffusion optimale du savoir produit par l'association.

#### **1.1.1 Le Goulot d'Étranglement Dynamique**

Le modèle WordPress repose sur la génération de pages à la volée. Lorsqu'un utilisateur consulte une étude critique telle que *"Stratégies et luttes face à l’Autorité"* 1, le serveur doit interroger la base de données, récupérer le contenu, assembler les gabarits PHP, et exécuter les extensions avant de renvoyer le premier octet (TTFB). Cette "hydratation" serveur consomme des ressources de calcul inutiles pour un contenu qui, par nature, est statique une fois publié.2 Dans le contexte d'un trafic fluctuant lié à l'actualité politique, cette architecture est vulnérable aux ralentissements, voire aux interruptions de service, nuisant à l'accessibilité de l'information citoyenne.

De plus, la dépendance aux extensions (plugins) pour des fonctionnalités aussi basiques que le référencement ou la mise en page (probablement via des constructeurs de page lourds) injecte une quantité massive de code JavaScript bloquant dans le navigateur du visiteur. Les audits de performance web modernes, basés sur les signaux *Core Web Vitals* de Google 3, sanctionnent sévèrement ces délais d'interaction (INP \- Interaction to Next Paint), ce qui pénalise le classement du site dans les résultats de recherche. Pour une organisation promouvant la "sobriété numérique" dans ses propres publications 4, maintenir une telle empreinte numérique constitue une contradiction performative qu'une architecture statique permettrait de résoudre.

#### **1.1.2 Vulnérabilité et Souveraineté des Données**

En tant qu'acteur de la société civile traitant de sujets sensibles comme les violences institutionnelles ou la critique des politiques d'austérité 5, le CPCP doit considérer la sécurité de ses données comme une priorité absolue. WordPress, propulsant près de 43% du web, est la cible privilégiée des attaques automatisées. La présence d'une base de données SQL exposée et d'une interface d'administration /wp-admin accessible publiquement constitue une surface d'attaque permanente.6 Une compromission du site pourrait non seulement entraîner une perte de données, mais aussi une altération du contenu politique, portant atteinte à la crédibilité de l'institution. L'architecture statique proposée élimine radicalement ce vecteur d'attaque en supprimant la base de données et le traitement serveur : un site statique ne peut pas être "hacké" au sens traditionnel, car il n'y a rien à exécuter sur le serveur.

### **1.2 Audit Sémantique et Structurel du Corpus**

L'analyse de la structure de contenu actuelle révèle une organisation hiérarchique traditionnelle qui ne rend pas justice à la richesse transversale des travaux du CPCP. Le site fonctionne selon une logique de "blog" chronologique et catégorielle, cloisonnant les savoirs plutôt que de les relier.

#### **1.2.1 La Siloïsation du Savoir**

Le contenu est actuellement segmenté en grands silos hermétiques : *Analyses*, *Études*, *Billets d'humeur*, et revues comme *Tumult*.5 Cette taxonomie, bien que claire administrativement, échoue à capturer la complexité des sujets traités. Par exemple, l'étude n°53 sur l'autorité et le logement 1 est intrinsèquement liée à l'analyse n°504 sur l'adresse de référence et les droits des sans-abri.4 Actuellement, un utilisateur lisant l'une ne se voit pas proposer un chemin cognitif direct vers l'autre, sauf si un lien manuel a été inséré dans le corps du texte. Il manque une méta-structure, une ontologie qui permettrait de dire : "Ces deux documents, bien que de formats différents, traitent du concept *Droit au Logement* et mobilisent la notion de *Violence Administrative*."

#### **1.2.2 Le Problème du "Cimetière PDF"**

Un constat critique de cet audit est la dépendance excessive aux fichiers PDF pour la diffusion des contenus à haute valeur ajoutée. Les rapports d'activités, les numéros de la revue *Tumult*, et les *Cahiers du numérique* sont souvent proposés en téléchargement.4 Si le PDF est excellent pour l'impression, il est désastreux pour le web sémantique et l'expérience mobile.

* **Opacité pour les Moteurs de Recherche :** Bien que Google indexe le texte des PDF, il ne comprend pas leur structure sémantique (titres, citations, données). Les concepts clés enfouis dans un PDF sont invisibles pour les graphes de connaissances (Knowledge Graphs) des moteurs de recherche.7  
* **Rupture de Navigation :** Le PDF constitue un "cul-de-sac" navigationnel. L'utilisateur quitte l'interface du site, perdant le menu de navigation et les liens contextuels.  
* **Incompatibilité GEO :** Les nouveaux moteurs de réponse par IA (comme ChatGPT Search ou Perplexity) privilégient le contenu HTML structuré qu'ils peuvent analyser et synthétiser. Un corpus enfermé dans des PDF risque l'invisibilité dans ce nouvel écosystème informationnel.

### **1.3 Potentiel Inexploité des Thématiques Transversales**

Le site actuel met en avant quatre piliers thématiques forts : *Sociétés et Environnement*, *Cultures, Violences et Institutions*, *Lieux de vie et Espace public*, et *Médias et Actions citoyennes*.5 Ces piliers sont pertinents, mais leur implémentation technique est rigide. Les travaux d'auteurs prolifiques comme Boris Fronteddu ou Olivia Martou 4 traversent souvent ces frontières. Par exemple, une analyse sur la "Sobriété Numérique" touche à la fois à l'environnement et aux médias. L'architecture actuelle oblige souvent à choisir une catégorie principale, appauvrissant la découvrabilité.

L'audit suggère donc que le principal défi du CPCP n'est pas la production de contenu — qui est riche, régulier et pertinent — mais son architecture de l'information. Le passage à un intranet statique structuré en graphe permettra de briser ces silos et de révéler la densité intellectuelle des travaux du centre.

## ---

**Partie II : Proposition d'Architecture "Intranet Knowledge Graph"**

Pour répondre à l'exigence d'un "intranet complet en web statique ultra fonctionnel", nous proposons une rupture paradigmatique : abandonner la métaphore du "Magazine" pour celle du "Jardin Numérique" ou du "Graphe de Connaissances".

### **2.1 Philosophie "Pure Web" et Architecture JAMstack**

La proposition repose sur l'approche JAMstack (JavaScript, APIs, Markup), mais dans sa version la plus puriste et résiliente : sans dépendance à des API externes critiques lors du rendu. L'intégralité du site sera pré-générée en fichiers HTML, CSS et JS statiques.

* **Hébergement Souverain sur GitHub Pages :** Le code source et le contenu (en Markdown) seront hébergés sur GitHub.8 Cela garantit une versionnabilité totale : chaque modification d'une analyse politique est tracée, datée et attribuable, offrant une transparence radicale alignée avec les valeurs démocratiques du CPCP. L'hébergement est gratuit, supporte un trafic massif via CDN, et élimine les coûts de maintenance serveur.  
* **Indépendance Technologique :** En utilisant du "Pur HTML/CSS/JS", nous nous affranchissons des frameworks lourds (React, Angular) qui vieillissent mal. Un fichier HTML bien structuré écrit aujourd'hui sera encore lisible par les navigateurs dans 20 ans, assurant l'archivage pérenne des luttes et stratégies documentées par le CPCP.

### **2.2 Ontologie Politique et Modélisation des Données**

Au cœur de cet intranet se trouve une ontologie personnalisée. Au lieu de simples "articles", nous définirons des types de contenus riches dans le "Frontmatter" (métadonnées en en-tête des fichiers Markdown).9

#### **2.2.1 Les Entités du Graphe CPCP**

Nous structurerons le corpus autour de quatre entités interconnectées :

1. **Ressources (Publications) :** Études, Analyses, Billets d'humeur.  
2. **Agents :** Auteurs (ex: Anne-Sophie Gerard), Interviewés (ex: Adèle Pierre), Organisations citées.  
3. **Concepts :** Mots-clés structurants (ex: "Adresse de référence", "Smart City", "Désobéissance civile").  
4. **Événements :** Ateliers d'éducation permanente, Conférences, Campagnes (ex: "Campagne 2025 sur le Sans-abrisme").

#### **2.2.2 Exemple de Structure de Données (YAML Frontmatter)**

Chaque fichier Markdown commencera par un bloc de métadonnées rigoureux :

YAML

\---  
titre: "L'adresse de référence est-elle un droit?"  
type: "Analyse"  
id: "a504-2025"  
date\_publication: "2025-09-15"  
auteurs:   
  \- "Emma Raucent"  
intervenants:  
  \- "Adèle Pierre"  
concepts\_cles:  
  \- "Droit au logement"  
  \- "Administration"  
  \- "Précarité"  
themes\_piliers:  
  \- "Lieux de vie et Espace public"  
relations\_internes:  
  \- "e53-autorite-logement"  \# Lien sémantique vers l'Étude 53  
resume\_geo: "Cette analyse explore les barrières administratives limitant l'accès à l'adresse de référence pour les sans-abri en Belgique, se basant sur un entretien avec la chercheuse Adèle Pierre."  
\---

Cette structure transforme chaque document en un nœud de données, permettant à des algorithmes de générer automatiquement des liens contextuels : "Puisque vous lisez sur le *Droit au logement*, voici l'Étude n°53 sur *l'Autorité* et le profil de *Adèle Pierre*."

### **2.3 Visualisation Interactive et Fonctionnelle (Cytoscape.js)**

L'intranet ne sera pas qu'une liste de liens. Il intègrera une interface d'exploration visuelle propulsée par la librairie **Cytoscape.js** 10, exécutée côté client (dans le navigateur).

* **Cartographie des Luttes :** Une vue "Graphe" permettra de visualiser les connexions entre les thématiques. L'utilisateur pourra voir physiquement comment le concept de "Numérique" est relié à la "Démocratie" à travers les différents *Cahiers du numérique*.  
* **Navigation Exploratoire :** En cliquant sur le nœud "Olivia Martou", le graphe se réorganisera pour centrer toutes ses publications et les co-auteurs avec qui elle a travaillé, révélant des communautés de pensée au sein de l'institution.  
* **Implémentation Pure JS :** Contrairement à des solutions nécessitant un backend (comme Neo4j), ici le graphe est généré à la compilation du site sous forme d'un fichier JSON (knowledge-graph.json). Le navigateur charge ce fichier léger et Cytoscape.js assure le rendu interactif fluide, sans aucune requête serveur supplémentaire.11

### **2.4 Architecture de l'Intranet Privé**

Bien que GitHub Pages soit public par défaut, nous créerons une section "Intranet" sécurisée pour les documents internes (brouillons, mémos stratégiques, annuaires internes).

* **Sécurisation par Chiffrement Client (Staticrypt) :** Nous utiliserons **Staticrypt** 12 pour chiffrer les fichiers HTML de la section privée. Le contenu est stocké sous forme chiffrée (AES-256) sur le serveur public.  
* **Expérience Utilisateur :** Lorsqu'un membre du personnel accède à /intranet/, une page de connexion statique apparaît. En entrant le mot de passe, une clé de déchiffrement est générée localement dans le navigateur, et le HTML est déchiffré à la volée et injecté dans le DOM.  
* **Avantage :** Aucune gestion de session serveur, aucun cookie traçable, aucune base de données d'utilisateurs à pirater. C'est la solution de sécurité la plus robuste pour un hébergement statique public, idéale pour des documents confidentiels mais non "secret défense".

## ---

**Partie III : Optimisation Avancée (SEO, GEO et Web Sémantique)**

La refonte vise à anticiper les mutations du web, passant d'un référencement basé sur les mots-clés (SEO 1.0) à une optimisation pour les moteurs de réponse et l'IA (GEO \- Generative Engine Optimization).

### **3.1 Stratégie GEO : Écrire pour les Machines**

Les modèles de langage (LLM) comme ChatGPT ou Perplexity ne "lisent" pas comme des humains ; ils cherchent des faits, des consensus et des relations de causalité.14 Pour que les analyses du CPCP soient citées comme sources de référence par ces IA, nous structurerons le contenu spécifiquement pour elles.

#### **3.1.1 Le Format "Question-Réponse" (Q\&A)**

Chaque publication, en plus de son corps de texte, inclura un bloc \<details\> structuré contenant des paires Question-Réponse explicites.7

* *Exemple :*  
  * **Q :** Quels sont les impacts de la "Smart City" sur la participation citoyenne selon le CPCP?  
  * **R :** Selon l'analyse n°493 de Benoît Debuigne, la Smart City tend à programmer une obsolescence de l'espace public traditionnel, remplaçant la médiation humaine par une gestion algorithmique souvent discriminatoire.

Ce format maximise les chances d'apparition dans les "Featured Snippets" de Google et les réponses directes des chatbots.

#### **3.1.2 Citations et Autorité (E-E-A-T)**

Pour renforcer l'autorité (E-E-A-T : Experience, Expertise, Authoritativeness, Trustworthiness), chaque affirmation statistique sera balisée sémantiquement. Si une analyse mentionne que "180.000 personnes seront exclues du chômage" 4, ce chiffre sera encapsulé dans une balise HTML5 \<data value="180000"\> associée à une citation source précise. Cela permet aux IA d'extraire des "faits vérifiés" et de citer le CPCP comme la source primaire de cette donnée.

### **3.2 Web Sémantique et Schema.org**

Nous implémenterons une couche de métadonnées JSON-LD exhaustive, invisible pour l'utilisateur mais cruciale pour les machines.15

#### **3.2.1 Typologie Schema.org Adaptée**

Contrairement au site actuel qui utilise des balises génériques, le nouvel intranet utilisera des types spécifiques :

* **NGO** 17 : Pour définir l'entité CPCP, sa mission et sa zone d'action (Belgique).  
* **ScholarlyArticle** 18 : Pour les études et analyses. Ce type est essentiel pour l'indexation dans **Google Scholar** 19, permettant aux travaux du CPCP d'être reconnus comme littérature académique/grise légitime.  
* **EducationalOccupationalProgram** 20 : Pour le catalogue de formations. Cela permettra aux modules d'éducation permanente d'apparaître dans les carrousels de formations des moteurs de recherche.  
* **DefinedTerm** : Pour créer un dictionnaire politique en ligne. Chaque concept clé (ex: "Violence Institutionnelle") aura sa propre URI et définition structurée, positionnant le CPCP comme l'autorité définitionnelle sur ces termes.

### **3.3 Accessibilité et Sobriété Numérique**

L'optimisation technique servira aussi les valeurs de l'association.

* **Performance Carbone :** L'architecture statique réduit drastiquement la consommation énergétique (pas de calcul serveur à chaque visite). Les images seront converties automatiquement en formats modernes (AVIF/WebP) et chargées en "lazy-loading", réduisant le poids des pages de 70% par rapport au site WordPress actuel.2  
* **Accessibilité (A11Y) :** Le code HTML pur garantira une compatibilité parfaite avec les lecteurs d'écran pour malvoyants, un aspect souvent brisé par les extensions WordPress mal codées.

## ---

**Partie IV : Fonctionnalités Techniques de l'Intranet Statique**

Cette section détaille comment des fonctionnalités avancées ("Ultra Fonctionnel") sont implémentées sans serveur backend, en respectant la contrainte "Pur HTML/CSS/JS".

### **4.1 Moteur de Recherche "Edge" (Pagefind)**

La recherche est la fonction vitale d'un intranet documentaire. Les solutions dynamiques classiques (ElasticSearch) sont trop lourdes. Nous utiliserons **Pagefind**.21

* **Mécanisme :** Pagefind génère un index statique binaire lors de la construction du site. Lorsqu'un utilisateur tape "austérité", le navigateur ne télécharge que les fragments d'index pertinents (quelques kilo-octets), sans jamais interroger de serveur.  
* **Performance :** La recherche est instantanée, fonctionne hors ligne (si le site est en cache), et respecte la confidentialité (aucune donnée de recherche n'est envoyée au serveur).  
* **Capacités Avancées :** Pagefind gère nativement le filtrage par facettes (Auteurs, Thèmes, Année) 23, permettant de trier le corpus du CPCP avec la même puissance qu'un site e-commerce.

### **4.2 Gestion des Archives Volumineuses (Git LFS)**

Pour gérer les archives PDF historiques (si elles ne sont pas converties en HTML) et les rapports d'activités volumineux, nous utiliserons **Git Large File Storage (LFS)**.24

* Git LFS remplace les gros fichiers par des pointeurs légers dans le dépôt, stockant les fichiers réels sur un serveur blob optimisé.  
* Cela permet de maintenir le dépôt GitHub principal léger et rapide à cloner pour les développeurs, tout en offrant un accès transparent aux fichiers pour les utilisateurs.  
* *Note Stratégique :* Si le volume dépasse les quotas gratuits de GitHub (1GB de stockage/bande passante), nous couplerons cette solution avec **Cloudflare R2** 26, un stockage objet compatible S3 sans frais de bande passante (egress fees), assurant une scalabilité à coût quasi-nul pour l'association.

### **4.3 Tableaux de Bord de Données (Data Visualization)**

Pour les rapports d'activité internes, nous intégrerons des tableaux de bord interactifs en pur JavaScript (utilisant des bibliothèques légères comme Chart.js ou D3.js).

* Ces tableaux pourront visualiser les statistiques de fréquentation des formations, la répartition géographique des projets citoyens, ou l'évolution des thématiques traitées au fil des ans.  
* Les données seront stockées dans des fichiers JSON ou CSV simples dans le dossier /data/ de l'intranet, facilement éditables par le personnel via un tableur classique, puis committés sur le dépôt.

## ---

**Partie V : Feuille de Route de Migration et Mise en Œuvre**

La transition vers cette nouvelle architecture doit être progressive pour garantir la continuité de service.

### **5.1 Phase 1 : Extraction et Assainissement (Mois 1-2)**

1. **Exportation du Contenu WordPress :** Utilisation d'outils spécialisés 27 pour convertir tous les articles, pages et types de contenus personnalisés en fichiers Markdown.  
2. **Nettoyage Sémantique :** Développement de scripts pour nettoyer le HTML "sale" généré par WordPress (suppression des shortcodes, des balises de style en ligne) et normaliser la structure des titres.  
3. **Enrichissement des Métadonnées :** Une étape cruciale de curation humaine sera nécessaire pour taguer les anciens contenus selon la nouvelle ontologie (lier les études aux concepts et auteurs).

### **5.2 Phase 2 : Développement du "Générateur" (Mois 3\)**

Bien que le résultat soit du HTML pur, nous utiliserons un Générateur de Site Statique (SSG) comme **Eleventy (11ty)** pour automatiser la production des pages.28 Eleventy est choisi pour sa flexibilité et sa capacité à manipuler des données JSON complexes (le graphe) tout en produisant un code HTML extrêmement léger.

* Création des gabarits HTML sémantiques.  
* Configuration du pipeline de construction du Graphe de Connaissances.  
* Intégration de Staticrypt pour la section privée.

### **5.3 Phase 3 : Déploiement et Formation (Mois 4\)**

1. **Mise en place de CI/CD :** Configuration de **GitHub Actions** pour que chaque modification du contenu déclenche automatiquement une reconstruction et un déploiement du site.30  
2. **Interface d'Édition (CMS Headless) :** Pour permettre à l'équipe du CPCP (non technique) de continuer à publier sans apprendre le code, nous connecterons une interface comme **Decap CMS** (anciennement Netlify CMS) directement sur le dépôt GitHub. Cela offre une interface visuelle proche de WordPress, mais qui écrit des fichiers Markdown en arrière-plan.  
3. **Formation :** Session de formation de l'équipe à la rédaction "orientée GEO" (structuration des réponses, maillage interne) et à l'utilisation du nouvel intranet.

### **Conclusion**

La proposition d'un intranet statique hébergé sur GitHub Pages n'est pas une simple mise à jour technique ; c'est un acte de cohérence politique pour le CPCP. En s'affranchissant des lourdeurs et vulnérabilités de WordPress, l'association gagne en **indépendance**, en **sécurité** et en **performance**. Plus fondamentalement, en structurant son savoir sous forme de Graphe de Connaissances sémantique optimisé pour l'IA, le CPCP s'assure que ses analyses critiques sur l'autorité, la citoyenneté et la société continueront d'influencer le débat public dans le nouvel écosystème numérique qui s'annonce.

# ---

**Annexe Technique : Spécifications Détaillées des Composants**

## **Tableau 1 : Comparatif des Architectures (Actuelle vs. Proposée)**

| Caractéristique | Architecture Actuelle (WordPress) | Architecture Proposée (Statique / Jamstack) | Avantage Stratégique |
| :---- | :---- | :---- | :---- |
| **Sécurité** | Surface d'attaque élevée (SQL, PHP, Plugins). Nécessite des patchs constants. 6 | Quasi-inviolable. Pas de base de données, pas de code serveur exécutable. 2 | **Souveraineté** : Protection des données sensibles et des analyses politiques. |
| **Performance** | Lenteur (TTFB élevé). Dépend de la charge serveur. Risque de crash lors des pics de trafic. | Instantanée (CDN). Les fichiers sont pré-générés. Scalabilité infinie à coût nul. 31 | **Expérience Utilisateur** : Accès fluide même sur connexions mobiles faibles. |
| **Coût** | Hébergement mensuel (€€) \+ Maintenance (€€€). | Hébergement GitHub Pages (Gratuit/€) \+ Stockage objet bas coût. | **Sobriété** : Réallocation du budget vers la recherche plutôt que la maintenance technique. |
| **Pérennité** | Données enfermées dans une base SQL propriétaire. Difficiles à exporter proprement. | Données en fichiers texte (Markdown) universels. Archivage naturel via Git. | **Mémoire** : Garantie de lisibilité du corpus à long terme (10-20 ans). |
| **SEO / GEO** | Optimisation superficielle (Meta tags). Contenu souvent opaque pour les IA (PDF). | Optimisation structurelle profonde (Schema.org, HTML sémantique). Contenu "Machine-Readable". | **Visibilité** : Positionnement en tant qu'autorité pour les moteurs de réponse IA. |
| **Recherche** | Basique, lente, souvent imprécise. | Recherche instantanée, tolérante aux fautes, facettes dynamiques (Pagefind). | **Fonctionnalité** : Retrouver une info précise dans 10 ans d'archives en millisecondes. |

## **Tableau 2 : Matrice de l'Ontologie Politique du CPCP**

Ce tableau définit comment les concepts clés du CPCP seront modélisés dans le *Frontmatter* pour alimenter le Knowledge Graph.

| Entité (Concept) | Propriétés Métadonnées (YAML) | Type Schema.org Associé | Exemple de Valeur (Corpus CPCP) |
| :---- | :---- | :---- | :---- |
| **Étude / Analyse** | authors, date, related\_concepts, citation\_weight, summary\_geo | ScholarlyArticle | *Stratégies et luttes face à l’Autorité* (Étude n°53) |
| **Auteur / Expert** | name, affiliation, expertise\_areas, related\_works | Person | *Olivia Martou*, *Boris Fronteddu* |
| **Thème Pilier** | name, description, sub\_concepts | DefinedTermSet | *Sociétés et Environnement*, *Cultures et Violences* |
| **Concept Clé** | name, definition, synonyms, parent\_concept | DefinedTerm | *Violence Institutionnelle*, *Sobriété Numérique*, *Habitat Léger* |
| **Événement** | date, location, organizer, related\_resource | Event / EducationEvent | *Atelier Éducation Permanente 2025* |

## **Tableau 3 : Stack Technique "Pure Web" (Conformité GitHub Pages)**

| Composant | Technologie Choisie | Rôle dans l'Architecture | Justification "Ultra Fonctionnel" |
| :---- | :---- | :---- | :---- |
| **Générateur (Build)** | **Eleventy (11ty)** | Compile le Markdown en HTML. | Le plus flexible pour manipuler les données JSON du Graphe. Ne laisse aucune trace JS inutile côté client. 28 |
| **Langage Client** | **Vanilla JS (ES6+)** | Gestion de l'interactivité (Graphe, Auth). | Aucun framework à charger (pas de React/Vue). Performance maximale, poids minimal. |
| **Style** | **CSS3 (Grid/Flex) \+ Variables** | Mise en page responsive. | Maintenance aisée, pas de dette technique liée à Bootstrap ou Tailwind. Design sur-mesure. |
| **Recherche** | **Pagefind** | Indexation et recherche full-text. | Fonctionne sans backend. Multilingue. Poids négligeable. |
| **Visualisation** | **Cytoscape.js** | Rendu du Graphe de Connaissances. | Puissant moteur de théorie des graphes exécuté entièrement dans le navigateur. 11 |
| **Sécurité** | **Staticrypt (WebCrypto API)** | Chiffrement de la zone Intranet. | Sécurité de niveau militaire (AES-256) sans serveur. Idéal pour GitHub Pages. 13 |
| **Intégration Continue** | **GitHub Actions** | Automatisation des mises à jour. | Déploie le site à chaque modification de contenu sans intervention humaine. |

#### **Sources des citations**

1. Stratégies et luttes face à l'Autorité \- Pratiques d'habitat | Etude n°53, consulté le janvier 25, 2026, [https://www.cpcp.be/publications/e53-autorite-logement/](https://www.cpcp.be/publications/e53-autorite-logement/)  
2. Static Websites vs WordPress, Wix, and other dynamic websites \- A9 Web Design, consulté le janvier 25, 2026, [https://a9webdesign.co.uk/articles/static-websites-vs-wordpress-wix-and-other-dynamic-websites/](https://a9webdesign.co.uk/articles/static-websites-vs-wordpress-wix-and-other-dynamic-websites/)  
3. Overview of CrUX | Chrome UX Report, consulté le janvier 25, 2026, [https://developer.chrome.com/docs/crux](https://developer.chrome.com/docs/crux)  
4. Toutes les publications | Citoyenneté & Participation, consulté le janvier 25, 2026, [https://www.cpcp.be/publications/](https://www.cpcp.be/publications/)  
5. CPCP \- Centre Permanent pour la Citoyenneté et la Participation, consulté le janvier 25, 2026, [https://www.cpcp.be/](https://www.cpcp.be/)  
6. Why Static Sites Are Perfect for Modern Business Websites (2025) \- Hungry Ram, consulté le janvier 25, 2026, [https://www.hungryram.com/blog/static-sites-business-websites](https://www.hungryram.com/blog/static-sites-business-websites)  
7. Generative Engine Optimization (GEO): Best Practices for Fortune 100 Marketers, consulté le janvier 25, 2026, [https://www.manhattanstrategies.com/insights/generative-engine-optimization-best-practices](https://www.manhattanstrategies.com/insights/generative-engine-optimization-best-practices)  
8. GitHub Pages limits \- GitHub Enterprise Server 3.14 Docs, consulté le janvier 25, 2026, [https://docs.github.com/en/enterprise-server@3.14/pages/getting-started-with-github-pages/github-pages-limits](https://docs.github.com/en/enterprise-server@3.14/pages/getting-started-with-github-pages/github-pages-limits)  
9. Seamlessly convert your WordPress posts, pages, and custom content types into well-structured Markdown (MD) files. Featuring customizable export settings, support for Advanced Custom Fields (ACF) and Pods, and a real-time progress bar for efficient content management. \- GitHub, consulté le janvier 25, 2026, [https://github.com/robertdevore/markdown-exporter-for-wordpress](https://github.com/robertdevore/markdown-exporter-for-wordpress)  
10. Implementing Agentic Knowledge Graphs using the A2UI Framework \- DEV Community, consulté le janvier 25, 2026, [https://dev.to/vishalmysore/implementing-agentic-knowledge-graphs-using-the-a2ui-framework-2jpi](https://dev.to/vishalmysore/implementing-agentic-knowledge-graphs-using-the-a2ui-framework-2jpi)  
11. Visualize Knowledge Graphs using cytoscape.js | by Ishan Mehta \- Medium, consulté le janvier 25, 2026, [https://ishan-mehta17.medium.com/visualize-knowledge-graphs-using-cytoscape-js-c640e8237d82](https://ishan-mehta17.medium.com/visualize-knowledge-graphs-using-cytoscape-js-c640e8237d82)  
12. Staticrypt : Password protect a static HTML page \- DEV Community, consulté le janvier 25, 2026, [https://dev.to/manishfoodtechs/staticrypt-password-protect-a-static-html-page-1e1h](https://dev.to/manishfoodtechs/staticrypt-password-protect-a-static-html-page-1e1h)  
13. robinmoisson/staticrypt: Password protect a static HTML page, decrypted in-browser in JS with no dependency. No server logic needed. \- GitHub, consulté le janvier 25, 2026, [https://github.com/robinmoisson/staticrypt](https://github.com/robinmoisson/staticrypt)  
14. Generative Engine Optimization: How to Dominate AI Search \- arXiv, consulté le janvier 25, 2026, [https://arxiv.org/html/2509.08919v1](https://arxiv.org/html/2509.08919v1)  
15. Getting started with schema.org using Microdata, consulté le janvier 25, 2026, [https://schema.org/docs/gs.html](https://schema.org/docs/gs.html)  
16. Intro to How Structured Data Markup Works | Google Search Central | Documentation, consulté le janvier 25, 2026, [https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data)  
17. NGO \- Schema.org Type, consulté le janvier 25, 2026, [https://schema.org/NGO](https://schema.org/NGO)  
18. ScholarlyArticle \- Schema.org Type, consulté le janvier 25, 2026, [https://schema.org/ScholarlyArticle](https://schema.org/ScholarlyArticle)  
19. Inclusion Guidelines for Webmasters \- Google Scholar, consulté le janvier 25, 2026, [https://scholar.google.com/intl/en/scholar/inclusion.html](https://scholar.google.com/intl/en/scholar/inclusion.html)  
20. EducationalOccupationalProgram \- Schema.org Type, consulté le janvier 25, 2026, [https://schema.org/EducationalOccupationalProgram](https://schema.org/EducationalOccupationalProgram)  
21. Pagefind | Pagefind — Static low-bandwidth search at scale, consulté le janvier 25, 2026, [https://pagefind.app/](https://pagefind.app/)  
22. Using the Pagefind search API | Pagefind — Static low-bandwidth search at scale, consulté le janvier 25, 2026, [https://pagefind.app/docs/api/](https://pagefind.app/docs/api/)  
23. Faceted search | Astro Digital Garden, consulté le janvier 25, 2026, [https://astro-digital-garden.stereobooster.com/recipes/faceted-search/](https://astro-digital-garden.stereobooster.com/recipes/faceted-search/)  
24. About Git Large File Storage \- GitHub Docs, consulté le janvier 25, 2026, [https://docs.github.com/repositories/working-with-files/managing-large-files/about-git-large-file-storage](https://docs.github.com/repositories/working-with-files/managing-large-files/about-git-large-file-storage)  
25. Git Large File Storage | Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise., consulté le janvier 25, 2026, [https://git-lfs.com/](https://git-lfs.com/)  
26. Cloudflare R2 vs AWS S3 | Review Pricing & Features, consulté le janvier 25, 2026, [https://www.cloudflare.com/pg-cloudflare-r2-vs-aws-s3/](https://www.cloudflare.com/pg-cloudflare-r2-vs-aws-s3/)  
27. Best Tools and Plugins for Converting WordPress to Markdown in 2025 \- WP Email Log, consulté le janvier 25, 2026, [https://wpemaillog.com/2025/09/16/best-tools-and-plugins-for-converting-wordpress-to-markdown-in-2025/](https://wpemaillog.com/2025/09/16/best-tools-and-plugins-for-converting-wordpress-to-markdown-in-2025/)  
28. Eleventy (11ty) vs. Hugo \- CloudCannon, consulté le janvier 25, 2026, [https://cloudcannon.com/blog/eleventy-11ty-vs-hugo/](https://cloudcannon.com/blog/eleventy-11ty-vs-hugo/)  
29. 11ty/eleventy-base-blog: A starter repository for a blog web site using the Eleventy static site generator. \- GitHub, consulté le janvier 25, 2026, [https://github.com/11ty/eleventy-base-blog](https://github.com/11ty/eleventy-base-blog)  
30. GitHub Pages site always flagged as "Deceptive site ahead" / Safe Browsing warning — account/subdomain suspected · community · Discussion \#177060, consulté le janvier 25, 2026, [https://github.com/orgs/community/discussions/177060](https://github.com/orgs/community/discussions/177060)  
31. Static vs Dynamic Websites: Which One Suits Your Business in 2025? \- Cogniter, consulté le janvier 25, 2026, [https://www.cogniter.com/Static-vs-Dynamic-Websites--Which-One-Suits-Your-Business-in-2025-blog.aspx](https://www.cogniter.com/Static-vs-Dynamic-Websites--Which-One-Suits-Your-Business-in-2025-blog.aspx)
