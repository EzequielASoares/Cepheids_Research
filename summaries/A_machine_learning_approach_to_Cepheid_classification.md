# 📌 A Machine Learning Approach to Cepheid Variable Star Classification
**Resumo detalhado do artigo: a machine learning approach to cepheid variable stars classification using data alignment and maximum likelihood.**  

---

## **1️⃣ Abstract - Resumo Geral**
Este artigo propõe um método baseado em aprendizado de máquina para classificar **Cefeidas** em duas categorias:  
✔️ **Modo Fundamental**  
✔️ **Primeiro Harmônico**  

A classificação se torna desafiadora quando aplicamos um modelo treinado em uma **galáxia próxima (LMC - Grande Nuvem de Magalhães)** a uma **galáxia distante (M33)** devido a:  
- **Mudança na magnitude aparente** – Cefeidas mais fracas tornam-se indetectáveis.  
- **Viés amostral** – A proporção de estrelas mais luminosas aumenta na galáxia-alvo.  

O artigo propõe um método de **alinhamento de dados via máxima verossimilhança** para corrigir essas diferenças e permitir a reutilização de um modelo treinado sem necessidade de re-rotulagem manual dos dados.  

---

## **2️⃣ Introdução**
- A relação **Período-Luminosidade (P-L)** é fundamental para medir distâncias astronômicas.  
- A mudança na distribuição dos dados entre galáxias dificulta a aplicação direta de um modelo treinado.  
- O artigo propõe um método para alinhar os dados da **M33** aos da **LMC** antes de aplicar a classificação.  

### **📌 Principais desafios abordados**
✔️ **Mudança sistemática na magnitude** devido à distância.  
✔️ **Dificuldade de identificar as classes corretas das Cefeidas sem novos rótulos.**  
✔️ **Adaptação do modelo sem precisar de um novo treinamento.**  

---

## **3️⃣ Conceitos Preliminares**
### **📌 Variáveis Cefeidas**
As **Cefeidas Clássicas** são estrelas pulsantes cuja **luminosidade varia periodicamente** de acordo com a seguinte equação:  

$$
\log_{10} L = a + b \cdot \log_{10} P
$$

Onde:  
- **\(L\)** → Luminosidade da estrela.  
- **\(P\)** → Período de oscilação.  
- **\(a, b\)** → Parâmetros da relação Período-Luminosidade.  

A **magnitude aparente** ($m$) de uma estrela é dada por:

$$
m = -2.5 \cdot \log_{10} \left(\frac{L}{d^2}\right)
$$

Onde **\(d\)** é a distância até a estrela. Assim, **quanto menor o valor de \(m\), mais brilhante a estrela aparece**.  

---

## **4️⃣ Metodologia**
A abordagem do artigo envolve **duas etapas principais**:  

### **📌 1. Ajuste da Magnitude por Máxima Verossimilhança**
O primeiro passo é encontrar um **deslocamento** $\delta$ na magnitude aparente para alinhar os dados da M33 aos da LMC.  

$$
x'_2 = x_2 + \delta
$$

O deslocamento $\delta$ é encontrado **maximizando a verossimilhança** dos dados da M33 em relação à distribuição das Cefeidas na LMC:  

$$
L(\delta | T_{te}') = \sum_{k=1}^{q} \log P_{tr}(x_k)
$$

Aqui, **$P_{tr}(x)$** representa a distribuição de probabilidade das Cefeidas na LMC, assumida como uma **mistura de duas distribuições Gaussianas**:  

$$
P_{tr}(x_1, x_2) = \sum_{i=1}^{2} \phi_i \frac{1}{2\pi\sigma_{i1}\sigma_{i2} \sqrt{1 - \rho_i^2}} \exp\left(-\frac{v_i}{2(1 - \rho_i^2)}\right)
$$

Onde os parâmetros **$\mu_i, \sigma_i, \phi_i$** são ajustados pelos dados da LMC.

### **📌 2. Refinamento do Ajuste Baseado na Proporção das Classes**
Após encontrar $\delta$, ajustamos iterativamente sua magnitude até que a proporção das classes prevista no conjunto de teste **coincida com a distribuição original da LMC**. Isso é feito aplicando **bootstrap** para estimar a proporção esperada das classes.  

---

## **5️⃣ Resultados Experimentais**
Os experimentos avaliaram a **precisão da classificação** em duas bandas:  
✔️ **Banda Visível (V)**  
✔️ **Banda Infravermelha (I)**  

### **📌 Comparação de Precisão (%)**
| Método | Sem correção | Deslocamento fixo | Passo 1 (Verossimilhança) | Passo 2 (Refinamento) |
|--------|------------|----------------|-------------------|----------------|
| **Redes Neurais** | 90,09% | 94,48% | **96,78%** | 95,72% |
| **SVM** | 93,38% | 95,30% | 95,98% | **97,09%** |
| **Árvores de Decisão** | 94,32% | 94,49% | 97,27% | **97,09%** |
| **Random Forest** | 94,12% | 94,80% | 96,13% | **96,40%** |

---

## **6️⃣ Conclusão**
- A técnica permite reutilizar um modelo treinado sem necessidade de rotulagem manual dos dados da galáxia-alvo.  
- O método melhora a precisão e supera abordagens anteriores baseadas em **deslocamento fixo**.  
- Pode ser aplicada em outras áreas onde há **mudanças sistemáticas nos dados**, como **física de partículas e aprendizado por transferência (transfer learning)**.  

---

## **📌 Pontos Positivos e Negativos da Reprodutibilidade**
### **✔️ Pontos Positivos**
✅ O método utiliza conceitos estatísticos bem estabelecidos.  
✅ Não exige novas rotulações manuais, reduzindo o custo da classificação.  
✅ Pode ser aplicado a outras áreas com problemas similares de deslocamento de dados.  

### **❌ Pontos Negativos**
❌ Depende de uma boa modelagem da distribuição inicial.  
❌ A precisão pode ser afetada por ruídos na medição das magnitudes.  
❌ O processo de ajuste pode ser computacionalmente caro.  
