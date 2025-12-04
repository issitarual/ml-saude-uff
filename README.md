# 🧠 Detecção Multiclasse de Deepfakes em Imagens Médicas (MRI & CT Scan)

Este repositório apresenta o projeto desenvolvido para a disciplina Aprendizado de Máquina na Área da Saúde, explorando métodos de deep learning para identificar manipulações (deepfakes) em imagens médicas de MRI e CT Scan.
O trabalho utiliza modelos avançados (ViT e EfficientNet-B7) e aborda um cenário multiclasse com imagens reais e sintéticas geradas por diferentes métodos (Stable Diffusion e CTGAN).

## 🎯 Objetivo Geral

Construir e avaliar pipelines de classificação multiclasse capazes de detectar deepfakes em exames médicos, diferenciando entre:

- TB / TM — imagens reais (True-Benign, True-Malign)
- FB / FM — imagens fake (Fake-Benign, Fake-Malign)

Subtipos adicionais no CT Scan: SD (Stable Diffusion) e CTGAN

## 📌 Arquiteturas

O repositório contém dois pipelines independentes, um para cada tipo de dado.

## 🩻 Pipeline CT Scan — Vision Transformer (ViT)

Para as imagens de tomografia computadorizada (CT Scan), utilizamos uma arquitetura baseada em Vision Transformer (ViT) devido à sua capacidade de capturar detalhes globais — importante para detectar manipulações estruturais em imagens densas.

Classes consideradas:
- FB_CTGAN
- FB_SD
- FM_CTGAN
- FM_SD
- TB
- TM

### 📊 Resultados — CT Scan (ViT)

Acurácia de Validação: 0.6543
Classification Report:

|Classe|Precision	|Recall|	F1-score|	Support|
| -------- | ----- | ----------- |---|---|
|FB_CTGAN|	0.15|	0.14|	0.15|	14|
|FB_SD	|0.56	|0.36|	0.43	|14|
|FM_CTGAN|	0.82	|0.79	|0.80	|52|
|FM_SD	|0.92	|0.94	|0.93	|52|
|TB	|0.22	|0.29	|0.25	|14|
|TM	|0.26	|0.31	|0.29	|16|

Macro F1: 0.48
As classes FM_SD e FM_CTGAN apresentaram excelente desempenho, enquanto classes de benigno (reais ou falsas) permanecem desafiadoras — indicando possível viés na distribuição ou sutileza das manipulações.

## 🧲 Pipeline MRI — EfficientNet-B7

Para as imagens de ressonância magnética (MRI), utilizamos EfficientNet-B7, uma arquitetura otimizada para capturar padrões complexos mantendo excelente eficiência.

Classes consideradas:
- FB
- FM
- TB
- TM

### 📊 Resultados — MRI (EfficientNet-B7)

Acurácia Global: 0.5566
F1-Score Ponderado: 0.5640
AUC (OvR): 0.8247

Classification Report:

|Classe|Precision	|Recall|	F1-score|	Support|
| -------- | ----- | ----------- |---|---|
|FB	|0.96|	0.96|	0.96|	26|
|FM	|1.00|	0.92|	0.96|	26|
|TB	|0.17|	0.19|	0.18|	27|
|TM|	0.19|	0.19|	0.19|	27|

O modelo alcança excelente desempenho na detecção de imagens falsas (FB/FM), mas enfrenta maior dificuldade com classes reais (TB/TM), possivelmente devido às manipulações serem mais evidentes nos fakes em MRI.

## 🧪 Métodos Utilizados
- Transfer Learning
- ViT pré-treinado
- EfficientNet-B7 pré-treinado
- Fine-tuning parcial e por blocos
- MixUp / CutMix
- Label Smoothing
- Class Weights (quando aplicável)
- Treinamento com CUDA / Colab usando T4

## 📈 Discussão dos Resultados
[x] O pipeline CT Scan + ViT apresentou melhor desempenho geral (~65% de acurácia)
[x]O pipeline MRI + EfficientNet-B7 mostrou alta sensibilidade para fakes, mas dificuldade com classes reais
[x] Ambas as arquiteturas conseguiram detectar com facilidade deepfakes mais artificiais (FM, FB), indicando que modelos generativos deixam padrões reconhecíveis, mesmo em dados médicos.

## 🚀 Próximos Passos

- Balanceamento avançado (SMOTE, oversampling por classe)
- Testes com outros modelos
- Combinação multimodal CT+MRI
- Treinamento com validação estratificada k-fold

## 👩‍⚕️ Conclusão

Este repositório explora como modelos modernos de deep learning podem ser aplicados para detectar deepfakes em contextos de saúde — um problema crescente com implicações clínicas e éticas importantes.
Os resultados mostram que a detecção é viável, mas ainda há espaço para melhorias, especialmente na diferenciação de deepfakes vs dados reais.
