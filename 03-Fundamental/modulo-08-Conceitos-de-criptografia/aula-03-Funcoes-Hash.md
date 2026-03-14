# 📚 Resumo — Módulo 8 | Aula 3: Funções Hash

## 🎯 Objetivos

- Compreender o conceito de função hash e sua importância na criptografia e integridade de dados.
- Explorar diferentes algoritmos de função hash e suas propriedades.
- Aplicar funções hash em exemplos práticos como verificação de integridade e autenticação de dados.

---

## 🔍 O que é uma Função Hash?

Uma função hash é um algoritmo matemático que recebe dados de entrada de **tamanho arbitrário** e produz uma saída de **tamanho fixo**, chamada de **hash**, **digest** ou **valor de hash**. Suas características fundamentais são:

- **Determinística**: a mesma entrada sempre produz o mesmo hash.
- **Rápida de calcular**: eficiente computacionalmente.
- **Irreversível**: não é possível recuperar os dados originais a partir do hash.
- **Sensível a mudanças**: qualquer alteração mínima na entrada gera um hash completamente diferente.

---

## ⚙️ Propriedades das Funções Hash

### 🔒 Resistência à Inversão (Pré-imagem)
Dado um valor de hash, é computacionalmente inviável encontrar a entrada original que o gerou. Isso é essencial no armazenamento de senhas — o sistema guarda o hash, não a senha em si.

### 💥 Colisões
Ocorrem quando **duas entradas diferentes** produzem o **mesmo valor de hash**. Existem dois tipos:

| Tipo | Descrição |
|---|---|
| **Acidental** | Resultado da natureza probabilística das funções hash |
| **Intencional** | Resultado de ataques deliberados para falsificar dados |

> ⚠️ Colisões comprometem a integridade e autenticidade dos dados. Funções hash seguras devem ter resistência robusta a colisões.

### 📊 Distribuição Uniforme
Os valores de hash devem ser distribuídos de forma **equilibrada** em todo o espaço de saída, evitando concentrações que aumentem a probabilidade de colisões.

### 🆔 Unicidade
Cada conjunto de dados diferente deve gerar um hash **único**. Embora colisões sejam matematicamente inevitáveis (espaço de saída finito), funções de qualidade as tornam extremamente improváveis na prática.

### ✅ Integridade
Permite **detectar qualquer modificação** nos dados. Como qualquer alteração, mesmo mínima, gera um hash completamente diferente, basta comparar o hash atual com o de referência para verificar se os dados foram adulterados.

### 🔀 Confusão
Torna a relação entre a entrada e o hash **complexa e imprevisível**, dificultando a inferência de informações sobre os dados originais a partir do hash.

### 🌊 Difusão
Garante que **qualquer mudança na entrada** afete **todos os bits do hash** resultante, espalhando as propriedades dos dados de forma caótica por toda a saída.

### 🎂 Paradoxo do Aniversário
Fenômeno estatístico que mostra que a probabilidade de colisões cresce rapidamente com o número de entradas. Quando o número de elementos se aproxima da **raiz quadrada do espaço de valores**, a probabilidade de colisão já se torna significativa.

> Exemplo: com um espaço de 10.000 valores de hash possíveis, com apenas ~100 entradas já há chance considerável de colisão.

---

## 🛠️ Aplicações das Funções Hash

- **Criptografia**: resumos criptográficos em assinaturas digitais (RSA, DSA) e hash de senhas (bcrypt, scrypt).
- **Verificação de integridade de arquivos**: detectar corrupção ou adulteração de dados.
- **Tabelas de dispersão (Hash Tables)**: indexação eficiente de dados em bancos e estruturas de dados.
- **Downloads seguros**: sites fornecem o hash do arquivo original para que o usuário compare após o download.
- **Integridade de mensagens em redes**: protocolos como IPsec e SSL/TLS usam hash para garantir que mensagens não foram alteradas em trânsito.

---

## 🏆 Principais Algoritmos de Funções Hash

### MD5 — Message Digest Algorithm 5
- Desenvolvido por **Ronald Rivest em 1991**.
- Gera hash de **128 bits**, operando em blocos de 512 bits.
- ❌ **Inseguro para aplicações criptográficas críticas** — colisões podem ser geradas com recursos computacionais modernos.
- Ainda usado em verificações simples de integridade (não criptográficas).

### SHA-1 — Secure Hash Algorithm 1
- Desenvolvido pelo **NIST em 1995**.
- Gera hash de **160 bits**, operando em blocos de 512 bits.
- ❌ **Vulnerabilidades descobertas em 2005** — colisões são encontráveis na prática.
- Uso desencorajado em favor de alternativas mais seguras.

### SHA-2 — Secure Hash Algorithm 2
- Família desenvolvida pelo **NIST** como evolução do SHA-1.
- Inclui variantes: **SHA-224, SHA-256, SHA-384 e SHA-512**.
- ✅ **SHA-256 é o padrão mais utilizado atualmente** — adotado em certificados digitais, TLS/SSL e autenticação.
- Muito mais resistente a colisões que MD5 e SHA-1.

### SHA-3 — Secure Hash Algorithm 3
- Selecionado pelo **NIST em 2012** como alternativa ao SHA-2.
- Inclui variantes: **SHA3-224, SHA3-256, SHA3-384 e SHA3-512**.
- Baseado na construção **Esponja (Sponge)**, diferente dos algoritmos anteriores.
- ✅ **O mais seguro entre os algoritmos apresentados** — resistente a ataques diferenciais e lineares.
- Recomendado para aplicações que exigem segurança de longo prazo.

### RIPEMD-160
- Desenvolvido em **1996** como alternativa ao MD5 e SHA-1.
- Gera hash de **160 bits**, operando em blocos de 512 bits.
- ⚠️ Nível de segurança **aceitável**, mas inferior ao SHA-256.
- Utilizado em criptografia, assinaturas digitais e autenticação de arquivos.

### Blake2
- Desenvolvido em **2012**, como evolução do Blake.
- Variantes: **Blake2b** (512 bits) e **Blake2s** (256 bits).
- ✅ **Desempenho excepcional** — significativamente mais rápido que a maioria dos algoritmos.
- Altamente resistente a colisões, pré-imagem e ataques diferenciais.
- Popular em aplicações que exigem hash rápido e seguro.

---

## 📊 Comparativo entre os Algoritmos

| Algoritmo | Tamanho do Hash | Segurança | Observação |
|---|---|---|---|
| **MD5** | 128 bits | ❌ Inseguro | Apenas usos não criptográficos |
| **SHA-1** | 160 bits | ❌ Vulnerável | Uso desencorajado |
| **SHA-256** | 256 bits | ✅ Seguro | Padrão atual mais adotado |
| **SHA-3** | 224–512 bits | ✅ Muito seguro | Mais robusto; recomendado |
| **RIPEMD-160** | 160 bits | ⚠️ Moderado | Alternativa legada |
| **Blake2** | 1–512 bits | ✅ Seguro | Mais rápido; flexível |

---

## ✅ Conclusão

As funções hash são peças fundamentais da segurança da informação, garantindo **integridade, autenticidade e confidencialidade** dos dados. Suas propriedades — resistência à inversão, unicidade, distribuição uniforme, confusão e difusão — tornam-nas indispensáveis em criptografia, armazenamento de senhas, verificação de arquivos e comunicações seguras. O **SHA-256** é o padrão mais utilizado hoje, enquanto o **SHA-3** e o **Blake2** representam as escolhas mais modernas e seguras para novas aplicações.

---

> 📌 **Módulo:** 8 — Conceitos de Criptografia  
> 📖 **Aula:** 3 — Funções Hash
