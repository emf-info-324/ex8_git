# Exercice — Git collaboratif en binôme (GitHub Flow)

**Modalité**

* Par groupe de 2 (Dev A / Dev B)
* Repo fourni via **GitHub Classroom**
* Règle : **aucun commit direct sur `main`** (branch protection active)

**Fichiers**

* `app.txt` (fourni dans le repo) contenant au départ :

```txt
Hello World
```
---

## Étape 0 — Setup (ensemble)

1. Chaque binôme récupère son repo Classroom
2. Clone en local
3. Vérifie que `main` est à jour :

```bash
git checkout main
git pull
```
---

## Étape 1 — Création de branches + 2 PR indépendantes

### Dev A

1. Crée une branche `feature/header`
2. Modifie `app.txt` en ajoutant à la fin :

```txt
=== HEADER ===
```

3. Commit + push + PR vers `main`
4. Création de la PR vers `main` (sur Github)
5. Merge de la PR (sur Github)

> :warning: Pour cet exerice, nous ferons le merge directement et sans approbation.

### Dev B

1. Crée une branche `feature/footer`
2. Modifie `app.txt` en ajoutant à la fin :

```txt
=== FOOTER ===
```

3. Commit + push + PR vers `main`

✅ Objectifs : **création de branche**, **push**, **PR**

---

## Étape 2 — Merge via PR (pas de commit direct)

1. Dev A fait merger **sa PR** (via GitHub)
2. Dev B **ne merge pas** tout de suite : il doit d’abord **mettre à jour sa branche** avec `main` (Étape 3)

✅ Objectif : respecter le **flux GitHub Flow** (intégration uniquement via PR)

---

## Étape 3 — Mise à jour de branche : merge vs rebase

### Dev B

Après le merge de Dev A, Dev B met à jour sa branche `feature/footer` :

Option attendue ici : **rebase** (pour historique propre)

```bash
git checkout feature/footer
git fetch origin
git rebase origin/main
```

Puis push (si nécessaire) :

```bash
git push --force-with-lease
```

✅ Objectif : **rebase** + compréhension du **force-with-lease** (sur sa branche uniquement)

---

## Étape 4 — Conflit volontaire (toujours via branches + PR)

On va provoquer un conflit sur **la même ligne**.

### Dev A (sur une nouvelle branche)

1. Crée `feature/change-greeting-A`
2. Change la première ligne de `app.txt` en :

```txt
Hello from Dev A
```

3. Commit + push + PR
4. Merge PR (via GitHub)

### Dev B (sur sa branche `feature/footer`)

1. Sans re-cloner, modifie **la même ligne** en :

```txt
Hello from Dev B
```

2. Commit + push
3. Rebase sur `main` :

```bash
git fetch origin
git rebase origin/main
```

➡️ Conflit attendu → résolution manuelle dans `app.txt`, puis :

```bash
git add app.txt
git rebase --continue
git push --force-with-lease
```

✅ Objectifs : **gestion de conflit**, **rebase + résolution**, **push forcé contrôlé**

---

## Étape 5 — Reset (sur branche uniquement)

### Dev A (ou Dev B, peu importe)

Sur une branche `feature/reset-practice` :

1. Fais un “mauvais commit” (ex. ajoute une ligne `BAD LINE`)
2. Montre `git log --oneline`

#### 5.1 Reset soft

Annule le commit **en gardant les changements prêts à recommit** :

```bash
git reset --soft HEAD~1
```

➡️ Recommit avec un message correct, puis push.

#### 5.2 Reset hard

Refais une modification “erreur”, commit, puis supprime **commit + modifs** :

```bash
git reset --hard HEAD~1
```

✅ Objectifs : différence **soft vs hard** (et rappel : sur branche perso)

---

## Étape 6 — Restore (working tree vs staging)

Sur une branche `feature/restore-practice` :

1. Modifie `app.txt` sans add, puis annule :

```bash
git restore app.txt
```

2. Modifie `app.txt`, puis :

```bash
git add app.txt
```

3. Retire du staging (sans perdre la modif) :

```bash
git restore --staged app.txt
```

✅ Objectifs : `restore` + `restore --staged` + compréhension index

---

## Livrables attendus

* Au minimum **4 PR** :

  1. header
  2. footer
  3. change-greeting-A
  4. reset/restore practice (au choix, regroupable)

* Dans l’historique, on doit voir :

  * 1 conflit résolu
  * 1 rebase avec push `--force-with-lease`
  * l’usage de `reset soft` et `reset hard` (preuve via capture ou copy/paste log)
