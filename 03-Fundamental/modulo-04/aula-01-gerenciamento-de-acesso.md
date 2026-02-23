# 🔐 Módulo 4 – Controles de Acesso
# Aulas 1 – Gerenciamento de Identidade e Autenticação

---

## 🎯 Objetivos de Aprendizagem

### **Aula 1:**
- ✅ Compreender os fundamentos do gerenciamento de identidade e acesso
- ✅ Explorar diferentes fatores e atributos de autenticação
- ✅ Analisar o design de autenticação e multifator de autenticação (MFA)

---

## 📚 Conceitos Fundamentais
- Fatores de Autenticação: Knowledge, Ownership, Biometric
- Atributos de Autenticação: Local, Comportamental, Baseado em Conhecidos
- Design de Autenticação e Multifator de Autenticação (MFA)
- 
---

## 🔍 Introdução

A **autenticação forte** é a primeira linha de defesa na batalha para proteger os recursos da rede. Existem diferentes métodos e mecanismos, alguns dos quais podem ser combinados para formar soluções mais eficazes.

**Projeto de Autenticação:**
Refere-se à criação e implementação de um sistema para verificar e validar a identidade de usuários antes de conceder acesso a determinados recursos, sistemas ou informações.

**Meta:**
Criar sistemas seguros e eficientes capazes de proteger contra acessos não autorizados, garantindo a integridade e confidencialidade das informações em ambientes digitais.

---

## 🔑 Gerenciamento de Identidade e Acesso (IAM)

### **Definição**

**IAM (Identity and Access Management):**
Disciplina de segurança da informação que se concentra em garantir a segurança, eficiência e conformidade nas interações de usuários com sistemas digitais.

**Abrange:**
- Criação e manutenção de identidades digitais
- Controle dos privilégios de acesso associados a essas identidades

---

### **Sistema de Controle de Acesso**

**Componentes:**

| Elemento | Descrição |
|----------|-----------|
| **Sujeitos** | Usuários, dispositivos, processos de software ou qualquer coisa que possa solicitar e ter acesso a um recurso |
| **Objetos** | Recursos (redes, servidores, bancos de dados, arquivos, etc.) |

---

### **Os 4 Processos Principais do IAM**

#### **1. Identificação**

**Definição:**
Processo de estabelecer a presença digital única de um usuário em um sistema.

**Como funciona:**
- Atribuição de identidade única
- Geralmente através de um nome de usuário ou ID exclusivo
- Criação de uma conta ou ID que represente o usuário, dispositivo ou processo

**Importância:**
✅ Primeiro passo para a construção de perfis digitais  
✅ Permite que o sistema reconheça e diferencie usuários individuais  

**Exemplo:**
```
Usuário: joao.silva
ID único: 12345
```

---

#### **2. Autenticação**

**Definição:**
Processo de verificar se a identidade apresentada é legítima.

**Como funciona:**
- Realizado através de credenciais:
  - Senhas
  - Tokens
  - Métodos biométricos

**Importância:**
✅ Assegura que apenas usuários autorizados tenham acesso aos recursos  
✅ Fortalece a segurança  

**É a prova de que um sujeito é quem afirma ser quando tenta acessar o recurso.**

---

#### **3. Autorização**

**Definição:**
Determina as permissões e privilégios concedidos a um usuário autenticado.

**Como funciona:**
- Estabelece quais direitos os sujeitos devem ter sobre cada recurso
- Faz cumprir esses direitos
- Baseia-se nas políticas de segurança e no perfil do usuário

**Importância:**
✅ Garante que os usuários tenham acesso apenas aos recursos relevantes às suas funções  
✅ Implementa o princípio do menor privilégio  

**Exemplo:**
```
Usuário: João Silva
Cargo: Analista
Permissões: Leitura (Sim), Escrita (Não), Exclusão (Não)
```

---

#### **4. Contabilidade (Accounting)**

**Definição:**
Registro e monitoramento das atividades do usuário.

**Como funciona:**
- Rastreia o uso autorizado de um recurso
- Rastreia o uso de direitos por um sujeito
- Alerta quando uso não autorizado é detectado ou tentado
- Cria uma trilha de auditoria

**Importância:**
✅ Reforça a responsabilidade  
✅ Fornece visão abrangente das ações realizadas no sistema  
✅ Contribui para detecção precoce de atividades suspeitas  
✅ Suporta análise de segurança e conformidade  

---

### **IAM e Definição de Atributos**

O IAM permite definir os atributos que compõem a identidade de uma entidade:
- Finalidade
- Função
- Habilitação de segurança
- E muito mais

**Benefício:**
Esses atributos permitem que os sistemas de gerenciamento de acesso tomem **decisões informadas** sobre:
- Conceder ou negar acesso a uma entidade
- Se concedido, decidir o que a entidade tem autorização para fazer

**Exemplo prático:**
```
Funcionário: Maria Santos
Departamento: TI
Cargo: Gerente de Segurança
Clearance: Confidencial

Decisão do sistema:
✅ Acesso concedido aos logs de segurança
✅ Acesso concedido aos relatórios de incidentes
❌ Acesso negado aos dados financeiros
```

---

### **AAA vs IAAA**

**AAA (Authentication, Authorization, Accounting):**
Servidores e protocolos que implementam estas três funções.

**IAAA:**
Inclui a fase de **Identificação**, que está sendo cada vez mais reconhecida como importante.

**Tendência:**
O uso do IAM para descrever processos e fluxos de trabalho empresariais está se tornando cada vez mais predominante.

---

## 🔐 Fatores de Autenticação

**Definição:**
Métodos e elementos utilizados para verificar a identidade de um usuário antes de conceder acesso a sistemas, dispositivos ou informações sensíveis.

**Importância:**
Cada fator desempenha um papel essencial na criação de sistemas de autenticação robustos. Muitas implementações bem-sucedidas **combinam vários desses elementos** para criar uma defesa multicamadas contra acessos não autorizados.

---

### **1. Knowledge Factor (Algo que Você Conhece)**

**Definição:**
Autenticação baseada em informações que o usuário conhece.

**Inclui:**
- 🔑 Senhas
- 🔢 Personal Identification Numbers (PIN)
- ❓ Respostas a perguntas específicas
- 📝 Passphrases (senhas longas compostas por várias palavras)

**Vantagens de Passphrases:**
✅ Mais seguras que senhas curtas  
✅ Mais fáceis de lembrar  

**Desafios:**
❌ Necessidade de criar senhas robustas  
❌ Gestão adequada para evitar vulnerabilidades  
❌ Usuários tendem a escolher senhas fracas  

**Exemplos:**
- Senhas de contas online
- Códigos PIN de cartões bancários
- Respostas a perguntas de segurança (nome do primeiro animal de estimação)

---

### **2. Ownership Factor (Algo que Você Tem)**

**Definição:**
Autenticação que requer que o usuário possua um objeto específico para confirmar sua identidade.

**Inclui:**
- 💳 Cartões inteligentes
- 🔐 Tokens de segurança
- 📱 Dispositivos físicos
- 🔑 Chaves de hardware

**Vantagens:**
✅ Adiciona camada extra de segurança  
✅ Invasor precisaria possuir fisicamente o objeto  
✅ Comum em ambientes corporativos  

**Como funciona:**
- Cartões de acesso geram códigos temporários
- Tokens geram códigos por tempo limitado
- Sincronização com servidor de autenticação

**Exemplos:**
- Cartões de acesso magnético
- Tokens de autenticação por tempo limitado (OTP)
- Chaves de hardware (YubiKey, Google Titan Key)
- Smartphones com aplicativos autenticadores

---

### **3. Biometric Factor (Algo que Você É ou Faz)**

**Definição:**
Autenticação que utiliza características únicas do corpo ou comportamentos individuais para confirmar a identidade.

**Características Corporais:**
- 👆 Impressões digitais
- 👤 Reconhecimento facial
- 👁️ Íris/Retina
- 🗣️ Voz
- 🖐️ Geometria da mão

**Características Comportamentais:**
- ⌨️ Padrões de digitação
- 🖱️ Movimento do mouse
- 🚶 Padrões de caminhada

**Vantagens:**
✅ Altamente personalizado (características únicas)  
✅ Difícil de falsificar  
✅ Não pode ser esquecido ou perdido  

**Desafios:**
❌ Necessidade de sistemas robustos  
❌ Lidar com avarias ou falsificações biométricas  
❌ Custo de implementação  
❌ Questões de privacidade  

**Exemplos:**
- Desbloqueio de smartphones por reconhecimento facial
- Leitores de impressões digitais para acesso a edifícios
- Autenticação por voz em sistemas de segurança
- Scanners de íris em aeroportos

---

## 🎨 Design de Autenticação

### **Definição**

Criação e implementação de estratégias, políticas, processos e sistemas que verificam e validam a identidade de usuários antes de conceder acesso a meios ou informações.

**Abrange:**
- Variedade de métodos e tecnologias
- Assegurar que apenas usuários autorizados possam interagir com recursos específicos

---

### **Requisitos do Design de Autenticação**

O design deve atender aos requisitos da **Tríade CIA:**

#### **1. Confidencialidade**

**Em termos de autenticação:**
É crítica porque se as credenciais da conta vazarem, agentes de ameaça podem:
- Se passar pelo titular da conta
- Agir no sistema com quaisquer direitos que possuam

**Requisitos:**
- Proteção de credenciais em trânsito
- Proteção de credenciais em repouso
- Criptografia forte

---

#### **2. Integridade**

**Significa que:**
O mecanismo de autenticação é confiável e não é fácil para agentes de ameaça:
- Contornarem
- Enganarem com credenciais falsas

**Requisitos:**
- Validação forte de credenciais
- Proteção contra falsificação
- Mecanismos anti-replay

---

#### **3. Disponibilidade**

**Significa que:**
O tempo necessário para autenticação:
- Não impede os fluxos de trabalho
- É bastante fácil para os usuários operarem

**Requisitos:**
- Tempo de resposta aceitável
- Alta disponibilidade do sistema
- Facilidade de uso

---

### **Aplicações Práticas do Design de Autenticação**

#### **1. Políticas de Senhas e Senhas Fortes**

**Implementação:**
- Senhas robustas
- Políticas efetivas de gerenciamento de senhas

**Elementos-chave:**
✅ Senhas complexas  
✅ Autenticação em dois fatores  
✅ Expiração regular de senhas  
✅ Histórico de senhas (evitar reutilização)  

**Exemplo de política:**
```
Requisitos de senha:
- Mínimo 12 caracteres
- Incluir: maiúsculas, minúsculas, números, símbolos
- Não pode conter nome de usuário
- Não pode ser senha anterior (últimas 5)
- Expiração: 90 dias
- Bloqueio após 5 tentativas falhadas
```

---

#### **2. Biometria**

**Sistemas que utilizam:**
- Impressões digitais
- Reconhecimento facial
- Reconhecimento de voz

**Benefícios:**
✅ Design de autenticação avançado  
✅ Camada adicional de segurança  
✅ Baseados em atributos únicos de cada indivíduo  

**Considerações:**
- Falsos positivos/negativos
- Armazenamento seguro de dados biométricos
- Backup para falhas de leitura

---

#### **3. Tokenização**

**Como funciona:**
Geração de códigos temporários por meio de:
- Tokens físicos
- Aplicativos autenticadores

**Características:**
✅ Abordagem eficaz no design de autenticação  
✅ Códigos dinâmicos  
✅ Apenas quem possui o dispositivo específico pode autenticar  

**Tipos:**
- **HOTP:** HMAC-based One-Time Password (baseado em contador)
- **TOTP:** Time-based One-Time Password (baseado em tempo)

**Exemplo TOTP:**
```
Código gerado: 123456
Validade: 30 segundos
Algoritmo: SHA-1
```

---

## 🔒 Multifator de Autenticação (MFA)

### **Definição**

Abordagem de segurança que exige que os usuários forneçam **mais de uma forma** de verificação de identidade para acessar um sistema ou recurso.

**Ao invés de:**
Depender apenas de uma única credencial (como senha)

**O MFA incorpora:**
Múltiplos fatores, aumentando significativamente a robustez da autenticação

---

### **Por Que MFA?**

✅ **Estratégia eficaz** para mitigar riscos associados a acessos não autorizados  
✅ Proporciona **camadas adicionais de proteção**  
✅ Protege mesmo se uma credencial for comprometida  
✅ Atende requisitos de compliance (PCI-DSS, HIPAA, etc.)  

**Princípio:**
Combinar fatores de **categorias diferentes** (Knowledge + Ownership, por exemplo)

---

### **Exemplos de Usos do MFA**

#### **1. Senha + Token**

**Cenário:**
Um usuário fornece sua senha convencional e, simultaneamente, um código gerado por um token físico ou aplicativo autenticador.

**Reforço de Segurança:**
Mesmo se a senha for comprometida, o acesso ainda é negado sem o token adicional.

**Implementação:**
```
Passo 1: Usuário digita senha (Knowledge)
Passo 2: Usuário digita código do token (Ownership)
Passo 3: Sistema valida ambos
Resultado: Acesso concedido
```

---

#### **2. Impressão Digital + Senha**

**Cenário:**
Além de digitar uma senha, o usuário precisa autenticar sua identidade por meio de uma leitura de impressão digital.

**Reforço de Segurança:**
Combinação de:
- Algo que o usuário **sabe** (senha)
- Algo que o usuário **é** (impressão digital)

**Benefício:**
Aumenta significativamente a segurança, pois requer tanto conhecimento quanto biometria.

---

#### **3. Reconhecimento Facial + Confirmação via Dispositivo**

**Cenário:**
1. Reconhecimento facial valida identidade
2. Usuário recebe notificação no dispositivo móvel
3. Usuário confirma a autenticação no dispositivo

**Reforço de Segurança:**
Combinação de:
- Validação biométrica (o que você é)
- Fator de propriedade (dispositivo móvel)

**Exemplo prático:**
```
Usuário tenta login no laptop
→ Sistema solicita reconhecimento facial
→ Facial validado com sucesso
→ Notificação push enviada ao smartphone
→ Usuário aprova no smartphone
→ Acesso concedido
```

---

## 🎯 Atributos de Autenticação

**Definição:**
Comparado aos três principais fatores de autenticação, um atributo de autenticação é uma **propriedade ou fator não exclusivo**, ou seja, que **não pode ser usado independentemente**.

**Diferença dos Fatores:**
Atributos são usados como **mecanismos complementares** ou de autenticação contínua, não como fatores primários.

---

### **1. Autenticação Baseada em Local**

**Definição:**
Valida a identidade do usuário com base em sua **localização física**.

**Como funciona:**
Pode envolver o uso de:
- Dispositivos de geolocalização (GPS)
- Endereço IP
- Localização geográfica por serviço de geolocalização
- Localização física por porta de rede
- VLAN (Virtual LAN)
- Rede Wi-Fi específica

**Uso típico:**
- ❌ **Não usado** como fator de autenticação primário
- ✅ Usado como **mecanismo de autenticação contínua**
- ✅ Usado como **recurso de controle de acesso**

---

**Exemplos de Aplicação:**

**Exemplo 1: Gateway VPN**
```
Usuário insere credenciais corretas
↓
Sistema verifica endereço IP
↓
IP mostra país diferente do esperado
↓
Ações possíveis:
- Aplicar controles de acesso mais restritivos
- Recusar completamente o acesso
- Solicitar autenticação adicional (MFA)
```

**Exemplo 2: Viagem Impossível**
```
Login 1: São Paulo, Brasil - 10:00 AM
Login 2: Tóquio, Japão - 10:30 AM

Sistema detecta: Fisicamente impossível
Ação: Bloquear acesso, alertar usuário
```

---

**Usos Práticos:**

| Cenário | Aplicação |
|---------|-----------|
| **Acesso a Redes Corporativas** | Garantir acesso apenas quando usuário em locais predefinidos |
| **Transações Financeiras** | Autorizar transações apenas se usuário próximo ao ponto de compra |
| **Acesso a Dados Sensíveis** | Bloquear acesso de países de alto risco |
| **Compliance** | Garantir acesso apenas de jurisdições permitidas |

---

### **2. Autenticação Baseada em Comportamento (Algo que Você Pode Fazer)**

**Definição:**
Leva em consideração os **padrões de comportamento** do usuário.

**Características Analisadas:**
- ⌨️ Velocidade de digitação
- 📱 Forma como segura um dispositivo
- 🖱️ Maneira como navega em uma página
- 🚶 Padrões de caminhada
- 📲 Como segura o smartphone

**Funcionamento:**
Características comportamentais podem identificá-lo de maneira única em um número considerável de atividades.

**Limitação:**
❌ Impraticável para autenticação primária  
✅ Pode ser usado para **autenticação contextual e contínua**  
✅ Garante que dispositivo continue operado pelo proprietário  

---

**Exemplos de Uso:**

**1. Verificação Contínua**
```
Sistema monitora constantemente:
- Padrão de digitação
- Velocidade de cliques
- Movimentação do mouse

Desvio detectado:
→ Solicitar reautenticação
```

**2. Prevenção contra Ameaças Internas**
```
Comportamento normal do usuário:
- Acessa 10-15 arquivos/dia
- Trabalha das 9h às 18h

Comportamento anômalo detectado:
- Acessou 500 arquivos em 1 hora
- Acesso às 3h da manhã
→ Alerta de segurança gerado
```

---

### **3. Autenticação Baseada em Algo que Você Exibe (Comportamental)**

**Definição:**
Considera como um usuário **interage com interfaces digitais**.

**Análise de Padrões:**
- 🖱️ Movimentos do mouse
- 🖱️ Velocidade de cliques
- ⌨️ Maneira como digita

**Ênfase específica:**
Traços de personalidade capturados por análise de aprendizado de máquina.

**Exemplo de análise:**
```
Padrão de uso de apps do smartphone:
- Preferências de aplicativos
- Horários de uso
- Frequência de uso
- Padrões de navegação web

Machine Learning cria modelo estatístico:
→ Se outra pessoa usar o dispositivo
→ Comportamento será diferente
→ Padrão anômalo detectado
→ Dispositivo bloqueado
→ Reautenticação exigida
```

---

**Exemplos de Uso:**

| Cenário | Aplicação |
|---------|-----------|
| **Prevenção de Fraudes** | Identificar atividades fraudulentas por variações no comportamento |
| **Identificação Contínua** | Adaptar autenticação com base no comportamento ao longo do tempo |
| **Detecção de Account Takeover** | Identificar quando conta foi comprometida |

---

### **4. Autenticação Baseada em Alguém que Você Conhece**

**Definição:**
Envolve autenticação com base no **conhecimento de relações pessoais** ou redes sociais.

**Pode incluir:**
- ❓ Perguntas sobre pessoas conhecidas
- 👥 Validação através de contatos de confiança
- 🌐 Modelo de rede de confiança

---

**Modelo de Rede de Confiança:**

**Como funciona:**
Usa um esquema onde **novos usuários são garantidos por usuários existentes**.

**Processo:**
```
Novo usuário se junta à rede
↓
Usuário existente garante identidade
↓
À medida que usuário participa
↓
Identidade fica mais estabelecida
```

**Exemplo: PGP Web of Trust**

**PGP (Pretty Good Privacy):**
- Software de criptografia de chave pública altamente seguro
- Originalmente escrito por Philip Zimmermann
- Tornou-se padrão de fato para criptografia de e-mail na internet

**Web of Trust:**
Modelo descentralizado usado pelo PGP como alternativa à PKI (Public Key Infrastructure).

---

**Exemplos de Uso:**

| Cenário | Aplicação |
|---------|-----------|
| **Recuperação de Conta** | Verificação via informações sobre pessoas conhecidas |
| **Acesso a Informações Sensíveis** | Conhecidos como camada adicional de autenticação |
| **Validação de Identidade** | Contatos confiáveis confirmam identidade |

---

## 💡 Conclusão

### **Principais Takeaways**

**Aula 1 - Gerenciamento de Identidade:**

✅ **IAM é fundamental** para segurança organizacional  
✅ **4 processos (IAAA)** formam base do gerenciamento de acesso  
✅ **3 fatores principais** de autenticação (Knowledge, Ownership, Biometric)  
✅ **MFA combina fatores** para máxima segurança  
✅ **Atributos complementam** fatores de autenticação  
✅ **Design de autenticação** deve balancear segurança e usabilidade  


---

## 🔗 Conceitos Relacionados

- **Zero Trust Architecture:** Nunca confie, sempre verifique
- **RBAC:** Role-Based Access Control
- **ABAC:** Attribute-Based Access Control
- **PKI:** Public Key Infrastructure
- **Certificate Authority:** Autoridade certificadora
- **LDAP:** Lightweight Directory Access Protocol
- **RADIUS:** Remote Authentication Dial-In User Service
- **TACACS+:** Terminal Access Controller Access-Control System Plus

---

## 📚 Glossário de Termos

| Termo | Definição |
|-------|-----------|
| **IAM** | Identity and Access Management - Gerenciamento de identidade e acesso |
| **IAAA** | Identification, Authentication, Authorization, Accounting |
| **MFA** | Multi-Factor Authentication - Autenticação multifator |
| **2FA** | Two-Factor Authentication - Autenticação de dois fatores |
| **SSO** | Single Sign-On - Logon único |
| **PAM** | Pluggable Authentication Modules - Módulos de autenticação plugáveis |
| **Kerberos** | Protocolo de autenticação de rede |
| **NTLM** | NT LAN Manager - Protocolo de autenticação Windows legado |
| **TGT** | Ticket Granting Ticket - Bilhete inicial do Kerberos |
| **LSA** | Local Security Authority - Autoridade de segurança local |
| **SAM** | Security Accounts Manager - Gerenciador de contas de segurança |
| **CHAP** | Challenge Handshake Authentication Protocol |
| **Hash** | Função criptográfica unidirecional |
| **Salt** | Valor aleatório adicionado ao hash para maior segurança |
| **Rainbow Table** | Tabela pré-computada de hashes |
| **Credential Stuffing** | Uso de credenciais vazadas em múltiplos sites |
| **Password Spraying** | Ataque horizontal com senhas comuns |
| **Brute Force** | Tentativa de todas as combinações possíveis |

---
