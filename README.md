# Détection des maladies du pêcher : YOLO26 vs YOLO11

Projet d'Intelligence Artificielle, 2e année Génie Électrique (2GEC), ENSIT, 2025-2026.

Comparaison de deux architectures Ultralytics (**YOLO26** et **YOLO11**) pour classifier l'état sanitaire de pêchers à partir d'images de verger.

## Classes

| Classe | Type | Description |
|--------|------|-------------|
| Anarsia lineatella | Ravageur | Petite mineuse du pêcher |
| Grapholita molesta | Ravageur | Tordeuse orientale du pêcher |
| Dead Trees | Dépérissement | Arbres morts ou en dépérissement |
| Healthy | Sain | Arbres sans symptôme visible |

## Dataset

[Peach Tree Disease (Kaggle)](https://www.kaggle.com/datasets/marslanarshad/peach-tree-disease) : 4 301 images, réparties 80 % entraînement (3 439) / 20 % validation (862), avec une graine aléatoire fixe (`random.seed(42)`) pour que les deux modèles reçoivent exactement les mêmes données.

Le dataset n'est pas inclus dans ce dépôt : il se télécharge depuis Kaggle.

| Classe | Train | Valid | Part du dataset |
|--------|-------|-------|-----------------|
| Anarsia lineatella | 294 | 74 | 8,56 % |
| Grapholita molesta | 241 | 61 | 7,02 % |
| Dead Trees | 49 | 13 | 1,44 % |
| Healthy | 2 855 | 714 | 82,98 % |

## Configuration d'entraînement

| Paramètre | Valeur |
|-----------|--------|
| Taille d'image | 224 × 224 |
| Epochs | 10 |
| Batch | 32 |
| Patience (early stopping) | 5 |
| Environnement | Google Colab, GPU NVIDIA T4 |

## Résultats

| Indicateur | YOLO11 | YOLO26 |
|------------|--------|--------|
| Top-1 Accuracy (validation) | 83,0 % | 81,1 % |
| Loss finale (validation) | 0,60 | 0,63 |
| Inférence par image | ~3,1 ms | ~2,0 ms |
| Poids du modèle | ~5,2 MB | ~3,1 MB |

YOLO26 est plus léger et plus rapide, au prix d'une exactitude légèrement inférieure.

## Démonstrations

- [Vidéo YOLO26](videos/yolo26_demo.mp4)
- [Vidéo YOLO11](videos/yolo11_demo.mp4)

## Limites et pistes d'amélioration

- **Déséquilibre des classes** : la classe Healthy représente 83 % du dataset. Une accuracy autour de 83 % est proche de ce qu'obtiendrait un modèle qui répondrait toujours « Healthy ». Il faut donc compléter l'évaluation avec la **matrice de confusion** et le **rappel par classe**, surtout pour Dead Trees.
- Entraînement court (10 epochs) : passer à 50-100 epochs.
- Augmentation de données pour les classes minoritaires.
- Quantification et déploiement embarqué du modèle YOLO26.

## Rapport

Le rapport complet est dans le dossier `docs/`.

## Auteurs

Yousfi Eya, Rojbani Imen, Abidi Wiem, Rebah Youssef

Enseignante : Mme Imen Saidi
