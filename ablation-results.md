# HLB-CIFAR10 — Résultats, Interprétations et Explications

## Résultats complets

Chaque commande a été exécutée avec 5 runs.

| Expérience                     | Acc. moyenne | Std    | Δ vs baseline | Temps final (s) |
| ------------------------------ | ------------ | ------ | ------------- | --------------- |
| **Baseline**                   | **0.9407**   | 0.0020 | —             | 68.7            |
| Sans SE                        | 0.9411       | 0.0011 | **+0.0004**   | 65.4            |
| Sans Whitening                 | 0.9318       | 0.0016 | -0.0090       | 69.1            |
| Sans EMA                       | 0.9346       | 0.0022 | -0.0061       | 67.9            |
| EMA 1 epoch                    | 0.9399       | 0.0009 | -0.0008       | 68.2            |
| EMA 4 epochs                   | 0.9392       | 0.0009 | -0.0016       | 68.7            |
| Sans TTA                       | 0.9343       | 0.0014 | -0.0064       | 68.6            |
| Sans Flip                      | 0.9338       | 0.0019 | -0.0069       | 68.2            |
| Sans Crop (avec pad)           | 0.9049       | 0.0017 | **-0.0358**   | 105.0           |
| Sans Crop ni Pad               | 0.9341       | 0.0017 | -0.0067       | 67.1            |
| Label Smoothing 0.0            | 0.9372       | 0.0025 | -0.0036       | 68.2            |
| Label Smoothing 0.1            | 0.9407       | 0.0013 | ~0            | 68.7            |
| Label Smoothing 0.2 (baseline) | 0.9407       | 0.0020 | —             | 68.7            |
| Label Smoothing 0.3            | 0.9411       | 0.0024 | +0.0004       | 68.0            |
| Sans channels_last             | 0.9401       | 0.0009 | -0.0006       | **96.3**        |
| Warmup 0%                      | 0.9333       | 0.0037 | -0.0075       | 68.0            |
| Warmup 10%                     | 0.9409       | 0.0014 | +0.0001       | 68.1            |
| Warmup 20% (baseline)          | 0.9407       | 0.0020 | —             | 68.7            |
| Warmup 35%                     | 0.9404       | 0.0008 | -0.0003       | 68.1            |
| Warmup 50%                     | 0.9398       | 0.0020 | -0.0009       | 68.2            |
| Batch 256, LR÷2                | 0.9421       | 0.0013 | +0.0013       | 68.7            |
| Batch 512 (baseline)           | 0.9407       | 0.0020 | —             | 68.7            |
| Batch 1024, LR×2               | 0.9369       | 0.0017 | -0.0038       | 68.9            |
| Batch 1024, LR×2, warmup 35%   | 0.9372       | 0.0016 | -0.0035       | 69.0            |
| **Tout désactivé**             | **0.8834**   | 0.0025 | **-0.0574**   | 94.8            |

## Classement par impact sur la précision

| Rang | Technique       | Δ        | Interprétation                 |
| ---- | --------------- | -------- | ------------------------------ |
| 1    | Random Crop     | -0.0358  | Technique la plus critique     |
| 2    | Whitening       | -0.0090  | Impact fort sur la convergence |
| 3    | Flip            | -0.0069  | Régularisation importante      |
| 4    | TTA             | -0.0064  | Gain gratuit à l'évaluation    |
| 5    | EMA             | -0.0061  | Stabilisation finale utile     |
| 6    | Warmup (0%)     | -0.0075  | Instabilité sans warmup        |
| 7    | Label Smoothing | -0.0036  | Gain modeste mais réel         |
| 8    | Batch 1024      | -0.0038  | Limite de la règle linéaire    |
| 9    | SE layers       | +0.0004  | Neutre sur CIFAR-10            |
| 10   | channels_last   | **+40s** | Impact vitesse uniquement      |

## Résultat clé : contribution totale

- **Baseline (tout activé)** : 94.07%
- **Tout désactivé** : 88.34%
- **Gain total de toutes les techniques** : **+5.73 points**
