# Classificação de Lesões de Pele com CNN e ResNet50

Este projeto aplica técnicas de **Deep Learning** para classificar imagens dermatoscópicas de lesões de pele da base **HAM10000**. O objetivo foi comparar uma **CNN simples** com uma arquitetura mais robusta, a **ResNet50 com Transfer Learning e Fine-tuning**.

> Projeto acadêmico e experimental. Este modelo não substitui avaliação médica.

---

## Objetivo

Desenvolver e avaliar modelos de visão computacional capazes de classificar imagens de lesões de pele em diferentes categorias diagnósticas, analisando o desempenho de uma CNN convencional e de uma ResNet50 pré-treinada.

---

## Dataset

Foi utilizada a base **HAM10000**, composta por imagens dermatoscópicas de lesões pigmentadas de pele.

As classes presentes na base são:

| Código  | Classe                                          |
| ------- | ----------------------------------------------- |
| `akiec` | Queratoses actínicas / carcinoma intraepitelial |
| `bcc`   | Carcinoma basocelular                           |
| `bkl`   | Lesões benignas semelhantes à queratose         |
| `df`    | Dermatofibroma                                  |
| `mel`   | Melanoma                                        |
| `nv`    | Nevos melanocíticos                             |
| `vasc`  | Lesões vasculares                               |

A base apresenta desbalanceamento entre as classes, principalmente pela maior quantidade de imagens da classe `nv`.

---

## Modelos utilizados

### CNN simples

Foi implementada uma CNN sequencial com blocos formados por:

* `Conv2D`
* `BatchNormalization`
* `MaxPooling2D`

Na parte final do modelo foram usadas:

* `GlobalAveragePooling2D`
* `Dense`
* `Dropout`
* `Softmax`

A CNN simples aprende os padrões diretamente das imagens, como bordas, texturas, cores e formas das lesões.

---

### ResNet50 com Transfer Learning

Também foi utilizada a arquitetura **ResNet50**, pré-treinada no ImageNet.

O treinamento foi feito em duas fases:

1. **Feature Extraction**
   A base da ResNet50 ficou congelada, e apenas a cabeça classificadora foi treinada.

2. **Fine-tuning**
   Parte das camadas finais da ResNet50 foi liberada para ajuste, permitindo adaptar melhor os filtros ao problema das lesões de pele.

---

## Métricas avaliadas

Foram utilizadas as seguintes métricas:

* Acurácia
* Precision
* Recall
* F1-score
* Matriz de confusão
* Curva ROC
* AUC por classe

Como a base é desbalanceada, o **F1-score** foi considerado uma métrica mais adequada que a acurácia isolada.

---

## Resultados

A troca da CNN simples para a ResNet50 apresentou melhora no desempenho geral do modelo.

| Modelo      | F1-score |
| ----------- | -------- |
| CNN simples | 0.48     |
| ResNet50    | 0.63     |

Além disso, a curva ROC da ResNet50 apresentou melhor separação entre as classes, com AUCs elevados para a maioria das categorias.

---

## Principais observações

* A CNN simples conseguiu aprender padrões visuais básicos, mas teve desempenho limitado.
* A ResNet50 melhorou a extração de características por aproveitar pesos pré-treinados.
* O desbalanceamento da base impacta diretamente a avaliação do modelo.
* A matriz de confusão percentual facilita a análise por classe.
* A classe `mel`, referente a melanoma, continuou sendo uma das mais desafiadoras.

---

## Tecnologias utilizadas

* Python
* TensorFlow / Keras
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn

---

## Estrutura geral do projeto

```text
├── cnn_ham10000_lesoes_pele.ipynb
├── cnn_ham10000_resnet50_transfer_learning.ipynb
├── README.md
└── resultados/
    ├── curva_roc_resnet50.png
    ├── matriz_confusao_resnet50.png
    └── distribuicao_classes.png
```

---

## Como executar

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
```

2. Instale as dependências:

```bash
pip install tensorflow pandas numpy matplotlib seaborn scikit-learn
```

3. Abra o notebook no Jupyter ou Google Colab.

4. Carregue a base HAM10000 e execute as células na ordem.

---

## Conclusão

A ResNet50 com Transfer Learning e Fine-tuning apresentou desempenho superior à CNN simples, elevando o F1-score de **0.48 para 0.63**. Isso indica que modelos pré-treinados podem ser mais eficientes em problemas de classificação de imagens médicas, especialmente quando a base é complexa e desbalanceada.
