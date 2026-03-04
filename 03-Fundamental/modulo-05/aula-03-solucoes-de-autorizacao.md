# Authorization Solutions

## 📚 Aula 3 — Soluções de Autorização

Nesta aula são apresentados diferentes modelos e tecnologias utilizadas para **controlar quem pode acessar recursos em um sistema**.

Essas soluções ajudam a garantir que **somente usuários autorizados tenham acesso a dados e sistemas**, fortalecendo a segurança da informação.

---

# Objetivos da Aula

- Compreender modelos de controle de acesso
- Conhecer permissões do sistema de arquivos
- Entender serviços de diretório
- Explorar autenticação federada e protocolos de identidade

---

# Controle de Acesso

Controle de acesso é um conjunto de **políticas e mecanismos que determinam quem pode acessar um recurso e quais ações podem ser realizadas**.

Ele envolve:

- autenticação (quem é o usuário)
- autorização (o que ele pode fazer)

O objetivo é proteger **dados sensíveis e recursos críticos**.

---

# Modelos de Controle de Acesso

## DAC — Discretionary Access Control

O **DAC** permite que o proprietário de um recurso defina quem pode acessá-lo.

Características:

- controle feito pelo dono do recurso
- permissões podem ser alteradas livremente
- geralmente usa **ACL (Access Control List)**

Exemplo:

Um usuário cria um arquivo e decide quem pode:

- ler
- editar
- excluir

---

## RBAC — Role-Based Access Control

No **RBAC**, o acesso é baseado em **funções dentro da organização**.

Funcionamento:

1. Criam-se funções (roles)
2. Permissões são atribuídas às funções
3. Usuários recebem funções

Exemplo:

Empresa financeira:

- Gerente de projeto → acesso a relatórios
- Analista financeiro → acesso a dados financeiros
- Administrador de TI → acesso ao sistema

---

## MAC — Mandatory Access Control

O **MAC** utiliza políticas de segurança definidas pelo sistema.

Características:

- usuários não controlam permissões
- baseado em **níveis de classificação**

Exemplo de classificações:

- Público
- Confidencial
- Restrito

Usuários só acessam dados com **nível de segurança compatível**.

---

## ABAC — Attribute-Based Access Control

O **ABAC** usa atributos para tomar decisões de acesso.

Os atributos podem incluir:

- usuário
- recurso
- horário
- localização
- contexto da solicitação

Isso permite **controle de acesso mais dinâmico e granular**.

---

# Permissões em Sistemas de Arquivos

Sistemas Unix/Linux usam três permissões principais:

| Permissão | Significado |
|--------|--------|
| r | leitura |
| w | escrita |
| x | execução |

Exemplo de permissões:
rwxr-xr-x 

Onde:

- primeiro grupo → proprietário
- segundo → grupo
- terceiro → outros usuários

Comandos importantes:

### chmod

Define permissões.

Exemplo:
chmod +x arquivo.sh

---

# PAM — Privileged Access Management

O **PAM** é um sistema de controle para **contas privilegiadas**.

Seu objetivo é proteger acessos críticos.

Práticas comuns incluem:

- identificação de contas privilegiadas
- autenticação multifator
- monitoramento de atividades
- rotação de senhas
- auditoria de acesso

---

# Serviços de Diretório

Serviços de diretório armazenam informações sobre:

- usuários
- dispositivos
- recursos da rede

Eles organizam esses dados em estrutura hierárquica.

---

## LDAP

O **LDAP (Lightweight Directory Access Protocol)** é um protocolo usado para acessar diretórios.

Ele permite:

- buscar usuários
- autenticar usuários
- gerenciar identidades

---

## Estrutura do Diretório

Componentes comuns:

| Elemento | Significado |
|--------|--------|
| CN | Common Name |
| OU | Unidade Organizacional |
| O | Organização |
| C | País |
| DC | Domínio |

Exemplo:
CN=Joao, OU=Vendas, O=EmpresaABC, C=BR


---

# Federação de Identidade

A federação permite que **usuários utilizem uma única identidade em vários sistemas**.

Participantes:

- IdP (Identity Provider)
- SP (Service Provider)

Exemplo:

Login com Google em aplicativos externos.

---

# SAML

O **Security Assertion Markup Language (SAML)** é um protocolo usado para troca de informações de autenticação entre sistemas.

Fluxo básico:

1. Usuário tenta acessar serviço
2. Serviço redireciona para IdP
3. IdP autentica usuário
4. IdP envia token SAML
5. Usuário recebe acesso

---

# SOAP

SOAP é um protocolo baseado em XML utilizado para comunicação entre aplicações.

Ele define estrutura de mensagens para troca de dados entre sistemas.

---

# OAuth

O **OAuth** permite que aplicações acessem recursos de um usuário **sem compartilhar sua senha**.

Componentes:

- cliente
- servidor de autorização
- servidor de recursos
- usuário

Exemplo:

Login com Google em aplicativos.

---

# OpenID Connect (OIDC)

O **OpenID Connect** é uma camada de autenticação construída sobre o OAuth 2.0.

Ele permite:

- autenticação de usuários
- emissão de tokens de identidade
- integração segura entre aplicações.

---

# Conclusão

Soluções de autorização são fundamentais para controlar acessos em sistemas modernos.

Os principais modelos incluem:

- DAC
- RBAC
- MAC
- ABAC

Além disso, tecnologias como **LDAP, SAML, OAuth e OpenID Connect** são amplamente utilizadas para autenticação e controle de identidade.
