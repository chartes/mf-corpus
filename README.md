# Corpus de moyen français annoté

Corpus de référence pour la lemmatisation, l'étiquetage POS et l'analyse morphologique du moyen français (1300–1532), constitué pour l'entraînement de modèles Pie extended. Les modèles et métriques associés sont publiés sur Zenodo (voir ci-dessous).

## Contexte

Ce corpus a été constitué dans la continuité des travaux de lemmatisation de l'ancien français menés à l'École nationale des chartes (modèle OF3C). Le modèle OF3C a été affiné (*fine-tuning*) en trois phases successives sur des sous-corpus annotés manuellement et post-corrigés via [Pyrrha](https://github.com/hipster-philology/pyrrha). Le service de lemmatisation [Deucalion](https://github.com/hipster-philology/deucalion) (Pie extended) a été utilisé pour produire les annotations initiales.

**Principaux défis** :
- Variation diachronique et diatopique importante (1300–1532, dialectes multiples)
- Adaptation du référentiel OF3C (pensé pour l'ancien français) aux évolutions grammaticales du moyen français : disparition progressive de la déclinaison bicasuelle, agglutination (*tresbon*, *nostredit*)
- Lacunes lexicographiques du référentiel Tobler-Lommatzsch pour certains lexiques techniques et la production tardive (rhétoriqueurs, ~1500)

## Contenu du dépôt

```
corpus.tsv            # Métadonnées des 83 textes du corpus global (~409 k tokens)
corpus/
  mf1.tsv             # Sous-corpus MF1 : ~56 k tokens (lemme, POS, MORPH)
  mf4.tsv             # Sous-corpus MF4 : ~37 k tokens (lemme, POS)
  mf6.tsv             # Sous-corpus MF6 : ~22 k tokens (lemme, POS, MORPH)
```

## Corpus global (`corpus.tsv`)

Tableau de métadonnées des 83 textes, couvrant ~409 340 tokens.

| Colonne | Description |
|---|---|
| `Date` | Date approximative du texte |
| `Auteur` | Auteur ou *Anonyme* |
| `Titre` | Titre du texte |
| `Genre` | Genre textuel (chronique, didactique, lyrique, narratif, pratique, théâtre…) |
| `Vers ou prose` | Vers / prose / mixte |
| `Traduction ?` | Oui si le texte est une traduction |
| `Edition` | Référence de l'édition utilisée |
| `Source` | Source numérique (BFM, BVH, DocLing, MCVF, Garnier, Actes princiers…) |
| `Mots` | Nombre de tokens |
| `Langue` | Variété dialectale si connue |
| `URL` | Lien vers la source numérique si disponible |

**Couverture** :

- **Diachronique** : 1300 (*Fouke le Fitz Waryn*) → 1532 (*Gargantua*)
- **Diatopique** : anglo-normand, picard, champenois, normand, parisien, orléanais, bourbonnais, poitevin, flamand, Ouest
- **Générique** : chronique, didactique, documentaire/pratique, hagiographie, histoire, lyrique, médecine, narratif, roman, sermon, théâtre, correspondance
- **Vers et prose**, textes originaux et traductions

## Sous-corpus annotés (`corpus/`)

### Format

Fichiers TSV à 5 colonnes :

| Colonne | Description |
|---|---|
| `form` | Forme graphique du token |
| `lemma` | Lemme (référentiel Tobler-Lommatzsch ; `OUT` = hors référentiel) |
| `POS` | Partie du discours (tagset Pie) |
| `morph` | Traits morphologiques (`MORPH=empty` si absent) |
| `gloss` | Glose éventuelle |

Les limites de texte sont marquées par des lignes **REF** : `REFANNEETitre` (ex. `REF1305Joinville`).

### Phases d'entraînement

| Sous-corpus | Tokens | Annotations |
|---|---|---|
| `mf1.tsv` | ~56 000 | lemme, POS, MORPH |
| `mf4.tsv` | ~37 000 | lemme, POS |
| `mf6.tsv` | ~22 000 | lemme, POS, MORPH |

Chaque phase a utilisé le modèle produit par la phase précédente comme point de départ, avec post-correction manuelle via Pyrrha.

## Modèles

Les modèles entraînés et leurs métriques d'évaluation sont disponibles sur Zenodo :

> Dugaz, Lucien. *Pie Model for Lemmatization, POS Tagging, and Morphological Analysis of Middle French*. Zenodo, juin 2026. [https://doi.org/10.5281/zenodo.20522515](https://doi.org/10.5281/zenodo.20522515)

```bibtex
@misc{dugaz_2026_20522515,
  author    = {Dugaz, Lucien},
  title     = {Pie Model for Lemmatization, POS Tagging, and
               Morphological Analysis of Middle French},
  month     = jun,
  year      = 2026,
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20522515},
  url       = {https://doi.org/10.5281/zenodo.20522515},
}
```

## Outils

- **Annotation / lemmatisation** : [Pie extended](https://github.com/hipster-philology/pie-extended) via [Deucalion](https://github.com/hipster-philology/deucalion) (École des chartes)
- **Post-correction** : [Pyrrha](https://github.com/hipster-philology/pyrrha)
- **Modèle de base** : Old French Corpus Collection (OF3C), École des chartes

## Référence

Ce travail s'inscrit dans la lignée de :

> Duval, Frédéric, Ing, Lucence, Camps, Jean-Baptiste, Kanaoka, Naomi, Pinche, Ariane et Clérice, Thibault. « Lemmatisation de l'ancien français : Présentation du modèle et des outils de l'École des chartes ». *Société de linguistique romane*, 2022, p. 1001-1012.
