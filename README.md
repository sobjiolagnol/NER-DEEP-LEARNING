


---

#  Détection des Entités Nommées (NER) avec LSTM, BiLSTM et Attention

##  Contributeurs

* **Lagnol SOBJIO**
* **Valdes FEUDJIO**

Projet réalisé dans le cadre du **Mastère Spécialisé Data Science pour la connaissance client**.

---

##  Introduction

Ce projet traite d’un problème fondamental du **Traitement Automatique des Langues (TAL)** :
➡️ **l’étiquetage de séquences et la détection des entités nommées (NER - Named Entity Recognition).**

L’objectif est d’identifier et de classer des entités spécifiques (personnes, lieux, organisations, etc.) dans un texte.
La tâche repose sur le **jeu de données standard CONLL 2003**, utilisant le format BIO (Begin, Inside, Outside).

---

##  Données

Les données sont fournies sous forme de fichiers texte, chaque ligne contenant un **token** et son **étiquette BIO**.
Elles sont réparties en 3 ensembles :

* `conll03-trn.txt` → **Entraînement**
* `conll03-val.txt` → **Validation**
* `conll03-tst.txt` → **Test**

---

##  Méthodologie

1. **Prétraitement**

   * Lecture des fichiers et extraction des tokens/étiquettes.
   * Conversion en séquences numériques (token2id, tag2id).
   * Padding des séquences pour un format compatible avec `tf.keras`.

2. **Modèles implémentés**

   * **LSTM simple** : Embedding → LSTM → Dense → Softmax
   * **BiLSTM** : Embedding → BiLSTM → Dense → Softmax
   * **BiLSTM + Attention** : Embedding → BiLSTM → MultiHeadAttention → Dense → Softmax

3. **Évaluation**

   * Précision et perte via `model.evaluate`.
   * Analyse fine avec `classification_report` (précision, rappel, F1-score par classe).

---

## Résultats

| Modèle                 | Perte (Loss) | Précision (Accuracy) |
| ---------------------- | ------------ | -------------------- |
| **LSTM simple**        | 0.0325       | 99.05 %              |
| **BiLSTM**             | 0.0353       | 99.14 %              |
| **BiLSTM + Attention** | 0.0373       | 99.24 %              |

---

## Analyse des performances

* **LSTM simple**
  ✅ Rapide à entraîner, robuste, bon compromis simplicité/performance.
  ❌ Ne prend pas en compte le contexte bidirectionnel.

* **BiLSTM**
  ✅ Amélioration légère de la précision grâce au contexte avant/après.
  ❌ Plus coûteux en calcul que le LSTM simple.

* **BiLSTM + Attention**
  ✅ Meilleure précision (99.24 %), capture des dépendances complexes.
  ❌ Complexité et temps d’entraînement plus élevés.

---

## ✅ Recommandations

* **Précision maximale** : utiliser **BiLSTM + Attention**.
* **Compromis performance/complexité** : privilégier **BiLSTM**.
* **Ressources limitées** : opter pour le **LSTM simple**.

---

##  Technologies utilisées

* **Python 3.x**
* **TensorFlow / Keras**
* **Scikit-learn**
* **Matplotlib**
* **Requests** (pour téléchargement des données)

---

##  Conclusion

Les trois modèles testés atteignent des **précisions supérieures à 99 %**, confirmant l’efficacité des réseaux neuronaux pour la NER.
Le choix final dépend du **contexte d’application** :

* Rapidité et simplicité → **LSTM simple**
* Bon compromis → **BiLSTM**
* Performance maximale → **BiLSTM + Attention**

---

