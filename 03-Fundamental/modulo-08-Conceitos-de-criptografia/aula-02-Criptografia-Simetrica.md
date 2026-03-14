# 📚 Resumo — Módulo 8 | Aula 2: Criptografia Simétrica

## 🎯 Objetivos

- Compreender os princípios básicos da criptografia simétrica.
- Conhecer as cifras de fluxo e de bloco.
- Analisar a segurança da criptografia simétrica.

---

## 🔑 O que é Criptografia Simétrica?

Na criptografia simétrica, uma **única chave** é usada tanto para **criptografar** quanto para **descriptografar** os dados. É uma das técnicas mais importantes para garantir a confidencialidade da informação.

### 🧩 Componentes Principais

| Componente | Descrição |
|---|---|
| **Texto Claro (Plaintext)** | Dados originais legíveis que se deseja proteger |
| **Chave Simétrica** | Valor secreto compartilhado entre remetente e destinatário |
| **Cifra (Cipher)** | Algoritmo matemático que realiza a transformação dos dados |
| **Texto Cifrado (Ciphertext)** | Resultado ilegível após a aplicação da criptografia |

> ⚠️ A chave simétrica deve ser mantida em segredo absoluto — quem a possuir terá acesso total aos dados.

---

## 🌊 Cifra de Fluxo

Opera em **tempo real**, criptografando os dados em um **fluxo contínuo** de bits ou bytes (ao invés de blocos fixos).

**Como funciona:**
1. A chave gera um **keystream** (fluxo de chave pseudoaleatório).
2. Cada bit do texto claro é combinado com o bit correspondente do keystream usando a operação **XOR**.

**Exemplo com XOR:**
```
Texto claro:   10101010
Fluxo de chave: 11001100
Texto cifrado:  01100110

Para descriptografar, basta aplicar XOR novamente:
Texto cifrado:  01100110
Fluxo de chave: 11001100
Texto claro:   10101010  ✅
```

**Vantagens:** Rápida e eficiente — ideal para comunicações em tempo real.  
**Cuidado:** O keystream deve ser gerado de forma segura e aleatória.

---

## 🧱 Cifra de Blocos

Divide o texto claro em **blocos de tamanho fixo** (geralmente 64 ou 128 bits) e criptografa cada bloco de forma independente.

### Modos de Operação

| Modo | Nome | Característica Principal |
|---|---|---|
| **ECB** | Electronic Codebook | Blocos idênticos geram saídas idênticas — **inseguro** para dados com padrões |
| **CBC** | Cipher Block Chaining | Cada bloco depende do anterior; usa vetor de inicialização (IV) — **muito usado** |
| **CFB** | Cipher Feedback | Trata blocos como fluxo de bits; criptografia síncrona |
| **OFB** | Output Feedback | Transforma cifra de bloco em cifra de fluxo; adequado para transmissões assíncronas |
| **CTR** | Counter Mode | Usa contador para gerar keystream; altamente **paralelizável** |

> 💡 O modo **CBC** oferece boa confidencialidade e integridade. O modo **CTR** é o mais eficiente computacionalmente.

---

## 🔄 Distribuição de Chaves

Um dos maiores desafios da criptografia simétrica: como **compartilhar a chave de forma segura**?

### Métodos de Distribuição
- **Distribuição direta:** Entrega física ou transmissão via canal seguro (ex: criptografia de chave pública).
- **Chave mestra:** Uma chave principal gera **chaves de sessão** únicas para cada comunicação.

### Principais Problemas
- **Segredo compartilhado:** Se a chave for interceptada durante a distribuição, toda a segurança é comprometida.
- **Quantidade de chaves:** Em redes grandes, cada par de usuários precisa de uma chave exclusiva, gerando um número enorme de chaves para gerenciar.
- **Escalabilidade:** Quanto mais participantes, mais complexo se torna o gerenciamento.

> 🛡️ Soluções: uso de **criptografia assimétrica** para troca inicial de chaves, protocolo **Diffie-Hellman**, **KMS** (Key Management Systems) e **PKI** (Public Key Infrastructure).

---

## 🏆 Principais Algoritmos de Criptografia Simétrica

### DES — Data Encryption Standard
- Desenvolvido nos anos 1970 pela IBM com a NSA.
- Opera em blocos de **64 bits** com chave de **56 bits**.
- Utiliza estrutura **Feistel** com 16 rounds.
- ❌ Considerado **inseguro** atualmente devido ao tamanho reduzido da chave.

### 3DES — Triple DES
- Extensão do DES: aplica três vezes a lógica **EDE** (Encrypt → Decrypt → Encrypt).
- Usa até três chaves distintas (K1, K2, K3).
- Mais seguro que o DES, porém **mais lento**.
- Sendo substituído pelo **AES**.

### RC4 — Rivest Cipher 4
- Cifra de **fluxo** com chave de tamanho variável (40 a 2048 bits).
- Gera um keystream combinado ao texto claro via XOR.
- ❌ Apresenta **vulnerabilidades conhecidas** — não recomendado para novos projetos.

### RC6 — Rivest Cipher 6
- Cifra de **blocos** de 128 bits.
- Suporta chaves de **128, 192 e 256 bits**.
- Baseado na estrutura Feistel com S-boxes e operações de multiplicação em corpo finito.

### Blowfish
- Cifra de blocos de **64 bits** com chave variável de 32 a 448 bits.
- Estrutura Feistel com 16 a 20 rounds.
- Rápido e eficiente, mas com tamanho de bloco limitado — menos recomendado atualmente.

### Twofish
- Finalista do concurso **AES em 2000**.
- Blocos de **128 bits**, suporta chaves de 128, 192 e 256 bits.
- Usa S-boxes altamente não lineares e permutações complexas.
- Altamente seguro e resistente a ataques conhecidos.

### Serpent
- Também finalista do **AES em 2000**.
- Blocos de **128 bits**, suporta chaves de 128, 192 e 256 bits.
- Reconhecido por sua **robustez e segurança** — considerado o mais conservador dos finalistas.

### AES — Advanced Encryption Standard ⭐
- Padrão adotado pelo **NIST em 2001** (também chamado de Rijndael).
- Opera em blocos de **128 bits** com chaves de 128, 192 ou 256 bits.
- Realiza 10, 12 ou 14 rounds dependendo do tamanho da chave.

**Etapas de cada round:**
1. **SubBytes** — Substituição não linear via S-Box.
2. **ShiftRows** — Deslocamento das linhas do bloco.
3. **MixColumns** — Combinação linear das colunas (omitida no último round).
4. **AddRoundKey** — XOR com a subchave do round.

> ✅ O **AES** é o algoritmo simétrico mais utilizado e confiável atualmente.

---

## 📊 Comparativo dos Algoritmos

| Algoritmo | Tipo | Tamanho do Bloco | Tamanho da Chave | Status |
|---|---|---|---|---|
| DES | Bloco | 64 bits | 56 bits | ❌ Inseguro |
| 3DES | Bloco | 64 bits | 112/168 bits | ⚠️ Legado |
| RC4 | Fluxo | — | 40–2048 bits | ❌ Vulnerável |
| RC6 | Bloco | 128 bits | 128/192/256 bits | ✅ Seguro |
| Blowfish | Bloco | 64 bits | 32–448 bits | ⚠️ Limitado |
| Twofish | Bloco | 128 bits | 128/192/256 bits | ✅ Seguro |
| Serpent | Bloco | 128 bits | 128/192/256 bits | ✅ Muito seguro |
| **AES** | **Bloco** | **128 bits** | **128/192/256 bits** | ✅ **Padrão atual** |

---

## ✅ Conclusão

A criptografia simétrica é uma base fundamental da segurança da informação. Aprendemos sobre seus componentes, os modos de operação das cifras de bloco (ECB, CBC, CFB, OFB, CTR), os desafios da distribuição de chaves e os principais algoritmos — com destaque para o **AES**, que é o padrão mais seguro e amplamente adotado hoje. Compreender esses conceitos é essencial para construir sistemas seguros e proteger dados contra ameaças cibernéticas.

---

> 📌 **Módulo:** 8 — Conceitos de Criptografia  
> 📖 **Aula:** 2 — Criptografia Simétrica
