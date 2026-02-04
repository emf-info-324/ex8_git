
# Exercice — Git en mode collaboratif (binôme)

**Objectif**
Manipuler Git dans un contexte réaliste de collaboration : branches, merge, conflits, rebase et commandes de correction.

**Modalité**

* Par groupe de **2**
* Un dépôt GitHub par binôme
* Rôles : **Dev A** et **Dev B** (à alterner)

---

## Contexte

Vous travaillez sur une mini-application très simple (ex. fichier `app.txt` ou `index.html`).

Le dépôt contient au départ :

```txt
Hello World
```

---

## Étape 1 — Mise en place (ensemble)

1. Un des deux crée le dépôt GitHub
2. Ajoute l’autre en collaborateur
3. Clone du dépôt en local
4. Vérifier que vous êtes bien sur `main`

---

## Étape 2 — Création de branches

**Dev A**

* Crée la branche `feature/header`
* Modifie le fichier :

```txt
Hello World
=== HEADER ===
```

* Commit
* Push
* Ouvre une Pull Request (sans merger)

**Dev B**

* Crée la branche `feature/footer`
* Modifie le fichier :

```txt
Hello World
=== FOOTER ===
```

* Commit
* Push
* Ouvre une Pull Request (sans merger)

👉 Objectif : **création de branches + commits indépendants**

---

## Étape 3 — Merge simple

1. Dev A merge sa PR dans `main`
2. Dev B met à jour sa branche avec `main`

   * soit par merge
   * soit par rebase (au choix)

👉 Objectif : **premier merge sans conflit**

---

## Étape 4 — Conflit Git

**Dev A**

* Sur `main`, modifie la ligne `Hello World` en :

```txt
Hello from Dev A
```

* Commit + push

**Dev B**

* Sur `feature/footer`, modifie la **même ligne** en :

```txt
Hello from Dev B
```

* Tente de merger ou rebase avec `main`

👉 Résultat attendu : **conflit**

**À faire**

* Identifier le conflit
* Le résoudre manuellement
* Finaliser le merge ou le rebase

---

## Étape 5 — Rebase (cas propre)

**Dev B**

1. Annule le merge précédent si besoin
2. Rebase `feature/footer` sur `main`
3. Résout le conflit
4. Push avec `--force-with-lease`

👉 Objectif : comprendre **rejouer ses commits** et la différence avec merge

---

## Étape 6 — Reset (erreur classique)

**Dev A**

1. Fait un commit « erreur » (ex. ajoute une ligne inutile)
2. Avant de push :

   * `reset --soft` → garder les modifications
   * recommit correctement
3. Refaire l’erreur
4. `reset --hard` → tout supprimer

👉 Objectif : distinguer **soft vs hard**

---

## Étape 7 — Restore

Sur n’importe quelle branche :

1. Modifier un fichier sans l’indexer
2. Annuler la modification avec `git restore`
3. Modifier + `git add`
4. Retirer le fichier de l’index avec :

```bash
git restore --staged
```

👉 Objectif : comprendre **working tree vs index**

---

## Livrable attendu

* Le dépôt GitHub
* Une PR avec :

  * historique lisible
  * conflits résolus
* Chaque membre doit être capable d’expliquer :

  * quand utiliser **merge / rebase**
  * quand utiliser **reset / revert**
  * le rôle de l’index


