# 📚 Resumo — Módulo 8 | Aula 4: Criptografia Assimétrica

## 🎯 Objetivos

- Compreender os princípios e conceitos fundamentais da criptografia assimétrica, incluindo chaves públicas e privadas.
- Explorar os algoritmos de criptografia assimétrica mais comuns, como RSA e ElGamal.
- Aprender a implementar corretamente a criptografia assimétrica, garantindo confidencialidade, integridade e autenticidade dos dados.

---

## 🔐 O que é Criptografia Assimétrica?

Diferente da criptografia simétrica (uma única chave), a criptografia assimétrica utiliza um **par de chaves matematicamente relacionadas**:

- **Chave Pública**: divulgada livremente para qualquer pessoa.
- **Chave Privada**: mantida em sigilo absoluto pelo proprietário.

O que uma chave cifra, **somente a outra consegue decifrar**. Isso elimina o problema de distribuição segura de chaves da criptografia simétrica.

---

## ⚙️ Componentes e Funcionamento

### Fluxo básico:
1. **Geração do par de chaves** — chave pública e privada matematicamente vinculadas, mas computacionalmente inviáveis de serem derivadas uma da outra.
2. **Criptografia** — o remetente usa a chave do destinatário para cifrar a mensagem.
3. **Transmissão** — a mensagem cifrada é enviada; interceptação não compromete o conteúdo.
4. **Descriptografia** — o destinatário usa sua chave correspondente para decifrar a mensagem.

---

## 🔏 Uso 1: Confidencialidade

Garante que **apenas o destinatário legítimo** possa ler a mensagem.

**Exemplo com Alice e Bob:**

| Etapa | Ação |
|---|---|
| 1 | Bob gera seu par de chaves (PubBob / PrivBob) |
| 2 | Alice cifra a mensagem usando **PubBob** |
| 3 | Alice envia a mensagem cifrada |
| 4 | Bob decifra com sua **PrivBob** |

> Mesmo que Eve ou Mallory interceptem a mensagem, não conseguirão decifrá-la sem a **PrivBob**.

---

## ✍️ Uso 2: Assinatura Digital

Garante **autenticidade** (quem enviou) e **integridade** (se foi alterado) dos dados.

**Exemplo com Alice assinando um documento:**

| Etapa | Ação |
|---|---|
| 1 | Alice gera seu par de chaves (PubAlice / PrivAlice) |
| 2 | Alice aplica uma **função hash** ao documento, gerando um resumo |
| 3 | Alice cifra o resumo com sua **PrivAlice** — formando a assinatura digital |
| 4 | Alice envia o documento + assinatura |
| 5 | Bob decifra a assinatura com **PubAlice**, obtendo o resumo original |
| 6 | Bob aplica o mesmo hash ao documento recebido e **compara os resumos** |
| 7 | Se idênticos ✅ — documento autêntico e íntegro |

> Se a assinatura for inválida, indica que o documento foi **alterado** ou **não veio de Alice**.

---

## ⚠️ Desafios e Considerações

- **Desempenho**: Operações matemáticas complexas tornam a criptografia assimétrica mais lenta que a simétrica — especialmente com chaves grandes.
- **Gerenciamento de chaves**: Chaves privadas devem ser armazenadas com máxima segurança; chaves públicas precisam de mecanismos confiáveis de distribuição.
- **Algoritmos confiáveis**: Sempre usar algoritmos amplamente revisados e padronizados.
- **Criptografia Híbrida**: Na prática, combina-se criptografia assimétrica (para troca segura de chaves) com simétrica (para cifrar os dados em si), unindo segurança e eficiência.
- **Atualização contínua**: Acompanhar avanços em criptoanálise para garantir segurança contínua dos sistemas.

---

## 🏆 Principais Algoritmos de Criptografia Assimétrica

### RSA — Rivest, Shamir, Adleman
- Desenvolvido em **1977** por Ron Rivest, Adi Shamir e Leonard Adleman.
- Baseia-se na **dificuldade de fatorar grandes números inteiros**.
- **Tamanho de chave recomendado**: 2048 bits (mínimo); 3072+ bits para segurança de longo prazo.
- **Como funciona (simplificado)**:
  1. Escolhe dois números primos grandes **p** e **q**.
  2. Calcula o módulo **n = p × q**.
  3. Calcula a função totiente **φ(n) = (p-1) × (q-1)**.
  4. Escolhe a chave pública **e** (coprimo de φ(n)).
  5. Calcula a chave privada **d** (inverso multiplicativo de e mod φ(n)).
  6. **Cifrar**: `c = m^e mod n` | **Decifrar**: `m = c^d mod n`
- **Usos**: TLS/SSL, criptografia de e-mails, PGP, SSH, autenticação 2FA.

### DSA — Digital Signature Algorithm
- Desenvolvido pelo **Governo dos EUA**, focado exclusivamente em **assinaturas digitais**.
- **Tamanho de chave recomendado**: 1024 a 3072 bits.
- Mais rápido que o RSA na geração e verificação de assinaturas.
- **Usos**: assinatura de e-mails, certificados digitais, protocolo TLS/SSL.

### Diffie-Hellman
- Desenvolvido por **Whitfield Diffie e Martin Hellman em 1976**.
- Não é um algoritmo de criptografia direta — é um **protocolo de troca de chaves**.
- Permite que duas partes estabeleçam uma **chave secreta compartilhada em um canal inseguro**.
- Segurança baseada na **dificuldade do problema do logaritmo discreto**.
- **Como funciona (simplificado)**:
  1. Alice e Bob concordam com parâmetros públicos: primo **p** e gerador **g**.
  2. Alice gera chave privada **a** → calcula chave pública **A = g^a mod p**.
  3. Bob gera chave privada **b** → calcula chave pública **B = g^b mod p**.
  4. Trocam as chaves públicas A e B.
  5. Alice calcula **S = B^a mod p** | Bob calcula **S = A^b mod p** → **mesmo resultado S**.
- **Usos**: TLS/SSL, SSH, VPNs, troca de chaves simétricas.

### ElGamal
- Combina criptografia de chave pública com a troca de chaves Diffie-Hellman.
- **Tamanho de chave recomendado**: 2048 bits ou mais.
- **Como funciona (simplificado)**:
  1. Chave privada: número secreto **x**.
  2. Chave pública: **y = g^x mod p**.
  3. **Cifrar**: gera par `(r, c)` onde `r = g^k mod p` e `c = (m × y^k) mod p`.
  4. **Decifrar**: `m = (c × r^-x) mod p`.
- **Usos**: criptografia de e-mails, compartilhamento seguro de chaves, criptografia de arquivos.

### ECC — Elliptic Curve Cryptography
- Baseado na teoria das **curvas elípticas sobre corpos finitos**.
- Equação geral da curva: **y² = x³ + ax + b**.
- Segurança baseada no **problema do logaritmo discreto em curvas elípticas**.
- **Grande vantagem**: oferece segurança equivalente ao RSA com **chaves muito menores**.

| Segurança equivalente | RSA | ECC |
|---|---|---|
| Nível padrão | 2048 bits | **256 bits** |
| Nível alto | 3072 bits | **384 bits** |

- **Usos**: TLS/SSL, smart cards, dispositivos IoT, autenticação em dispositivos com recursos limitados.

---

## 📊 Comparativo entre os Algoritmos

| Algoritmo | Tipo | Chave Mínima Segura | Ponto Forte | Limitação |
|---|---|---|---|---|
| **RSA** | Cifra + Assinatura | 2048 bits | Amplamente adotado | Lento com chaves grandes |
| **DSA** | Apenas Assinatura | 1024–3072 bits | Rápido para assinaturas | Não cifra dados |
| **Diffie-Hellman** | Troca de chaves | 2048 bits | Troca segura em canal inseguro | Não cifra/assina diretamente |
| **ElGamal** | Cifra + Assinatura | 2048 bits | Baseado no DH | Chaves maiores que ECC |
| **ECC** | Cifra + Assinatura | 256 bits | Chaves menores, mais eficiente | Implementação mais complexa |

---

## 🔄 Criptografia Simétrica vs. Assimétrica

| Característica | Simétrica | Assimétrica |
|---|---|---|
| **Número de chaves** | 1 (compartilhada) | 2 (pública + privada) |
| **Velocidade** | ✅ Mais rápida | ❌ Mais lenta |
| **Distribuição de chaves** | ❌ Desafio | ✅ Simples |
| **Uso principal** | Cifrar grandes volumes de dados | Troca de chaves e assinaturas |
| **Exemplo de algoritmo** | AES | RSA, ECC |

> 💡 Na prática, os dois modelos são usados em conjunto — **criptografia híbrida**: assimétrica para trocar a chave; simétrica para cifrar os dados.

---

## ✅ Conclusão

A criptografia assimétrica é um pilar fundamental da segurança digital moderna. Com o uso de pares de chaves pública e privada, ela resolve o problema da distribuição segura de chaves e viabiliza **confidencialidade**, **autenticidade** e **integridade** nas comunicações. Os algoritmos **RSA** e **ECC** são os mais utilizados hoje, com o ECC ganhando destaque por sua eficiência com chaves menores — especialmente em dispositivos móveis e IoT. Na prática, a **criptografia híbrida** combina o melhor dos dois mundos: assimétrica para a troca segura de chaves e simétrica para a cifragem eficiente dos dados.

---

> 📌 **Módulo:** 8 — Conceitos de Criptografia  
> 📖 **Aula:** 4 — Criptografia Assimétrica
