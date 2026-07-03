# Predição de risco de INR supraterapêutico em pacientes com varfarina

MVP de Machine Learning para sinalizar, na atenção primária, pacientes em uso do medicamento varfarina com maior risco de INR supraterapêutico. Ferramenta de triagem e priorização, sem substituir a decisão clínica.

Elaborado por João Victor Amaral dos Santos como parte da nota para aprovação na sprint de Machine Learning e Analytics

## Contexto

Bases institucionais de anticoagulação têm acesso restrito, então o estudo usa um dataset sintético de ~10.847 pacientes calibrado a partir da literatura. Problema de classificação binária, alvo `inr_status` (0 = terapêutico, 1 = supraterapêutico), com distribuição 54/46.

## Principais achados

- **Modelo final:** XGBoost otimizado via `GridSearchCV` (270 fits).
- **Desempenho no teste:** F1 **0,928**, Recall **0,920**, ROC AUC **0,985**, Acurácia **0,934**.
- **Ganho sobre os baselines** (F1 no teste): +47 pp vs DummyClassifier (0,46), +35 pp vs Logistic Regression (0,58), +11 pp vs árvore simples (0,82).
- **Generalização estável:** diferença CV vs teste de apenas -0,55 pp.
- **Feature dominante:** uso de amiodarona, seguido de dose semanal de varfarina e IMC.
- **Hipóteses:** H1, H2 e H3 confirmadas; H4 parcialmente confirmada (top-5 clinicamente plausível, com divergência atribuída à natureza sintética dos dados).

## Stack

Python, scikit-learn, XGBoost, pandas, seaborn, matplotlib. Execução completa em ~6,6 min. Seed fixa (`42`) para reprodutibilidade.

