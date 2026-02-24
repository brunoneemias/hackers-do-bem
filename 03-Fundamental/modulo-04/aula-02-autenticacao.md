# 🎓 AULA 2 – Autenticação Baseada em Conhecimento

## 🔍 Introdução

A **autenticação baseada em conhecimento** refere-se principalmente à criação de credenciais de usuários com mecanismos de acesso à conta baseados em senha.

**Importância:**
- Configurar protocolos de autenticação baseados em senha
- Fornecer suporte a usuários com problemas de autenticação
- Parte importante da função de segurança da informação

**Nesta aula aprenderemos:**
- Como funcionam protocolos de autenticação comuns
- Como podem ser configurados
- Técnicas de quebra de senha

---

## 🔐 Autenticação Local, de Rede e Remota

### **Provedor de Autenticação**

**Definição:**
Um dos recursos mais importantes de um sistema operacional é o **provedor de autenticação**.

**O que é:**
- Arquitetura de software e código
- Sustenta o mecanismo pelo qual o usuário é autenticado
- Antes de iniciar um shell

**Nomes comuns:**
- **Login** (Linux)
- **Logon** ou **Sign-in** (Microsoft)

**Padrão:**
Autenticação baseada em conhecimento, usando senha ou PIN, é o provedor de autenticação padrão para a maioria dos sistemas operacionais.

---

### **Processo de Login**

**Definição:**
Sequência de passos pelos quais um usuário fornece suas credenciais para acessar um sistema, aplicativo ou recurso protegido.

**Credenciais geralmente consistem em:**
- Nome de usuário (ou identificador)
- Senha ou PIN

**Podem também incluir:**
- Autenticação biométrica (impressão digital, reconhecimento facial)
- Tokens de segurança

---

### **Hashes Criptográficos**

**Por que usar hashes?**

**Risco:**
Uma senha em texto simples geralmente **não é transmitida** ou **armazenada** em um banco de dados devido ao risco de comprometimento.

**Solução:**
Senha é armazenada como um **hash criptográfico**.

---

**Como funciona:**

```
Cadastro de senha:
Usuário cria senha: "Senh@Forte123"
↓
Sistema aplica função hash (ex: SHA-256)
↓
Hash gerado: "a3f5e9c2d8b1..."
↓
Hash armazenado no banco de dados
```

```
Login:
Usuário digita senha: "Senh@Forte123"
↓
Autenticador converte em hash
↓
Hash transmitido para autoridade
↓
Autoridade compara com hash do banco
↓
Se corresponderem: Autenticado ✅
Se não: Acesso negado ❌
```

**Benefício:**
Mesmo administradores não conhecem a senha em texto claro.

---

### **Passos do Processo de Login**

#### **1. Identificação do Usuário**

**O que acontece:**
Usuário fornece um identificador exclusivo.

**Exemplos:**
- Nome de usuário
- Endereço de e-mail
- Número de identificação

---

#### **2. Fornecimento de Credenciais**

**O que acontece:**
Usuário informa a senha associada ao identificador fornecido.

**Pode incluir:**
- Inserção de código de autenticação
- Uso de métodos biométricos
- Inserção de token

---

#### **3. Envio das Credenciais ao Sistema**

**O que acontece:**
Informações de identificação e credenciais são enviadas ao sistema de autenticação.

**Destino:**
- Localmente no dispositivo, ou
- Em um servidor remoto

---

#### **4. Validação das Credenciais**

**O que acontece:**
Sistema verifica correspondência entre:
- Credenciais fornecidas
- Credenciais armazenadas em sua base de dados

**Resultado:**
Se credenciais válidas → Usuário autenticado

---

#### **5. Concessão de Acesso**

**O que acontece:**
Uma vez autenticado com sucesso, sistema concede ao usuário acesso aos:
- Recursos
- Serviços
- Informações autorizados

---

#### **6. Geração de Sessão**

**O que acontece:**
Uma sessão é estabelecida para o usuário.

**Benefício:**
Permite interação contínua com o sistema **sem necessidade de autenticação repetida** durante um período específico.

**Componentes de sessão:**
- Session ID
- Timeout
- Tokens de acesso

---

## 🖥️ Tipos de Autenticação

### **1. Autenticação Local**

**Definição:**
Processo de verificar a identidade de um usuário em um **dispositivo específico**.

**Características:**
- Usuário interage diretamente com o sistema
- Como um computador pessoal ou dispositivo móvel
- Para ganhar acesso aos recursos locais

**Implementação Prática:**

| Método | Exemplo |
|--------|---------|
| **Senhas/PINs** | Acesso a computador pessoal |
| **Biometria** | Leitores de impressões digitais em smartphones |
| **Padrão de desbloqueio** | Padrão gráfico em tela touch |

---

### **2. Autenticação de Rede**

**Definição:**
Expande o escopo para incluir acesso a **recursos compartilhados em uma rede corporativa**.

**Características:**
- Verificação de identidade **não ocorre no dispositivo local**
- Ocorre em um **servidor central**
- Exemplo: Active Directory no ecossistema Windows

**Implementação Prática:**

**Protocolo LDAP:**
- Usado para autenticar usuários em servidor centralizado
- LDAP (Lightweight Directory Access Protocol)

**Active Directory (AD):**
- Usuários autenticam credenciais em servidor central
- Ao ingressar na rede
- Permite acesso a recursos compartilhados:
  - Servidores de arquivos
  - Impressoras
  - Aplicativos

**Benefícios:**
✅ Garante integridade dos dados  
✅ Garante segurança dos dados  
✅ Gerenciamento centralizado  

---

### **3. Autenticação Remota**

**Definição:**
Permite validação da identidade de usuários que buscam acessar recursos **a partir de locais geograficamente distintos**.

**Importância:**
Essencial para:
- Organizações com equipes distribuídas globalmente
- Organizações que permitem trabalho remoto

**Implementação Prática:**

**VPNs (Redes Privadas Virtuais):**
Exemplo notável de autenticação remota.

**Como funciona:**
```
Usuário remoto em casa
↓
Conecta à VPN corporativa
↓
Conexão segura estabelecida
↓
Túnel criptografado criado
↓
Autenticação remota realizada
↓
Como se estivesse fisicamente na sede
```

**Benefícios:**
✅ Acesso seguro de qualquer local  
✅ Criptografia end-to-end  
✅ Mesmas políticas de segurança da rede local  

---

## 🪟 Autenticação no Windows

**Arquitetura:**
Envolve uma complexa arquitetura de componentes.

**Cenários típicos:**

### **1. Sign-in Local (Logon Interativo)**

**Como funciona:**
- Autenticação realizada no próprio dispositivo
- Usuário fornece credenciais diretamente
- Para acessar recursos específicos

**Processo técnico:**
```
Usuário insere credenciais
↓
LSA (Local Security Authority) recebe
↓
LSA compara credencial enviada
↓
Com hash armazenado no SAM
↓
SAM (Security Accounts Manager)
↓
Parte do registro do Windows
↓
Se corresponder: Acesso concedido
```

**Componentes:**

**LSA (Local Security Authority):**
- Componente do sistema operacional Windows
- Responsável por:
  - Implementação de políticas de segurança locais
  - Autenticação de usuários
  - Controles de acesso
  - Manutenção de informações de segurança no nível local

**SAM (Security Accounts Manager):**
- Banco de dados local de contas
- Armazena hashes de senhas
- Parte do registro do Windows

---

### **2. Autenticação de Rede no Windows**

**Gerenciamento:**
Amplamente gerenciado pelo **Active Directory (AD)**.

**Como funciona:**
```
Usuário tenta acessar recurso compartilhado
↓
Credenciais enviadas
↓
Controlador de domínio no AD verifica
↓
Validação centralizada
↓
Políticas de segurança aplicadas
```

**Benefícios:**
✅ Abordagem centralizada  
✅ Aplicação consistente de políticas em toda rede  
✅ Gestão eficiente de usuários e grupos  

**Processo técnico:**
```
LSA passa credenciais para serviço de rede
↓
Sistema preferencial: Kerberos
↓
Aplicativos herdados: NTLM
```

---

### **Kerberos - Protocolo Preferencial**

**O que é:**
Protocolo de autenticação forte que visa proporcionar forma segura de autenticar usuários em redes.

**Uso:**
Especialmente utilizado em ambientes que fazem parte de um domínio do Active Directory.

**Como funciona:**

**Modelo de Bilhete:**

```
1. Usuário se autentica no domínio
   ↓
2. Sistema emite TGT (Ticket Granting Ticket)
   ↓
3. TGT usado para solicitar outros tickets de serviço
   ↓
4. Acesso a recursos específicos
   ↓
5. Sem necessidade de reautenticação
```

**Componentes principais:**

| Componente | Função |
|------------|--------|
| **KDC** | Key Distribution Center - Centro de distribuição de chaves |
| **TGT** | Ticket Granting Ticket - Bilhete inicial |
| **Service Ticket** | Bilhete para acessar serviço específico |
| **AS** | Authentication Server - Servidor de autenticação |
| **TGS** | Ticket Granting Server - Servidor de bilhetes |

**Segurança:**
✅ Protocolo altamente seguro  
✅ Utiliza técnicas de criptografia  
✅ Protege credenciais durante autenticação  
✅ Protege comunicação entre sistemas  
✅ Minimiza risco de replay attacks  
✅ Minimiza risco de man-in-the-middle attacks  

---

### **NTLM - Protocolo Legado**

**O que é:**
Protocolo de autenticação mais antigo, ainda suportado no Windows por razões de compatibilidade.

**Segurança:**
❌ Não oferece o mesmo nível de segurança que o Kerberos

**Como funciona:**

**Desafio-Resposta:**
```
1. Usuário tenta acessar recurso
   ↓
2. Servidor emite desafio
   ↓
3. Cliente responde com versão hasheada da senha
   ↓
4. Servidor valida resposta
```

**Limitações:**

❌ Forma básica de autenticação  
❌ Senhas armazenadas em hash de 8 caracteres  
❌ Mais vulnerável a ataques  
❌ Não oferece proteções contra ataques sofisticados como Kerberos  

**Quando é usado:**
- Aplicativos legados
- Autenticação de workgroup (sem domínio)
- Fallback quando Kerberos não disponível

---

### **3. Autenticação Remota no Windows**

**Tecnologias:**

**SSTP (Secure Socket Tunneling Protocol):**
Para VPNs.

**Como funciona:**
```
Usuário remoto autentica via conexão segura
↓
Geralmente usando certificados digitais
↓
Ou outros métodos seguros
↓
Autenticação ocorre como se estivesse fisicamente na rede
```

**Relevância:**
Particularmente importante quando equipe precisa acessar recursos da empresa de locais externos.

---

## 🐧 Autenticação no Linux

### **1. Login Local**

**Autenticação local envolve:**
- Senhas
- Chaves de autenticação SSH
- Outros métodos (dependendo da configuração)

**Arquivos de Configuração:**

**`/etc/passwd`:**
- Armazena nomes das contas de usuários locais
- Informações públicas do usuário

**`/etc/shadow`:**
- Armazena hashes de senhas
- Somente root pode ler
- Quando usuário efetua login em shell interativo local
- Senha é verificada no hash armazenado aqui

**Formato do /etc/shadow:**
```
username:$6$salt$hash:lastchange:min:max:warn:inactive:expire:reserved
```

---

### **2. Autenticação de Rede no Linux**

**SSH (Secure Shell):**

**Como funciona:**
Login interativo em rede realizado usando SSH.

**Métodos de autenticação:**
- Chaves criptográficas (em vez de senha)
- Senhas (menos seguro)

**Vantagens das chaves SSH:**
✅ Mais seguras que senhas  
✅ Não transmitem credenciais  
✅ Resistentes a ataques de força bruta  

---

**PAM (Pluggable Authentication Modules):**

**O que é:**
Pacote para habilitar diferentes provedores de autenticação.

**Benefícios:**
✅ Flexibilidade na escolha de métodos de autenticação  
✅ Para diferentes serviços de rede  
✅ Integração com serviços de diretório (LDAP)  

**Exemplo de uso:**
```
Login com cartão inteligente
LDAP para autenticação centralizada
Kerberos em ambientes mistos
```

**Integração com LDAP:**
- Autenticar usuários em rede centralizada
- Similar ao Active Directory no Windows

---

### **3. Autenticação Remota no Linux**

**Protocolo principal: SSH**

**Métodos de autenticação:**
- Chaves SSH
- Senhas

**Benefícios:**
✅ Execução segura de comandos remotamente  
✅ Transferência segura de arquivos  

**Uso comum:**
- Administração de servidores Linux
- Servidores em data centers
- Servidores em nuvens (AWS, Azure, GCP)

**Exemplo de uso:**
```bash
# Conectar via SSH com chave
ssh -i ~/.ssh/id_rsa user@servidor.com

# Copiar arquivo via SCP
scp arquivo.txt user@servidor.com:/home/user/

# Tunelamento SSH
ssh -L 8080:localhost:80 user@servidor.com
```

---

**PAM para Servidores de Rede:**

**Uso:**
Estrutura PAM também pode ser usada para implementar autenticação em servidores de redes.

**Benefícios:**
✅ Configuração flexível  
✅ Múltiplos módulos de autenticação  
✅ Integração com diversos backends  

---

## 🔐 Single Sign-On (SSO)

### **Definição**

Sistema de logon único que permite que o usuário:
- Se autentique **uma vez** em um dispositivo local
- Seja autenticado em servidores de aplicativos compatíveis
- **Sem precisar inserir credenciais novamente**

**Benefícios principais:**
✅ Simplifica a experiência do usuário  
✅ Melhora a segurança (reduz número de senhas)  
✅ Reduz fadiga de senha  
✅ Menor risco de senhas fracas  

---

### **SSO no Windows**

**Implementação:**
Fornecido pela estrutura **Kerberos**.

**Como funciona:**
```
Usuário faz login no Windows
↓
Kerberos autentica
↓
TGT (Ticket Granting Ticket) emitido
↓
Usuário acessa recurso (ex: SharePoint)
↓
Sistema usa TGT para obter Service Ticket
↓
Acesso concedido sem nova senha
```

---

### **Padrões e Protocolos de SSO**

SSO é implementado usando diferentes padrões:

| Padrão | Descrição |
|--------|-----------|
| **OAuth** | Autorização delegada |
| **OpenID Connect** | Camada de identidade sobre OAuth 2.0 |
| **SAML** | Security Assertion Markup Language |

**Escolha depende de:**
- Requisitos do ambiente
- Características da implementação

---

### **Etapas do Processo SSO**

#### **1. Autenticação Inicial**

**O que acontece:**
Processo começa quando usuário realiza autenticação inicial em um dos serviços conectados ao sistema SSO.

**Normalmente envolve:**
Fornecimento de credenciais (nome de usuário e senha)

---

#### **2. Emissão de Token de Sessão**

**O que acontece:**
Após autenticação bem-sucedida, sistema SSO emite um **token de sessão** para o usuário.

**Token:**
- Identificador único
- Contém informações sobre autenticação do usuário
- Assinado criptograficamente

---

#### **3. Armazenamento Seguro do Token**

**Onde é armazenado:**

**Lado do cliente:**
- Cookie (geralmente)
- Armazenamento local do navegador

**Lado do servidor:**
- Banco de dados de sessões
- Cache distribuído

**Benefício:**
Permite validar identidade do usuário durante todo o processo de sessão.

---

#### **4. Acesso a Outros Serviços**

**Como funciona:**
```
Usuário tenta acessar outro serviço
↓
Token de sessão é apresentado
↓
Serviço utiliza token para verificar autenticidade
↓
Sem exigir novas credenciais
↓
Acesso concedido
```

---

#### **5. Renovação de Token**

**O que acontece:**
Periodicamente, token pode ser renovado para garantir segurança contínua.

**Características:**
✅ Geralmente feito sem interrupção para usuário  
✅ Mantém experiência SSO  
✅ Sem necessidade de reautenticação frequente  

---

#### **6. Logout Único (Single Logout)**

**O que acontece:**
Quando usuário decide encerrar sessão, SSO realiza um **logout único**.

**Resultado:**
- Revoga acesso a **todos os serviços** conectados simultaneamente
- Usuário desconectado de todos os serviços associados
- Com apenas uma ação

**Benefício:**
✅ Segurança aprimorada  
✅ Experiência de usuário consistente  

---

## 📡 Protocolos de Autenticação

### **1. PAP (Password Authentication Protocol)**

**Características:**

| Aspecto | Detalhe |
|---------|---------|
| **Segurança** | ❌ Menos seguro |
| **Transmissão** | Texto simples (sem criptografia) |
| **Adequação** | Ambientes onde segurança não é principal preocupação |

**Como funciona:**
```
Cliente envia:
- Nome de usuário (texto simples)
- Senha (texto simples)
↓
Servidor valida
↓
Resposta: Aceito/Rejeitado
```

**Vulnerabilidades:**
❌ Credenciais podem ser interceptadas  
❌ Suscetível a sniffing  
❌ Sem proteção contra replay attacks  

**Usos históricos:**
- Redes dial-up (descontinuado)
- Autenticação HTTP básica (não recomendado)

**Status atual:**
❌ Menos comum em ambientes modernos  
❌ Vulnerável a ataques de captura de dados  

---

### **2. CHAP (Challenge Handshake Authentication Protocol)**

**Características:**

| Aspecto | Detalhe |
|---------|---------|
| **Segurança** | ✅ Mais seguro que PAP |
| **Método** | Desafio e resposta |
| **Transmissão** | Senha nunca enviada em texto simples |

**Como funciona:**

**Processo de autenticação:**
```
1. Cliente solicita conexão
   ↓
2. Servidor envia desafio (valor aleatório)
   ↓
3. Cliente calcula resposta:
   Hash(senha + desafio)
   ↓
4. Cliente envia resposta hasheada
   ↓
5. Servidor valida:
   Compara com próprio cálculo
   ↓
6. Aceita ou rejeita
```

**Exemplo técnico:**
```
Servidor envia: desafio = "abc123"
Cliente calcula: MD5("minhaSenha" + "abc123")
Cliente envia: "d41d8cd98f00b204e9800998ecf8427e"
Servidor valida comparando com seu próprio cálculo
```

**Vantagens:**
✅ Senha não enviada pela rede  
✅ Proteção contra sniffing  
✅ Desafio diferente a cada autenticação  

**Usos:**
- Conexões PPP (Point-to-Point Protocol)
- Redes dial-up
- VPNs onde segurança da senha é preocupação

---

### **3. MS-CHAP (Microsoft Challenge Handshake Authentication Protocol)**

**Características:**

| Aspecto | Detalhe |
|---------|---------|
| **Origem** | Variação do CHAP desenvolvida pela Microsoft |
| **Melhorias** | Suporte à troca de senhas criptografadas |
| **Ambiente** | Frequentemente usado em ambientes Microsoft |

**Versões:**

**MS-CHAPv1:**
- Versão original
- Vulnerabilidades conhecidas
- ❌ Não recomendado

**MS-CHAPv2:**
- Versão melhorada
- ✅ Melhor segurança
- Autenticação mútua
- Chaves de criptografia mais fortes

**Usos comuns:**
- VPNs em ambientes Windows
- Conexões PPTP (Point-to-Point Tunneling Protocol)
- Autenticação em redes Microsoft

---

### **Comparação dos Protocolos**

| Aspecto | PAP | CHAP | MS-CHAP |
|---------|-----|------|---------|
| **Segurança** | ❌ Baixa | ✅ Média-Alta | ✅ Alta (v2) |
| **Criptografia** | ❌ Não | ✅ Sim | ✅ Sim |
| **Transmissão de senha** | Texto simples | Hash | Hash |
| **Adequação** | Baixa segurança | Segurança prioritária | Ambientes Windows |
| **Uso atual** | Raro | Comum | VPNs Windows |
| **Compatibilidade** | Universal | Ampla | Principalmente Microsoft |

---

## 🎯 Ataques de Senha

### **Conceito de Hash de Senha**

**Como funciona:**

**Criação de senha:**
```
Usuário escolhe senha: "MinhaSenha123"
↓
Sistema aplica função hash (MD5, SHA)
↓
Hash gerado e armazenado
↓
Texto simples não é recuperável do hash
```

**Teoria:**
Ninguém, exceto o usuário (nem mesmo o administrador do sistema), conhece a senha, porque o texto simples não deve ser recuperável a partir do hash.

**Tipos de ataques:**

---

### **1. Ataque de Texto Simples/Não Criptografado**

**O que é:**
Ataque que explora armazenamento de senhas ou protocolo de autenticação que **não usa criptografia**.

**Como ocorre:**
- Senhas transmitidas em formato legível
- Armazenadas sem criptografia
- Atacantes interceptam ou acessam diretamente

**Exemplos vulneráveis:**
- PAP
- Autenticação HTTP/FTP básica
- Telnet

**Tipos de violação:**
- Senhas em arquivo não gerenciado
- Senhas incorporadas no código do aplicativo
- Código carregado em repositório público

**Prevenção:**
✅ Utilizar comunicações seguras (HTTPS)  
✅ Armazenar senhas com hash e criptografia adequados  
✅ Nunca salvar senhas em texto simples  

---

### **2. Ataques Online**

**Definição:**
Ataque onde agente da ameaça interage **diretamente com o serviço de autenticação**.

**Exemplos de alvos:**
- Formulário de login na web
- Gateway VPN
- Portal de autenticação

**Como funciona:**
```
Atacante envia senhas usando:
- Banco de dados de senhas conhecidas
- Variações de senhas
- Lista de senhas quebradas offline
↓
Tentativas automáticas e contínuas
↓
Até encontrar combinação correta
```

**Características:**
- Tentativas automáticas e contínuas
- Exploram capacidade de tentar repetidamente
- Procuram combinação correta de usuário e senha

**Prevenção:**
✅ Bloqueios automáticos após tentativas mal sucedidas  
✅ Autenticação de dois fatores (2FA)  
✅ Senhas fortes  
✅ CAPTCHA  
✅ Rate limiting  

---

### **3. Pulverização de Senhas (Password Spraying)**

**O que é:**
Ataque online **horizontal** de força bruta.

**Como funciona:**
```
Atacante escolhe senhas comuns:
- "senha"
- "123456"
- "admin"
- "Verão2024"
↓
Testa em conjunto com vários nomes de usuário
↓
Poucas tentativas por conta
↓
Evita detecção automática
```

**Estratégia:**
- Limita número de tentativas por conta
- Evita bloqueios automáticos
- Mais difícil de detectar

**Exemplo:**
```
Senha "123456" testada em:
- usuario1
- usuario2
- usuario3
- ... (centenas de usuários)
↓
Apenas 1 tentativa por usuário
↓
Não aciona bloqueio
```

**Prevenção:**
✅ Monitorar padrões de login  
✅ Bloqueios baseados em comportamento  
✅ Ferramentas de detecção de pulverização  
✅ Políticas de senha forte  
✅ Análise de anomalias  

---

### **4. Ataques Offline**

**Definição:**
Envolvem obtenção de informações de autenticação **armazenadas localmente**.

**O que é obtido:**
- Hashes de senhas
- Bancos de dados de credenciais

**Característica principal:**
Permite tentativas de quebra **sem interação** com sistema alvo.

**Como funciona:**
```
Invasor obtém banco de dados de senhas
↓
Usa técnicas offline:
- Força bruta
- Ataque de dicionário
- Rainbow tables
↓
Trabalha localmente, sem ser detectado
```

**Como acontece o ataque:**

**Obtenção do banco de dados:**
- Invasor conseguiu acesso a bancos de dados de hashes
- Violação de segurança
- Exploit de vulnerabilidade

**Processo:**
```
Cracker não interage com sistema de autenticação
↓
Único indicador:
- Log de auditoria do sistema de arquivos
- Registro de conta maliciosa acessando arquivos
↓
Ou presença de ferramentas de ataque no host
```

**Métodos de obtenção:**

**1. Banco de dados de senhas:**
- Acesso direto a arquivos do sistema
- `/etc/shadow` no Linux
- SAM no Windows

**2. Sniffer de pacotes:**
- Captura resposta do cliente a desafio do servidor
- Em protocolos como NTLM, CHAP/MS-CHAP
- Calcula hash a partir da resposta

**Prevenção:**
✅ Armazenar senhas com hash forte  
✅ Usar salt nos hashes  
✅ Proteger bancos de dados contra acesso não autorizado  
✅ Monitorar acesso a arquivos de credenciais  
✅ Usar algoritmos de hash lentos (bcrypt, scrypt)  

---

### **5. Ataque de Força Bruta**

**Definição:**
Tenta **todas as combinações possíveis** no espaço de saída para corresponder a um hash capturado.

**Espaço de saída:**
Determinado pelo número de bits do algoritmo:
- MD5: 128 bits
- SHA256: 256 bits

**Como funciona:**
```
Gerar todas as combinações possíveis:
"a", "b", "c", ... "z"
"aa", "ab", ... "zz"
"aaa", "aab", ... "zzz"
↓
Aplicar hash em cada uma
↓
Comparar com hash capturado
↓
Encontrar correspondência
```

**Fator de dificuldade:**
Quanto maior:
- Espaço de saída
- Número de caracteres na senha

Mais difícil calcular e testar cada hash possível.

**Limitações:**
❌ Fortemente limitado por tempo  
❌ Fortemente limitado por recursos computacionais  

**Eficácia:**
✅ Mais eficaz na quebra de senhas curtas

**Ataques distribuídos:**
Ataques de força bruta distribuídos em:
- Vários componentes de hardware
- Cluster de placas gráficas de última geração
- Podem ter sucesso na quebra de senhas mais longas

**Exemplo de tempo:**

| Senha | Tempo (GPU única) | Tempo (cluster GPUs) |
|-------|-------------------|----------------------|
| 4 caracteres | Segundos | Instantâneo |
| 8 caracteres | Horas-Dias | Minutos-Horas |
| 12 caracteres | Anos | Dias-Semanas |
| 16+ caracteres | Séculos | Anos |

---

### **6. Ataque de Dicionário**

**Diferença da força bruta:**
- **Força bruta:** Tenta todas as combinações possíveis
- **Dicionário:** Usa lista de palavras comuns

**Quando usar:**
Há boa chance de adivinhar valor provável do texto simples.

**Como funciona:**
```
Lista de palavras (dicionário):
- senha
- admin
- 123456
- futebol
- João
- maria123
↓
Software gera hash de cada palavra
↓
Tenta combinar com hash capturado
```

**Fontes de dicionário:**
- Palavras de idiomas
- Nomes próprios
- Senhas vazadas anteriormente
- Termos comuns
- Combinações populares

**Eficácia:**
✅ Rápido contra senhas não complexas  
✅ Muitas senhas são previsíveis  

**Exemplo de senha vulnerável:**
```
"joao123"
"maria2024"
"futebol"
"senha123"
```

**Prevenção:**
✅ Políticas de senhas fortes  
✅ Promover senhas complexas  
✅ Bloqueios automáticos  
✅ Evitar palavras de dicionário  

---

### **7. Ataque Híbrido**

**Definição:**
Usa **combinação** de ataques de dicionário e de força bruta.

**Alvo:**
Principalmente senhas ingênuas com complexidade inadequada.

**Exemplos de senhas vulneráveis:**
```
"james1"
"maria123"
"senha@2024"
"joao!silva"
```

**Como funciona:**

**Algoritmo:**
```
Testa palavras de dicionário
↓
Em combinação com máscara
↓
Limita número de variações
↓
Adição de prefixos/sufixos numéricos
```

**Padrões comuns testados:**
```
Palavra base: "senha"

Variações testadas:
- senha1, senha2, ... senha99
- senha!, senha@, senha#
- Senha1, Senha2
- senha2024, senha2023
- @senha, senha@
```

**Baseado em comportamento de usuários:**
Algoritmos aplicados com base no que hackers sabem sobre como usuários se comportam quando forçados a selecionar senhas complexas.

**Substituições comuns:**
```
"s" → "S" ou "$"
"o" → "0"
"a" → "@"
"i" → "!"
"e" → "3"
```

**Exemplos de transformações:**
```
"senha" → "S3nh@"
"jose" → "j0s3"
"maria" → "M@r!@"
```

**Objetivo:**
Atacantes buscam equilibrar:
- Eficiência de ataque de força bruta
- Previsibilidade de padrões de senha comuns

**Prevenção:**
✅ Senhas únicas e complexas  
✅ Evitar padrões previsíveis  
✅ Bloqueios automáticos  
✅ Monitoramento proativo  
✅ Educação de usuários  

---

## 🔐 Gerenciamento de Autenticação

### **Problema Comum**

**Práticas inadequadas dos usuários:**
- Usar mesma senha para redes corporativas e sites de consumidores
- Senhas fracas
- Anotar senhas em post-its
- Compartilhar senhas

**Risco:**
Torna segurança da rede corporativa **vulnerável a violações** de dados de sites externos.

---

### **Solução: Gerenciadores de Autenticação**

**O que é:**
Dispositivo ou serviço como proxy para armazenamento de credenciais.

**Como funciona:**
```
Gerente gera senha forte e exclusiva
↓
Para cada conta baseada na web
↓
Usuário autoriza gerente a autenticar
↓
Em cada site usando senha mestra
↓
Única senha que usuário precisa lembrar
```

**Benefícios:**
✅ Senha única e forte para cada site  
✅ Usuário lembra apenas senha mestra  
✅ Reduz risco de reutilização de senhas  
✅ Facilita uso de senhas complexas  

---

### **Implementações**

#### **1. Chave de Senha (Password Key)**

**O que é:**
Tokens USB para conexão com PCs e smartphones.

**Tecnologias de comunicação:**
- 🔌 Conectividade física (USB)
- 📡 NFC (Near Field Communication)
- 📶 Bluetooth

**Exemplos:**
- YubiKey
- Google Titan Key
- SoloKeys

**Características:**
✅ Hardware físico  
✅ Proteção adicional contra malware  
✅ Portátil  

---

#### **2. Cofre de Senhas (Password Vault)**

**O que é:**
Gerenciador de senhas baseado em software.

**Implementação típica:**
- Serviço de nuvem
- Permite acesso de qualquer dispositivo
- Sincronização automática

**Chave USB:**
Provavelmente também usa um cofre para backup.

**Exemplos:**

**Nativos do SO:**
- Windows Credential Manager
- iCloud Keychain (Apple)
- GNOME Keyring (Linux)

**Nativos do navegador:**
- Chrome Password Manager
- Firefox Lockwise
- Safari Passwords

**Terceiros:**
- 1Password
- LastPass
- Bitwarden
- Dashlane
- KeePass

**Características:**
✅ Acesso de múltiplos dispositivos  
✅ Sincronização em nuvem  
✅ Geração automática de senhas  
✅ Preenchimento automático  
✅ Auditoria de segurança de senhas  

---

### **Funcionalidades Comuns**

**Geração de senhas:**
```
Configuração:
- Comprimento: 16 caracteres
- Incluir: letras, números, símbolos
- Excluir: caracteres ambíguos

Senha gerada:
"K9#mL2$pQ7@nW5&x"
```

**Organização:**
- Pastas/categorias
- Tags
- Busca
- Favoritos

**Segurança:**
- Criptografia forte (AES-256)
- Autenticação multifator para acesso ao cofre
- Auditoria de senhas fracas/reutilizadas
- Alertas de violações de dados

**Conveniência:**
- Auto-preenchimento
- Captura automática de credenciais
- Compartilhamento seguro (família/equipe)

---

## 💡 Conclusão

### **Principais Takeaways**

✅ **Hashes protegem senhas** em armazenamento e transmissão  
✅ **Múltiplos tipos de autenticação** (local, rede, remota)  
✅ **Windows usa Kerberos** como protocolo preferencial  
✅ **Linux oferece flexibilidade** via PAM e SSH  
✅ **SSO melhora experiência** sem comprometer segurança  
✅ **Ataques de senha são variados** e sofisticados  
✅ **Gerenciadores de senha** são solução eficaz  

---

### **Mensagem Final**

**Autenticação como primeira linha de defesa:**
A autenticação é o portão de entrada para a segurança digital. Adotar práticas robustas é essencial para proteger informações sensíveis e manter a integridade dos sistemas.

**Estratégias multicamadas:**
Ao adotar estratégias como autenticação multifatorial, que adiciona camadas de segurança, e ao implementar políticas de senhas que promovem complexidade e rotação regular, estamos construindo uma defesa resiliente contra ameaças cibernéticas.

**Conscientização é crucial:**
A conscientização dos usuários sobre a importância das práticas seguras de autenticação é uma peça crucial nesse quebra-cabeça.

**Tecnologias avançadas:**
Exploramos tecnologias avançadas, como autenticação biométrica e o uso de protocolos seguros, que oferecem soluções inovadoras para os desafios contemporâneos de segurança.

**Adaptação constante:**
A adaptação constante às últimas tendências e a integração de soluções de gerenciamento de senhas proporciona uma abordagem holística para fortalecer a autenticação.

**Monitoramento e análise:**
A incorporação de monitoramento contínuo, bloqueios automáticos inteligentes e a análise de contexto durante a autenticação contribuem para a detecção precoce de atividades suspeitas.

**Resiliência digital:**
Ao adotar práticas e tecnologias avançadas, mantemos a confidencialidade, integridade e disponibilidade dos sistemas, criando um ambiente digital resiliente diante das ameaças emergentes.

Parabéns por ter finalizado mais esta importante etapa! 🎉

---

## 🎓 Frameworks e Padrões de Referência

### **Autenticação e Identidade**
- **NIST 800-63:** Digital Identity Guidelines
- **FIDO (Fast IDentity Online):** Padrões de autenticação forte
- **OAuth 2.0:** Framework de autorização
- **OpenID Connect:** Camada de identidade sobre OAuth 2.0
- **SAML 2.0:** Security Assertion Markup Language

### **Gerenciamento de Senhas**
- **NIST SP 800-63B:** Authentication and Lifecycle Management
- **OWASP Password Storage Cheat Sheet**
- **CIS Controls:** Password Management

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
