# 📌 PCA vs. ICA na Classificação de Estrelas Variáveis  

## 1️⃣ Introdução  
Este artigo analisa curvas de luz de **Cefeidas, RR Lyrae, Binárias Eclipsantes e Miras** utilizando:  
- **Análise de Componentes Principais (PCA)** → Redução de dimensionalidade baseada na variância dos dados.  
- **Análise de Componentes Independentes (ICA)** → Identificação de padrões independentes nas curvas de luz.  
- **Algoritmo K-means** → Agrupamento das estrelas com base nos coeficientes extraídos.  

O objetivo é determinar **se ICA supera PCA** na separação das classes estelares.  

---

## 2️⃣ Dados Utilizados  
✔️ **65.100 curvas de luz do OGLE**, cobrindo **LMC, SMC e Via Láctea**.  
✔️ **Curvas normalizadas em fase (0 a 1) e interpoladas para 1000 pontos**.  
✔️ **Estrelas analisadas**:  
   - **Cefeidas (FU e FO)**  
   - **RR Lyrae (RRab e RRc)**  
   - **Binárias Eclipsantes (EA, EB, EW)**  
   - **Miras e Semirregulares**  

---

## 3️⃣ Metodologia  

### 📌 1. Representação das Curvas de Luz  
Cada curva de luz foi ajustada usando **séries de Fourier**:  

$$
m(\phi) = A_0 + \sum_{k=1}^{N} A_k \cos(2\pi k \phi) + B_k \sin(2\pi k \phi)
$$  

✔️ **\( A_k, B_k \)** → Coeficientes que representam a curva.  
✔️ **\( $$\phi$$ \)** → Fase normalizada da curva de luz.  
✔️ **\( N \)** → Número de harmônicos utilizados.  

### 📌 2. PCA - Análise de Componentes Principais  
A **PCA** encontra os **componentes principais** resolvendo a equação de autovalores da matriz de covariância:  

$$
C = \frac{1}{N} \sum_{i=1}^{N} (m_i - \bar{m}) (m_i - \bar{m})^T
$$  

Os componentes principais são os **autovetores \($$v_k$$\)** da matriz \( C \), e cada curva é projetada nesses componentes:  

$$
z_{ik} = (m_i - \bar{m}) \cdot v_k
$$  

### 📌 3. ICA - Análise de Componentes Independentes  
A **ICA** assume que os dados \( X \) são uma combinação linear de fontes independentes \( S \):  

$$
X = A S
$$  

O objetivo é encontrar a matriz de separação \( W \), tal que:  

$$
S = W X
$$  

### 📌 4. K-means - Agrupamento das Classes Estelares  
O **K-means** foi aplicado para encontrar agrupamentos nas curvas de luz, minimizando a função:  

$$
J = \sum_{j=1}^{K} \sum_{x_i \in C_j} || x_i - \mu_j ||^2
$$  

A separação dos clusters foi avaliada pelo **índice de Silhueta**:  

$$
s(i) = \frac{b(i) - a(i)}{\max(a(i), b(i))}
$$  

---

## 4️⃣ Resultados e Discussão  

✔️ **ICA separou melhor as classes estelares do que PCA.**  
✔️ **Os coeficientes da ICA foram mais eficientes para identificação de padrões físicos.**  
✔️ **O K-means aplicado à ICA resultou em agrupamentos mais precisos.**  
✔️ **Os diagramas Período-Luminosidade e Cor-Magnitude gerados com ICA foram mais bem definidos.**  

### 📌 Diagramas construídos  
1️⃣ **Diagrama Período-Luminosidade (P–L):**  

$$
M = a \cdot \log P + b + \epsilon
$$  

2️⃣ **Diagrama Cor-Magnitude (CMD):**  

$$
M_V = M_B - M_V
$$  

---

## 5️⃣ Conclusões  

✅ **ICA superou PCA na separação das classes estelares e identificação de padrões físicos.**  
✅ **A combinação ICA + K-means resultou em uma classificação mais precisa.**  
✅ **Os diagramas Período-Luminosidade e Cor-Magnitude gerados com ICA foram mais precisos.**  
✅ **A metodologia pode ser aplicada a outros levantamentos astronômicos.**  

---

## 6️⃣ Pontos Positivos e Negativos da Reprodutibilidade  

### ✔️ Pontos Positivos  
✅ **Uso de dados do OGLE**, um dos levantamentos mais bem documentados da astronomia.  
✅ **Meu supervisor tem experiência com o OGLE**, facilitando a reprodutibilidade.  
✅ **A metodologia pode ser facilmente implementada com bibliotecas como `sklearn` e `FastICA`.**  
✅ **Os diagramas gerados são mais limpos e menos dispersos, tornando a análise mais confiável.**  

### ❌ Pontos Negativos  
❌ **Acesso aos dados do OGLE pode ter restrições.**  
❌ **ICA pode ser computacionalmente cara para grandes conjuntos de dados.**  
❌ **Escolha do número de componentes na PCA e ICA pode afetar os resultados.**  
❌ **K-means depende da escolha correta do número de clusters.**  

---

## 7️⃣ Impacto e Aplicações Futuras  
✔️ ICA pode melhorar a **classificação de estrelas variáveis em levantamentos como LSST e Gaia**.  
✔️ Pode refinar a **calibração da relação Período-Luminosidade**.  
✔️ Pode ser aplicada a **outros domínios científicos**, como análise de espectros estelares e trânsitos planetários.  
