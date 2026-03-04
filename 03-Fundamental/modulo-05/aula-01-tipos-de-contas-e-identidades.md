# Identity and Account Management (IAM)

## 📚 Aula 1 — Gerenciamento de Identidades e Contas

O **Identity and Access Management (IAM)** é um conjunto de práticas utilizadas para controlar **quem pode acessar recursos dentro de um sistema ou organização**.

O objetivo é garantir que **somente usuários autorizados tenham acesso aos recursos corretos**, protegendo dados e sistemas contra acessos indevidos.

---

# Objetivos da Aula

- Entender o conceito de **identidade digital**
- Conhecer **tipos de contas**
- Compreender **gestão de privilégios**
- Entender processos de **onboarding e offboarding**
- Aprender boas práticas de **segurança de contas**

---

# Identidade Digital

Uma **identidade digital** representa um usuário dentro de um sistema.

Ela normalmente é composta por:

- Nome de usuário
- Credenciais de autenticação
- Permissões de acesso
- Atributos da conta

Essa identidade permite que sistemas **identifiquem, autentiquem e autorizem usuários**.

---

# Certificados Digitais e PKI

A **PKI (Public Key Infrastructure)** permite criar identidades digitais seguras usando criptografia.

Ela funciona com um **par de chaves criptográficas**:

- 🔑 Chave pública
- 🔐 Chave privada

A chave pública é incluída em um **certificado digital emitido por uma Autoridade Certificadora (CA)**.

### Vantagens

- Autenticação forte
- Maior segurança
- Integridade de identidade

A chave privada pode ser armazenada em:

- computador
- smart cards
- token USB
- TPM

---

# Tokens de Autenticação

Tokens são utilizados em sistemas de **Single Sign-On (SSO)**.

Funcionamento básico:

1. Usuário autentica no **provedor de identidade**
2. Recebe um **token criptográfico**
3. Usa esse token para acessar múltiplos serviços

### Vantagem

Permite acessar vários sistemas com apenas um login.

### Risco

Se o token for roubado, um atacante pode utilizá-lo.

---

# Provedores de Identidade (IdP)

Um **Identity Provider (IdP)** é responsável por:

- autenticar usuários
- gerenciar identidades
- conceder acesso a aplicações

Exemplos comuns:

- Google
- Microsoft
- GitHub

Esse modelo permite **identidade federada**, onde um único login acessa vários serviços.

---

# Gestão de Privilégios

## Princípio do Menor Privilégio

Usuários devem possuir **apenas as permissões necessárias para realizar suas tarefas**.

Benefícios:

- reduz impacto de ataques
- limita movimentação lateral
- melhora controle de acesso

---

## Separação de Funções

Nenhuma pessoa deve ter **controle total sobre um processo crítico**.

Exemplo:

- um funcionário cria uma solicitação
- outro aprova

Isso reduz riscos de:

- fraude
- abuso de poder
- erros operacionais

---

# Políticas de Segurança para Funcionários

## Recrutamento

Antes da contratação podem ocorrer:

- verificação de antecedentes
- validação de histórico profissional

Isso ajuda a reduzir **ameaças internas**.

---

## Onboarding

Onboarding é o processo de **integração de novos funcionários**.

Inclui:

- criação de contas
- definição de permissões
- entrega de equipamentos
- treinamento de segurança

---

## Offboarding

Offboarding é o processo de **desligamento seguro de funcionários**.

Inclui:

- desativar contas
- revogar acessos
- recolher equipamentos
- alterar credenciais compartilhadas

---

# NDA (Non Disclosure Agreement)

Um **NDA** é um acordo legal onde o funcionário se compromete a **não divulgar informações confidenciais da empresa**.

Protege:

- dados sensíveis
- segredos comerciais
- propriedade intelectual

---

# Tipos de Contas

## Conta de Usuário

Conta utilizada para atividades comuns do dia a dia.

---

## Conta Administrativa

Conta com privilégios elevados que permite:

- instalar softwares
- alterar configurações
- gerenciar usuários

Se comprometida, pode comprometer todo o sistema.

---

## Contas de Serviço

Utilizadas para executar serviços do sistema.

Tipos comuns:

- **System account**
- **Local service**
- **Network service**

---

## Contas Compartilhadas

São contas usadas por múltiplos usuários.

Problema:

- difícil rastrear ações
- menor controle de auditoria

---

## Contas de Equipamento

Associadas a dispositivos como:

- servidores
- impressoras
- equipamentos de rede

---

# Gestão de Credenciais

Credenciais são utilizadas para autenticação.

Podem incluir:

- senha
- certificados digitais
- tokens
- biometria
- smart cards

Uma boa gestão de credenciais envolve:

- criação segura
- armazenamento protegido
- revogação quando necessário
- auditoria de uso

---

# Chaves SSH

SSH Keys são usadas para autenticação segura em servidores.

Funcionamento:

- chave privada → mantida pelo usuário
- chave pública → armazenada no servidor

Vantagens:

- mais seguras que senhas
- resistentes a ataques de força bruta
- comuns em ambientes Linux e DevOps
