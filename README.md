# PEA Manager 2026 🚀

> Application web de gestion de PEA (Plan d'Épargne en Actions) — 100% personnelle, hébergée sur GitHub Pages, sans serveur, sans abonnement.

🔗 **https://pierredupre71130.github.io/pea-2026/**

---

## Présentation

PEA Manager 2026 est une application monopage (single-file HTML) qui centralise tout le suivi d'un PEA : portefeuille, transactions, planning d'achat mensuel, simulation long terme, budget personnel, analyses IA et bien plus. Elle fonctionne entièrement dans le navigateur — les données sont stockées localement (localStorage) et peuvent être synchronisées entre plusieurs appareils via un Gist GitHub privé.

**Aucune installation. Aucun serveur. Aucune donnée envoyée à un tiers (sauf Gist GitHub optionnel et les APIs IA si configurées).**

---

## Fonctionnalités

### 📊 Tableau de bord

Vue d'ensemble instantanée du portefeuille :

- **4 métriques clés** : valeur totale du portefeuille, capital investi, plus-value latente (montant + %), liquidités disponibles
- **Graphique d'allocation** : camembert des positions en temps réel
- **Graphique Plus/moins-values par titre** : barres colorées positif/négatif pour chaque ligne
- **Évolution du PEA** : courbe temporelle avec filtres 1S / 1M / 3M / 1A / MAX et bouton 🔄 de rechargement
- **Transactions récentes** : les 5 dernières opérations avec accès direct à la liste complète

---

### 💼 Portefeuille

Tableau détaillé de toutes les positions ouvertes :

- **PRU (Prix de Revient Unitaire)** calculé automatiquement à partir des transactions d'achat, avec possibilité de surcharge manuelle
- **Plus-value latente** en euros et en % par ligne
- **Cours actuel** récupéré automatiquement (via cache mis à jour manuellement)
- **Poids dans le portefeuille** (% de la valeur totale)
- **Nombre de parts** et valeur de marché
- Tri par valeur décroissante

---

### 🔄 Transactions

Historique complet de toutes les opérations :

- **Types supportés** : Achat, Vente, Dividende, Dépôt, Retrait
- **Ajout manuel** avec formulaire complet (ticker, nom, date, quantité, prix, frais)
- **Scan IA** : photo ou copié-collé d'un avis d'opération → l'IA extrait automatiquement les données et pré-remplit le formulaire (multi-lignes supporté)
- **Filtres** par type et recherche par ticker/nom
- **Modification et suppression** de chaque transaction
- **Import automatique depuis le plan** : bouton "✓ Acheter" dans le Planning qui crée directement la transaction

---

### 💰 Trésorerie

Suivi des liquidités et du plafond légal PEA :

- **Liquidités disponibles** : solde en espèces dans le PEA
- **Total versé** : cumul de tous les dépôts
- **Plafond restant** : 150 000 € légal − total versé, avec barre de progression visuelle
- **Historique des mouvements** : tous les dépôts et retraits chronologiques
- Indicateur de plafond en sidebar (toujours visible)

---

### 🏠 Budget Perso

Gestion du budget mensuel personnel, complètement séparée du PEA :

#### Récapitulatif du mois
- **Solde de départ du mois** : montant saisi avant tout prélèvement
- **Charges fixes récurrentes** : total des dépenses mensuelles et annuelles (divisées par 12)
- **Charges ponctuelles** : dépenses uniques du mois (ex. virement PEA), listées séparément
- **Encours carte bancaire** : montant dépensé par carte ce mois (débité le mois suivant)
- **Reste disponible** : solde après toutes déductions, avec % du solde de départ

#### Calendrier des prélèvements
- Vue chronologique de **tous** les prélèvements du mois (J.4, J.7, J.16…)
- **Solde courant affiché après chaque débit** (passés en grisé, aujourd'hui en surbrillance)
- Badges « prélevé » pour les charges passées, « ponctuel » pour les charges uniques
- Solde final après tous les prélèvements du mois

#### Gestion des charges
- **Fréquence** : mensuelle, annuelle (÷12 automatique), ou ponctuelle (unique)
- **Jour de prélèvement** configurable par charge (ex : loyer le 7, mutuelle le 27)
- **Catégories** : Logement, Alimentation, Transport, Santé, Loisirs, Abonnements, Épargne/Investissement, Autres
- Répartition par catégorie avec barres de progression (% des charges et % du solde)
- Tableau détaillé : montant mensuel, annuel, jour de prélèvement, notes
- Ajout, modification et suppression de chaque charge

#### Encours carte
- Configuration du nom de la carte et du jour de débit (ex : Gold Caisse d'Épargne, le 4)
- Saisie mensuelle de l'encours (variable selon les achats du mois)

---

### 📅 Planning Mensuel

Simulation et optimisation du plan d'achat mensuel :

#### Budget et ETFs
- **Budget mensuel total** configurable
- **Répartition ETF** : allocation cible en % pour chaque ETF (total doit faire 100%)
- **Simulation d'achat automatique** :
  - Calcule le montant idéal à acheter pour chaque ETF selon sa pondération cible
  - Intègre les **frais de courtage réels Boursobank** (1,99 € fixe si < 500 €, sinon % configuré)
  - Minimum d'achat 200 € (Boursobank) : si le montant idéal est inférieur, forçage au minimum (⚡ Min. forcé)
  - **Règle ±3%** : tolère un écart de 3% autour de la cible après achat. Si un ETF s'écarte davantage, le budget est redirigé depuis les ETFs sur-pondérés vers les sous-pondérés
  - Statuts : ✓ OK, ↑ Renforcé, ↓ Réduit, ⏭ Différé, ⚡ Min. forcé, < Min.
- **Arrondi en parts entières** (Boursobank ne supporte pas les fractions)
- **TER** (Total Expense Ratio) affiché et mis à jour depuis justETF
- **% ETF actuel → projeté** après achat

#### Titres directs (actions)
- Nombre de parts mensuel configurable par titre
- Cours actuel, montant total (net + frais), frais de courtage

#### Gestion concentration Air Liquide (AI.PA)
- **Curseur ⚠️ Alerte** (défaut 30%) : affiche une alerte orange si AI.PA dépasse ce % du portefeuille total
- **Curseur 🛑 Limite** (défaut 35%) : au-delà de ce seuil, le plan est automatiquement **cappé à 1 action maximum**
- Le cash libéré par le cap AI.PA est **automatiquement redirigé vers WPEA.PA** (parts supplémentaires calculées au plus bas), même si WPEA dépasse son % cible
- Badges visuels : `+Nx ↩AI` sur WPEA, `cappé` sur AI.PA
- Seuils persistés dans les paramètres (localStorage)

#### Plans sauvegardés
- Sauvegarde du plan courant en 1 clic
- Plans générés par l'IA sauvegardés automatiquement (avec couleur)
- Chargement et suppression de plans sauvegardés

#### Actualisation des cours
- Bouton "⟳ Actualiser les cours" : récupère les prix en temps réel pour tous les tickers du plan
- Bouton "📡 MAJ TER" : met à jour les TER depuis justETF
- Bouton "🌐 MAJ Base complète" : actualise toute la base de données ETF PEA

#### Projection après achat
- Tableau de toutes les positions projetées après les achats du mois
- % actuel et % projeté dans le portefeuille total
- Valeur actuelle et valeur projetée

---

### 🔮 Simulation Long Terme

Projection de l'évolution du PEA sur plusieurs années :

- **Paramètres configurables** : durée (mois), rendement annuel %, budget mensuel, départ depuis la valeur actuelle ou depuis zéro
- **Courbe de projection** : valeur du portefeuille vs capital investi mois par mois
- **Statistiques finales** : valeur projetée, capital versé, plus-value totale, rendement annualisé (XIRR)

#### Simulation Loyauté Air Liquide
- Simule les **dividendes Air Liquide** reçus chaque année (basé sur le nombre de parts projeté)
- Gère le **bonus nominatif +10%** (éligible après 2 ans civils d'inscription au nominatif)
- Simule l'**attribution d'actions gratuites** (1 action pour 10 détenues, tous les 2 ans)
- Tableau détaillé : date d'inscription au nominatif, année d'éligibilité, historique de chaque événement (dividende, action gratuite)

---

### 📈 Performance

Analyse approfondie de la performance réelle du portefeuille :

- **XIRR** (Taux de Rendement Interne avec dates exactes) calculé sur l'ensemble des flux de trésorerie
- **Benchmark MSCI World** : comparaison avec l'indice mondial, reconstitué à partir des dates réelles d'achat (DCA)
- **Évolution de la performance** dans le temps
- Statistiques détaillées : capital investi, valeur actuelle, P&L total, rendement annualisé

---

### 📉 Analyse Technique

Indicateurs techniques pour n'importe quel titre :

- **Sélection** depuis les positions en portefeuille ou saisie manuelle d'un ticker Yahoo Finance
- **Périodes** : 1 mois, 3 mois, 6 mois, 1 an, 2 ans
- **Indicateurs** : Moyennes mobiles (MM20, MM50, MM200), RSI, MACD, Bollinger Bands, supports & résistances
- Graphiques Chart.js interactifs

---

### 📰 Actualités

Veille sur les titres du portefeuille et les marchés :

- Flux d'actualités par ticker (depuis le portefeuille)
- Actualités générales marchés (CAC 40, ETF, économie)
- Liens directs vers les articles sources
- Date et source affichés pour chaque article

---

### 🤖 Analyse IA

Assistant IA intégré, connecté aux données réelles du portefeuille :

#### Actions rapides
- **📊 Analyse du portefeuille** : diagnostic complet (allocation, risques, diversification, recommandations)
- **📅 Conseil achat mensuel** : recommandations d'achat basées sur le budget et le plan
- **⚡ Analyse des risques** : concentration, volatilité, corrélations
- **📋 Analyse du plan mensuel** : évaluation et optimisation du Planning
- **📈 Rapport trimestriel** : bilan de la période
- **🏭 Analyse sectorielle** : répartition sectorielle du portefeuille

#### Outils avancés
- **💰 Valorisation IA** : estimation du juste prix d'une action (DCF, multiples, consensus)
- **📝 Thèse d'investissement** : analyse bull/bear complète d'un titre
- **🔄 Comparaison de plans** : compare deux allocations différentes (rendement, risque, frais)

#### Chat libre
- Conversation libre avec l'IA sur n'importe quel sujet financier
- L'IA a accès au contexte complet du portefeuille (positions, transactions, budget, plan)
- Historique de la conversation dans la session

#### Fournisseurs IA supportés
| Fournisseur | Modèles | Coût |
|---|---|---|
| **Claude (Anthropic)** | Haiku / Sonnet / Opus | Payant (clé API) |
| **Gemini (Google)** | Flash / Pro | Gratuit (1 500 req/jour) |
| **Groq LLaMA** | LLaMA 3.x | Gratuit, ultra-rapide |
| **Grok (xAI)** | Grok-2 | Avec recherche web |

---

### ⚙️ Paramètres

#### Compte
- Nom du PEA personnalisable
- Budget mensuel (utilisé dans Planning et Simulation)

#### Fournisseur IA
- Choix du moteur IA (Claude, Gemini, Groq, Grok)
- Saisie et test des clés API
- Choix du modèle par fournisseur

#### Synchronisation multi-appareils (GitHub Gist)
- **Principe** : les données sont sauvegardées dans un Gist GitHub **privé** (invisible publiquement)
- **Token GitHub** : Personal Access Token avec scope `gist` uniquement
- **Auto-découverte** : si le Gist existe déjà sur un autre appareil, il est trouvé automatiquement
- **Sync automatique** : toute modification est poussée après 3 secondes (debounce)
- **Sécurité** : les clés API ne sont **jamais** incluses dans le Gist (filtrées avant push)
- **Multi-appareils** : iPhone + PC + tablette — toutes les données synchronisées
- Statut de sync visible en sidebar (✓ synchronisé / 🔄 en cours / ✗ erreur)

#### Données
- **Export JSON** : sauvegarde complète de toutes les données
- **Import JSON** : restauration depuis un fichier
- **Réinitialisation** : remise à zéro (avec confirmation)

---

## Architecture technique

| Aspect | Détail |
|---|---|
| **Type** | Single-file HTML (index.html ~9 000 lignes) |
| **Framework** | Vanilla JS — aucune dépendance npm |
| **Graphiques** | Chart.js 4.4.0 (CDN) |
| **Stockage** | localStorage (`pea_2026`) |
| **Sync** | GitHub Gist API (optionnel) |
| **Hébergement** | GitHub Pages (branche `main`) |
| **Mobile** | Responsive — navigation bottom bar sur mobile |
| **Thème** | Dark theme (CSS variables) |

---

## Déploiement

L'application est déployée automatiquement sur GitHub Pages à chaque push sur `main`.

```
https://pierredupre71130.github.io/pea-2026/
```

Pour voir les dernières mises à jour sur iPhone (Safari) : ouvrir en **onglet privé** pour éviter le cache.

---

## Sécurité

- Aucune donnée envoyée à des serveurs tiers (sauf Gist GitHub si configuré, et APIs IA si utilisées)
- Les clés API sont stockées **uniquement** dans localStorage, jamais dans GitHub
- Le Gist de synchronisation est **privé** — non indexé, non accessible sans le token
- Filtrage systématique des clés API avant tout push Gist

---

## Développement

Toutes les modifications passent par une feature branch et une PR avant merge sur `main` :

```bash
git checkout -b feature/ma-fonctionnalite
# ... modifications ...
git push origin feature/ma-fonctionnalite
# Créer PR → squash merge → GitHub Pages déploie automatiquement
```
