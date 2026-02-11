# 🔍 Módulo 3 – Técnicas de Identificação de Ameaças
## Aula 2 – Scanner de Vulnerabilidades: Ativo vs. Passivo

---

## 📋 Resumo Executivo

Esta aula aborda as **técnicas de reconhecimento** e **testes de penetração** como métodos fundamentais para identificação proativa de vulnerabilidades. Compreender a diferença entre reconhecimento ativo e passivo, além do ciclo de vida completo de um pen test, é essencial para avaliar e fortalecer a postura de segurança de uma organização.

---

## 🎯 Objetivos de Aprendizagem

- ✅ Distinguir técnicas de reconhecimento ativo e reconhecimento passivo
- ✅ Entender a finalidade e importância de testes de penetração
- ✅ Compreender as fases do ciclo de vida de um pen test
- ✅ Conhecer metodologias de ataque estruturadas (kill chain)
- ✅ Aprender sobre ética e legalidade em testes de segurança

---

## 📚 Conceitos Fundamentais

- Reconhecimento ativo e passivo
- Penetration Testing (Pen Test)
- Ciclo de vida do ataque (Kill Chain)
- OSINT (Open Source Intelligence)
- Engenharia social
- Footprinting e fingerprinting
- Frameworks de teste de penetração
- Ética e conformidade em testes de segurança


---

## 🔎 Reconhecimento: Primeira Fase de Qualquer Ataque

### **O Que é Reconhecimento?**

**Definição:**
O reconhecimento é o **primeiro passo** em qualquer avaliação de segurança cibernética. Antes de um atacante ou profissional de segurança explorar uma rede ou sistema, é necessário coletar informações sobre o alvo.

**Objetivo:**
- Mapear a superfície de ataque
- Identificar pontos de entrada potenciais
- Coletar informações sobre tecnologias usadas
- Descobrir possíveis vulnerabilidades
- Entender a arquitetura da infraestrutura
- Identificar pessoas-chave na organização

**Duas abordagens distintas:**
É nesse ponto que surgem o reconhecimento ativo e o reconhecimento passivo.

---

## ⚡ Reconhecimento Ativo

### **Definição**

O reconhecimento ativo envolve a **interação direta com o alvo**. É semelhante a "bater à porta" do alvo para ver como ele responde.

**Características principais:**
- Interage diretamente com sistemas alvo
- Gera tráfego detectável
- Pode ser identificado por sistemas de segurança
- Apresenta **maior risco de detecção**
- Pode envolver acesso físico às instalações
- Uso de ferramentas de varredura

---

### **Técnicas de Reconhecimento Ativo**

### **1. Engenharia Social**

**Definição:**
Obtenção de informações, acesso físico às instalações, ou mesmo acesso a uma conta de usuário através da arte da persuasão.

**Características:**
- Embora a quantidade de interação possa variar
- Pode ser classificado como técnica ativa
- Envolve manipulação humana

**Técnicas comuns:**
- **Phishing:** E-mails fraudulentos para obter credenciais
- **Pretexting:** Criar cenário falso para obter informações
- **Baiting:** Isca física ou digital (USB malicioso)
- **Tailgating:** Seguir alguém para área restrita
- **Vishing:** Phishing por telefone (voice phishing)
- **SMiShing:** Phishing por SMS

**Exemplo prático:**
```
Atacante liga para help desk:
"Olá, sou João da TI. Estou tendo problemas com meu VPN. 
Pode resetar minha senha? Meu usuário é joao.silva"
```

---

### **2. Footprinting (Pegada Digital)**

**Definição:**
Usando ferramentas de software para obter informações sobre um host ou topologia de rede.

**Ferramentas:**
**Nmap (nmap.org)** é a ferramenta mais comum

**Onde pode ser usado:**
- Hosts da web
- Segmentos de rede com ou sem fio (se houver acesso físico)

**Tipos de informação coletada:**
- Topologia de rede
- Hosts ativos
- Sistemas operacionais
- Serviços em execução
- Versões de software

**Limitação:**
Embora a busca passiva seja possível (limitando-a a detecção de pacotes), a maioria das técnicas de varredura requer conexões de rede ativas com o alvo que podem ser identificadas pelo software de detecção.

**Exemplo de comando Nmap:**
```bash
# Varredura básica de rede
nmap 192.168.1.0/24

# Varredura com detecção de versão e OS
nmap -sV -O 192.168.1.100

# Varredura agressiva completa
nmap -sV -O -A --script vuln 192.168.1.100

# -sV: Detecta versões de serviços
# -O: Detecta sistema operacional
# -A: Modo agressivo (completo)
# --script vuln: Roda scripts de detecção de vulnerabilidades
```

---

### **3. Varredura de Portas (Port Scanning)**

**Objetivo:**
Identificar quais portas estão abertas e quais serviços estão em execução.

**Informações obtidas:**
- Portas TCP/UDP abertas
- Serviços rodando nessas portas
- Possíveis vulnerabilidades em serviços
- Regras de firewall

**Tipos de varredura:**

| Tipo | Descrição | Detectabilidade |
|------|-----------|-----------------|
| **TCP Connect Scan** | Completa o three-way handshake | Alta (mais ruidosa) |
| **SYN Scan (Half-open)** | Não completa a conexão | Média (mais silenciosa) |
| **UDP Scan** | Testa portas UDP | Variável |
| **ACK Scan** | Identifica regras de firewall | Baixa |
| **FIN/NULL/XMAS Scan** | Bypass de alguns firewalls | Baixa |

**Exemplo com Nmap:**
```bash
# SYN Scan (stealth)
nmap -sS 192.168.1.100

# TCP Connect Scan
nmap -sT 192.168.1.100

# UDP Scan
nmap -sU 192.168.1.100

# Scan de portas específicas
nmap -p 80,443,22,21 192.168.1.100
```

---

### **4. Solicitações DNS**

**Objetivo:**
Descobrir informações sobre a infraestrutura de rede.

**Técnicas:**

**DNS Enumeration:**
- Listar todos os registros DNS de um domínio
- Identificar subdomínios
- Mapear infraestrutura

**Zone Transfer (AXFR):**
- Tentativa de obter cópia completa da zona DNS
- Geralmente bloqueado, mas quando falha de configuração existe, revela tudo

**Ferramentas:**
- `nslookup`
- `dig`
- `host`
- `dnsrecon`
- `fierce`

**Exemplos de comandos:**
```bash
# Consulta DNS básica
nslookup example.com

# Consulta detalhada com dig
dig example.com ANY

# Tentativa de zone transfer
dig axfr @ns1.example.com example.com

# Enumeração de subdomínios
dnsrecon -d example.com -t std
```

**Informações reveladas:**
- Servidores de e-mail (MX records)
- Servidores DNS (NS records)
- Endereços IP (A/AAAA records)
- Subdomínios
- Servidores de aplicação

---

### **5. Ping Sweeps**

**Objetivo:**
Identificar hosts ativos na rede.

**Como funciona:**
Envia ICMP echo requests para range de IPs e aguarda respostas.

**Exemplo com Nmap:**
```bash
# Ping sweep simples
nmap -sn 192.168.1.0/24

# Ping sweep sem ICMP (útil se ICMP bloqueado)
nmap -sn -PS 192.168.1.0/24
```

**Uso:**
- Mapear alcance de IPs
- Identificar dispositivos ativos
- Descobrir segmentos de rede

---

### **6. Banner Grabbing**

**Objetivo:**
Coletar informações dos banners de serviços em execução.

**O que são banners:**
Mensagens que serviços exibem ao estabelecer conexão, geralmente contendo:
- Tipo de serviço
- Versão do software
- Sistema operacional

**Técnicas:**

**Manual com Telnet/Netcat:**
```bash
# Banner grabbing de servidor web
telnet example.com 80
GET / HTTP/1.0

# Com netcat
nc example.com 80
HEAD / HTTP/1.0

# Banner SSH
nc example.com 22

# Banner FTP
nc example.com 21
```

**Com Nmap:**
```bash
# Captura de banners
nmap -sV --script banner 192.168.1.100
```

**Exemplo de resposta:**
```
Server: Apache/2.4.41 (Ubuntu)
X-Powered-By: PHP/7.4.3
OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
```

**Valor das informações:**
Esses detalhes ajudam a identificar vulnerabilidades conhecidas para aquelas versões específicas de software.

---

### **Resumo: Reconhecimento Ativo**

**Características gerais:**
- ⚠️ **Alto risco de detecção**
- Gera tráfego anômalo na rede
- Pode acionar sistemas IDS/IPS
- Atividades ficam registradas em logs
- Pode violar termos de serviço ou leis
- **Requer autorização** para testes legítimos

**Quando usar:**
- Testes de penetração autorizados
- Avaliações internas de segurança
- Red team exercises
- Quando informações detalhadas são necessárias

---

## 🕵️ Reconhecimento Passivo

### **Definição**

Em contraste, o reconhecimento passivo é mais **discreto** e envolve a coleta de informações **sem interação direta** com o alvo.

**Características principais:**
- Não perturba o alvo
- Não gera tráfego suspeito
- ✅ **Baixo/nenhum risco de detecção**
- Usa fontes públicas de informação
- Legal e discreto

**O que inclui:**
- Monitoramento de tráfego de rede
- Análise de logs
- Pesquisa de informações publicamente disponíveis (OSINT)
- Outras técnicas que não perturbam o alvo

---

### **Técnicas de Reconhecimento Passivo**

### **1. OSINT (Open Source Intelligence)**

**Definição:**
Inteligência de código aberto - usando ferramentas de pesquisa na web, mídias sociais e sites que verificam vulnerabilidades em dispositivos e serviços conectados à internet.

**Características:**
- Quase não requer acesso privilegiado
- Depende da localização de informações que a empresa disponibiliza publicamente
- Intencionalmente ou não
- Altamente eficaz e legal

---

#### **Fontes de OSINT**

**Motores de Busca:**
- Google, Bing, DuckDuckGo
- **Google Dorking:** Uso de operadores avançados de busca

**Exemplos de Google Dorks:**
```
site:example.com filetype:pdf
site:example.com inurl:admin
site:example.com intitle:"index of"
site:example.com ext:sql | ext:txt
```

**Redes Sociais:**
- LinkedIn (estrutura organizacional, tecnologias usadas)
- Facebook, Twitter (informações pessoais de funcionários)
- GitHub (código fonte, credenciais expostas)

**Registros Públicos:**
- **WHOIS:** Informações de registro de domínios
- **DNS público:** Registros DNS
- Certificados SSL/TLS

**Vazamento de Dados:**
- **Pastebin:** Credenciais e dados vazados
- **Have I Been Pwned:** Verificar e-mails comprometidos
- Fóruns underground
- Dark web marketplaces

**Buscadores Especializados:**
- **Shodan:** "Mecanismo de busca para a Internet das Coisas"
  - Dispositivos IoT expostos
  - Câmeras, roteadores, SCADA
  - Servidores mal configurados
  
- **Censys:** Similar ao Shodan
  - Certificados SSL
  - Hosts e serviços

**Repositórios de Código:**
- **GitHub/GitLab:** 
  - Código fonte público
  - Credenciais hardcoded
  - API keys expostas
  - Configurações

---

#### **Ferramentas de OSINT**

| Ferramenta | Descrição | Uso |
|------------|-----------|-----|
| **theHarvester** | Agregador de informações públicas | E-mails, subdomínios, IPs |
| **Maltego** | Plataforma de inteligência e análise | Mapeamento de relacionamentos |
| **Recon-ng** | Framework de reconhecimento | Automação de OSINT |
| **SpiderFoot** | Automação de OSINT | Coleta abrangente automatizada |
| **Amass** | Enumeração de subdomínios | Descoberta de ativos |
| **Shodan CLI** | Interface de linha de comando para Shodan | Busca de dispositivos |

**Exemplo com theHarvester:**
```bash
# Coletar e-mails e subdomínios
theHarvester -d example.com -b google,bing,linkedin

# -d: domínio alvo
# -b: fontes de busca
```

---

#### **Tipos de Informações Coletadas via OSINT**

**Informações Organizacionais:**
- Estrutura da empresa
- Funcionários e cargos
- Parceiros e fornecedores
- Localizações físicas

**Informações Técnicas:**
- Endereços IP públicos
- Domínios e subdomínios
- Endereços de e-mail
- Tecnologias utilizadas (CMS, frameworks)
- Versões de software
- Serviços expostos

**Informações Pessoais:**
- Nomes de funcionários
- Cargos e responsabilidades
- Contatos (telefone, e-mail)
- Redes sociais pessoais
- Hobbies e interesses (engenharia social)

**Credenciais Vazadas:**
- Senhas em breaches anteriores
- API keys expostas
- Tokens de acesso
- Chaves SSH/certificados

---

### **2. Monitoramento de Tráfego de Rede**

**Técnica:**
Sniffing passivo de pacotes de rede sem injetar tráfego próprio.

**O que pode ser identificado:**
- Identificação de protocolos em uso
- Análise de padrões de comunicação
- Sistemas operacionais (através de análise de TTL, flags TCP)
- Serviços em uso

**Ferramentas:**
- **Wireshark:** Captura e análise de pacotes
- **tcpdump:** Captura de pacotes via linha de comando
- **p0f:** Fingerprinting passivo de OS

**Exemplo com tcpdump:**
```bash
# Capturar tráfego em interface
tcpdump -i eth0 -w capture.pcap

# Capturar apenas tráfego HTTP
tcpdump -i eth0 port 80
```

**Característica-chave:**
✅ Não injeta pacotes na rede, apenas observa tráfego existente.

---

### **3. Análise de Logs Públicos**

**Fontes:**
- Servidores web com directory listing habilitado
- Arquivos de log expostos inadvertidamente
- Logs de erro acessíveis publicamente
- Arquivos de configuração deixados acessíveis

**Exemplo:**
```
https://example.com/.git/
https://example.com/backup/
https://example.com/phpinfo.php
https://example.com/server-status
```

**Informações reveladas:**
- Estrutura de diretórios
- Tecnologias utilizadas
- Possíveis vulnerabilidades
- Credenciais (em casos extremos)

---

### **Resumo: Reconhecimento Passivo**

**Características gerais:**
- ✅ **Baixo/nenhum risco de detecção**
- Não gera tráfego suspeito
- Legal e discreto (quando usando fontes públicas)
- Não requer autorização específica
- Pode ser feito anonimamente

**Limitações:**
- Pode não fornecer informações tão detalhadas
- Informações podem estar desatualizadas
- Depende de informações disponibilizadas publicamente

**Quando usar:**
- Fase inicial de avaliação
- Quando autorização ainda não foi obtida
- Inteligência de ameaças
- Monitoramento de exposição da própria organização

---

## ⚔️ Comparação: Reconhecimento Ativo vs. Passivo

| Aspecto | Ativo | Passivo |
|---------|-------|---------|
| **Interação** | Direta com o alvo | Sem contato direto |
| **Detectabilidade** | Alta | Baixa/Nula |
| **Informações** | Detalhadas e atuais | Gerais e públicas |
| **Velocidade** | Rápida | Mais lenta |
| **Legalidade** | Requer autorização | Geralmente legal |
| **Ferramentas** | Nmap, Metasploit, Burp | OSINT, theHarvester, Wireshark (passivo) |
| **Risco** | Pode causar indisponibilidade | Seguro |
| **Logs** | Deixa rastros | Não deixa rastros |
| **Custo** | Pode consumir recursos | Baixo custo |

---

## 🎯 Teste de Penetração (Pen Test)

### **Definição**

Um teste de penetração, também conhecido como **pen test**, é uma **simulação controlada de um ataque cibernético** realizado em um sistema, rede ou aplicação para avaliar sua segurança.

**Objetivo:**
Identificar vulnerabilidades **antes** que atacantes maliciosos o façam, permitindo que organizações fortaleçam suas defesas e protejam informações confidenciais.

---

### **Importância dos Testes de Penetração**

**Por que são essenciais:**

✅ **Identifica vulnerabilidades reais:**
- Vai além de varreduras automatizadas
- Valida se vulnerabilidades são exploráveis

✅ **Avalia eficácia dos controles:**
- Testa se medidas de segurança funcionam na prática
- Identifica gaps em defesas

✅ **Mede capacidade de resposta:**
- Avalia detecção de ataques
- Testa resposta a incidentes
- Verifica tempos de reação

✅ **Atende compliance:**
- PCI-DSS exige pen tests regulares
- ISO 27001 recomenda testes
- LGPD incentiva avaliações de segurança

✅ **Reduz superfície de ataque:**
- Correção proativa de vulnerabilidades
- Fortalecimento de controles

✅ **Conscientização:**
- Demonstra riscos reais para stakeholders
- Justifica investimentos em segurança

---

### **Ética e Conformidade em Testes de Penetração**

**⚠️ Aspectos Legais e Éticos são FUNDAMENTAIS**

A ética e a conformidade são fundamentais em testes de penetração. Isso inclui:

### **1. Autorização Formal Obrigatória**

**Documentos necessários:**
- Contrato de pen test assinado por ambas as partes
- Escopo bem definido e documentado
- Regras de engajamento (Rules of Engagement - RoE) claras
- Statement of Work (SOW)

**O que deve estar no contrato:**
- Sistemas/redes a serem testados
- Sistemas/redes FORA do escopo
- Técnicas permitidas e proibidas
- Horários de teste
- Contatos de emergência

---

### **2. Respeito às Leis e Regulamentações**

**Legislação Brasileira:**
- **Lei 12.737/2012 (Lei Carolina Dieckmann):** Lei de Crimes Cibernéticos
- **LGPD (Lei 13.709/2018):** Lei Geral de Proteção de Dados

**Legislação Internacional:**
- Computer Fraud and Abuse Act (CFAA) - EUA
- Computer Misuse Act - Reino Unido
- GDPR - União Europeia

**⚠️ IMPORTANTE:**
Pen test **sem autorização** é **CRIME** e pode resultar em:
- Processos criminais
- Multas pesadas
- Prisão
- Responsabilidade civil

---

### **3. Notificação das Partes Interessadas**

**Quem deve ser informado:**
- Stakeholders executivos
- Equipes de TI e segurança
- Equipe de SOC (Security Operations Center)
- Administradores de sistemas

**Por quê:**
- Coordenação de atividades
- Evitar alarmes falsos
- Garantir suporte em caso de problemas
- Comunicação de incidentes

---

### **4. Documentação Completa**

**O que documentar:**
- Todas as atividades realizadas
- Comandos executados
- Vulnerabilidades encontradas
- Evidências (screenshots, logs)
- Timestamps de todas as ações

**Chain of Custody:**
- Manter integridade das evidências
- Rastreabilidade completa
- Importante para aspectos legais

---

### **5. Confidencialidade**

**Medidas necessárias:**
- **NDA (Non-Disclosure Agreement):** Acordo de confidencialidade
- Proteção de dados sensíveis descobertos
- Armazenamento seguro de relatórios
- Compartilhamento restrito de informações

**Dados sensíveis podem incluir:**
- Credenciais
- Informações pessoais (PII)
- Propriedade intelectual
- Dados financeiros

---

### **Princípios Éticos**

1. **Não causar danos:** Objetivo é melhorar segurança, não prejudicar
2. **Transparência:** Comunicar descobertas honestamente
3. **Profissionalismo:** Manter confidencialidade e integridade
4. **Responsabilidade:** Assumir responsabilidade por ações
5. **Respeito:** Respeitar privacidade e propriedade

---

## 📊 Objetivos de um Pen Test

### **Objetivos Principais**

1. **Identificar Vulnerabilidades**
   - Fraquezas em sistemas, redes e aplicações
   - Falhas de configuração
   - Vulnerabilidades de software

2. **Avaliar Eficácia das Medidas de Segurança**
   - Controles preventivos funcionam?
   - Controles detectivos alertam adequadamente?
   - Controles corretivos são efetivos?

3. **Medir Capacidade de Detecção e Resposta**
   - Quão rápido a equipe detecta ataques?
   - Quão eficaz é a resposta a incidentes?
   - SOC identifica atividades maliciosas?

4. **Testar Controles de Segurança**
   - Firewalls, IDS/IPS
   - EDR, antivírus
   - WAF, DLP
   - Autenticação e controle de acesso

5. **Fornecer Recomendações Práticas**
   - Correções priorizadas
   - Melhorias de processo
   - Estratégias de hardening

6. **Validar Investimentos**
   - ROI de ferramentas de segurança
   - Efetividade de treinamentos
   - Justificar novos investimentos

---

## 🔄 Fases de um Pen Test

### **Visão Geral do Processo**

```
┌─────────────────┐
│  1. Planejamento │
└────────┬─────────┘
         ↓
┌─────────────────┐
│ 2. Coleta Info  │
└────────┬─────────┘
         ↓
┌─────────────────┐
│  3. Análise     │
└────────┬─────────┘
         ↓
┌─────────────────┐
│  4. Exploração  │
└────────┬─────────┘
         ↓
┌─────────────────┐
│ 5. Pós-Exploit  │
└────────┬─────────┘
         ↓
┌─────────────────┐
│6. Documentação  │
└────────┬─────────┘
         ↓
┌─────────────────┐
│ 7. Remediação   │
└─────────────────┘
```

---

### **1. Planejamento (Planning)**

**Objetivo:**
Definir claramente escopo, objetivos e regras do teste.

**Atividades:**
- Definição de objetivos claros e mensuráveis
- Determinação do escopo preciso
  - Sistemas incluídos
  - Sistemas EXCLUÍDOS (crítico!)
- Escolha da metodologia (OSSTMM, OWASP, PTES)
- Aprovação da alta administração
- Definição de regras de engajamento (RoE)
- Cronograma detalhado
- Alocação de recursos

**Documentos Produzidos:**
- Contrato de pen test
- Statement of Work (SOW)
- Regras de engajamento
- Plano de comunicação
- Plano de contingência

**Questões a responder:**
- Qual tipo de teste? (Black box, White box, Gray box)
- Quando executar? (horário comercial, fora do horário)
- Quem será notificado?
- Quais limites não devem ser ultrapassados?

---

### **2. Coleta de Informações (Reconnaissance)**

**Objetivo:**
Reunir o máximo de informações sobre o alvo.

**Atividades:**
- **OSINT:** Informações públicas
  - Google Dorking
  - Redes sociais
  - WHOIS, DNS
  - Shodan, Censys
- Varredura de DNS
- Identificação de alvos (IPs, domínios, subdomínios)
- Mapeamento de tecnologias
- Footprinting e fingerprinting
- Identificação de funcionários

**Ferramentas:**
- theHarvester, Maltego, Recon-ng
- WHOIS, nslookup, dig
- Shodan, Censys
- Google Dorking
- LinkedIn, redes sociais

**Resultado:**
Documento com todas as informações coletadas sobre o alvo.

---

### **3. Análise (Scanning & Enumeration)**

**Objetivo:**
Identificar vulnerabilidades e pontos de entrada.

**Atividades:**
- **Varredura de portas e serviços**
  - Quais portas estão abertas?
  - Que serviços estão rodando?
  
- **Identificação de versões**
  - Versões de software
  - Sistemas operacionais
  
- **Detecção de vulnerabilidades**
  - CVEs aplicáveis
  - Configurações inseguras
  
- **Enumeração**
  - Usuários
  - Grupos
  - Compartilhamentos (shares)
  - Serviços
  
- **Análise de aplicações web**
  - Tecnologias utilizadas
  - Pontos de entrada
  - Formulários, APIs

**Ferramentas:**
- **Scanners de rede:** Nmap, Masscan
- **Scanners de vulnerabilidade:** Nessus, OpenVAS
- **Web scanners:** Nikto, Burp Suite
- **Enumeração:** Enum4linux, SMBMap, ldapsearch
- **Web app analysis:** Wappalyzer, WhatWeb

**Resultado:**
Lista priorizada de vulnerabilidades potenciais.

---

### **4. Exploração (Exploitation)**

**Objetivo:**
Tentar explorar vulnerabilidades identificadas para ganhar acesso.

**Atividades:**
- Tentativas de exploração de vulnerabilidades
  - Usar exploits conhecidos
  - Desenvolver exploits customizados
  
- Ganho de acesso inicial (initial foothold)
  - Shell reverso
  - Webshell
  - Acesso via credenciais
  
- Estabelecimento de backdoors
  - Garantir persistência
  
- Teste de controles de segurança
  - Bypasses de firewall
  - Evasão de IDS/IPS
  - Evasão de EDR/Antivírus

**Ferramentas:**
- **Metasploit Framework:** Exploração automatizada
- **SQLmap:** SQL Injection
- **Hydra, Medusa:** Força bruta
- **Burp Suite:** Web exploitation
- **Custom exploits:** Scripts Python, Ruby

**Nota Crítica:**
Esta fase requer **máxima cautela** para não causar danos ou indisponibilidade.

**Exemplo de controle:**
- Fazer backup antes de explorar
- Ter plano de rollback
- Testar em ambiente de staging primeiro (se possível)
- Coordenar com equipe técnica

---

### **5. Pós-Exploração (Post-Exploitation)**

**Objetivo:**
Demonstrar impacto real da vulnerabilidade explorada.

**Atividades:**

**Manutenção de Acesso (Persistência):**
- Instalação de backdoors
- Criação de contas ocultas
- Modificação de tarefas agendadas
- Rootkits (em ambientes de teste)

**Escalação de Privilégios:**
- De usuário comum para administrador
- De admin local para domain admin
- Técnicas: kernel exploits, configurações incorretas

**Movimento Lateral:**
- Explorar rede interna
- Comprometer outros sistemas
- Passar de DMZ para rede interna

**Coleta de Dados (Demonstrativa):**
- Identificar dados sensíveis
- **NÃO exfiltrar dados reais** (apenas demonstrar capacidade)
- Screenshots como evidência

**Pivoting:**
- Usar host comprometido como ponte
- Acessar redes isoladas

**Objetivos Demonstrados:**
- Quais dados **poderiam** ser exfiltrados
- Que sistemas **poderiam** ser comprometidos
- Impacto real de um ataque no negócio

**⚠️ Importante:**
- Coordenar com cliente antes de movimentos laterais
- Não acessar dados reais sensíveis sem autorização específica
- Documentar todas as ações

---

### **6. Documentação e Relatório (Reporting)**

**Objetivo:**
Documentar completamente descobertas e fornecer guia de remediação.

**Conteúdo do Relatório:**

#### **Executive Summary**
- Resumo para gestão (não-técnico)
- Principais descobertas (high-level)
- Nível de risco global
- Recomendações estratégicas

#### **Metodologia**
- Como o teste foi conduzido
- Ferramentas utilizadas
- Limitações do teste
- Período de execução

#### **Escopo**
- Sistemas testados
- Sistemas fora do escopo
- Regras de engajamento

#### **Descobertas Detalhadas**

Para cada vulnerabilidade:

| Campo | Conteúdo |
|-------|----------|
| **Nome/Título** | Identificação clara |
| **Severidade** | Crítica/Alta/Média/Baixa (CVSS) |
| **Descrição** | O que é a vulnerabilidade |
| **Impacto** | Consequências para o negócio |
| **Evidências** | Screenshots, comandos, outputs |
| **Passos de Reprodução** | Como explorar |
| **Remediação** | Correções específicas |
| **Referências** | CVEs, CWEs, links |

#### **Análise de Risco e Impacto**
- Matriz de risco (Probabilidade vs. Impacto)
- Cenários de ataque
- Impacto financeiro potencial

#### **Recomendações Priorizadas**
1. **Quick wins:** Correções rápidas (< 1 semana)
2. **Médio prazo:** Remediações complexas (1-3 meses)
3. **Longo prazo:** Melhorias estratégicas (> 3 meses)

#### **Conformidade (se aplicável)**
- PCI-DSS findings
- ISO 27001 gaps
- LGPD considerations

#### **Apêndices**
- Comandos completos utilizados
- Logs técnicos detalhados
- Glossário de termos
- Referências externas

---

### **7. Remediação e Reteste**

**Objetivo:**
Validar que correções foram implementadas corretamente.

**Processo:**

1. **Cliente implementa correções**
   - Baseado em recomendações do relatório
   - Priorização por criticidade

2. **Pen tester valida remediações**
   - Reteste das vulnerabilidades corrigidas
   - Verifica se correção foi efetiva
   - Identifica se surgiram novos problemas

3. **Relatório final de validação**
   - Status de cada vulnerabilidade
   - Confirmação de correções
   - Vulnerabilidades residuais (se houver)

**Ciclo contínuo:**
Pen tests devem ser realizados periodicamente (anuais, semestrais) para manter segurança.

---

## 🔗 Ferramentas Comuns de Pen Test

| Ferramenta | Categoria | Uso Principal |
|------------|-----------|---------------|
| **Nmap** | Scanner de rede | Port scanning, OS detection, service enumeration |
| **Metasploit** | Framework de exploração | Automatiza ataques e exploração |
| **Burp Suite** | Web app testing | Proxy, scanner, intruder para web apps |
| **Wireshark** | Análise de tráfego | Captura e análise de pacotes |
| **John the Ripper** | Cracking de senhas | Força bruta, rainbow tables |
| **Hashcat** | Cracking de senhas | GPU-accelerated password cracking |
| **Aircrack-ng** | Wireless testing | Auditoria de redes Wi-Fi |
| **SQLmap** | SQL Injection | Exploração automatizada de SQL injection |
| **Nikto** | Web scanner | Varredura de servidores web |
| **Hydra** | Força bruta | Ataques de força bruta em serviços |
| **Gobuster** | Web enumeration | Brute force de diretórios e arquivos |
| **Mimikatz** | Credential dumping | Extração de credenciais do Windows |
| **BloodHound** | AD enumeration | Mapeamento de Active Directory |
| **Cobalt Strike** | C2 Framework | Command & Control para Red Team |

---

## 💀 Kill Chain: Ciclo de Vida do Ataque

### **O Que É Kill Chain?**

**Conceito:**
Termo comumente utilizado em segurança cibernética para descrever as **etapas sequenciais** que um atacante segue durante um ataque cibernético, desde o planejamento inicial até a execução e exploração bem-sucedida.

**Origem:**
Adaptado do conceito militar de "cadeia de morte" para cybersecurity.

**Por que é importante:**
Essas etapas são projetadas para representar o ciclo de vida típico de um ataque e podem ser usadas para entender, analisar e **defender-se** contra ameaças cibernéticas.

**Princípio de Defesa:**
Se uma organização for capaz de **identificar e interromper uma etapa** da cadeia, poderá impedir um ataque cibernético antes que ele tenha sucesso.

---

### **Etapas da Cyber Kill Chain**

```
┌─────────────────┐
│ 1. Reconhecimento│ ← Coleta de informações
└────────┬────────┘
         ↓
┌─────────────────┐
│  2. Exploração  │ ← Acesso inicial
└────────┬────────┘
         ↓
┌─────────────────┐
│ 3. Persistência │ ← Manter acesso
└────────┬────────┘
         ↓
┌─────────────────┐
│ 4. Escalonamento│ ← Privilégios elevados
└────────┬────────┘
         ↓
┌─────────────────┐
│5. Mov. Lateral  │ ← Expandir acesso
└────────┬────────┘
         ↓
┌─────────────────┐
│ 6. Ações/Objeti.│ ← Exfiltração, impacto
└────────┬────────┘
         ↓
┌─────────────────┐
│  7. Limpeza     │ ← Remover rastros
└─────────────────┘
```

---

### **1. Reconhecimento (Reconnaissance)**

**Objetivo:**
Coletar informações sobre o alvo.

**Atividades:**
- OSINT (Open Source Intelligence)
- Footprinting
- Identificação de vulnerabilidades
- Mapeamento de funcionários e parceiros
- Análise de infraestrutura
- Perfis em redes sociais

**Dados Coletados:**
- Tecnologias em uso (CMS, frameworks)
- Estrutura organizacional
- Endereços de e-mail de funcionários
- Sistemas expostos na internet
- Subdomínios e domínios relacionados

**Perspectiva de Pen Tester:**
Esta fase é onde se reúnem informações para planejar os próximos passos do teste.

**Defesa:**
- Minimizar informações públicas
- Monitorar vazamentos de dados (Have I Been Pwned)
- Conscientização sobre compartilhamento em redes sociais
- Web Application Firewalls (WAF)
- Honeytokens para detectar reconhecimento

---

### **2. Exploração (Weaponization/Delivery)**

**Objetivo:**
Obter acesso inicial ao ambiente alvo.

**Técnicas:**

**E-mail de Phishing:**
- Payload malicioso em anexo
- Links para sites comprometidos
- Credenciais falsas

**Exploração de Vulnerabilidades:**
- Serviços expostos sem patch
- Zero-days
- Configurações incorretas

**Credenciais:**
- Obtidas via engenharia social
- Senhas padrão
- Credenciais vazadas

**Outros Métodos:**
- Drive-by downloads (exploração ao visitar site)
- Watering hole attacks (comprometer site visitado por alvos)
- USB drops (deixar USBs maliciosos)

**Ferramentas:**
- Frameworks de exploração (Metasploit)
- Malware customizado
- Kits de exploração (Exploit Kits)

**Perspectiva de Pen Tester:**
Usar ferramenta de software para obter algum tipo de acesso à rede do alvo. Isso pode ser feito usando:
- E-mail e payload de phishing
- Credenciais obtidas por engenharia social

**Defesa:**
- Email security (anti-spam, sandboxing)
- Patch management rigoroso
- Filtros web (URL filtering)
- EDR/Antivírus avançado
- User awareness training

---

### **3. Persistência (Persistence)**

**Objetivo:**
Manter acesso ao sistema comprometido mesmo após reinicializações ou logoffs.

**Por quê?**
Atacantes (ou pen testers) precisam garantir que possam se reconectar ao host comprometido.

**Técnicas:**

**Backdoors:**
- Instalação de trojans
- Shells reversos persistentes
- Web shells em servidores

**Contas Ocultas:**
- Criação de usuários não autorizados
- Modificação de contas existentes

**Modificações do Sistema:**
- Tarefas agendadas (cron jobs, Windows Task Scheduler)
- Chaves de registro (Windows)
- Scripts de inicialização
- Serviços do sistema

**Rootkits:**
- Ocultação de processos e arquivos
- Nível de kernel

**RAT (Remote Access Tool):**
Estabelecer ferramenta de acesso remoto ou backdoor.

**Comando e Controle (C2/C&C):**
O pen tester deve estabelecer uma rede de comando e controle usando para:
- Controlar o host comprometido
- Carregar ferramentas de ataque adicionais
- Baixar dados exfiltrados

**Requisitos para C2:**
A conexão com o host comprometido normalmente exigirá:
- Executável de malware rodando após eventos de desligamento/logoff
- Conexão com uma porta de rede
- Endereço IP do invasor disponível

**Defesa:**
- EDR com análise comportamental
- Monitoramento de processos e conexões
- Baseline de configurações
- Application whitelisting
- Integrity monitoring
- Análise de eventos de logon

---

### **4. Escalonamento de Privilégios (Privilege Escalation)**

**Objetivo:**
Obter privilégios mais elevados (admin, root, SYSTEM).

**Por Quê?**
- Acesso inicial geralmente é limitado (usuário comum)
- Necessário para acessar dados sensíveis
- Movimentação lateral requer privilégios
- Instalar ferramentas requer privilégios

**Contexto:**
A persistência é seguida por reconhecimento adicional onde o pen tester tenta:
- Mapear a rede interna
- Descobrir serviços em execução
- Identificar contas configuradas

Mover-se dentro da rede ou acessar ativos de dados provavelmente exigirá níveis de privilégio mais elevados.

**Exemplo de Escalação:**
```
Acesso inicial: 
  Usuário "joao.silva" em workstation
  ↓
Exploração: 
  Vulnerabilidade no serviço local (CVE-XXXX-XXXX)
  ↓
Resultado: 
  Privilégios de SYSTEM (Windows) ou root (Linux)
```

**Técnicas:**

**Exploração de Vulnerabilidades Locais:**
- Kernel exploits
- Vulnerabilidades em drivers
- Software vulnerável com privilégios

**Configurações Incorretas:**
- Permissões fracas em arquivos/pastas
- Serviços mal configurados
- Sudoers misconfiguration (Linux)
- UAC bypass (Windows)

**Roubo de Credenciais:**
- Pass-the-Hash (PtH)
- Pass-the-Ticket (PtT) - Kerberos
- Mimikatz (Windows credential dumping)
- Token impersonation

**Abuso de Funcionalidades:**
- Scheduled tasks executando como SYSTEM
- SUID binaries (Linux)
- DLL hijacking

**Defesa:**
- Patch management religioso
- Princípio do menor privilégio
- PAM (Privileged Access Management)
- Hardening de sistemas
- Application whitelisting
- Credential Guard (Windows)
- Audit logging

---

### **5. Movimento Lateral / Pivotagem (Lateral Movement)**

**Objetivo:**
Expandir acesso para outros sistemas na rede interna.

**Por Quê?**
- Descobrir mais oportunidades de acesso
- Localizar ativos de dados valiosos
- Evitar detecção (dispersão)
- Alcançar objetivos finais (servidores, databases)

**Técnicas:**

**Pass-the-Hash (PtH):**
- Usar hash de senha sem precisar crackeá-la
- Autenticação NTLM

**Pass-the-Ticket (PtT):**
- Roubo de tickets Kerberos
- Kerberoasting

**RDP (Remote Desktop Protocol):**
- Acesso visual remoto a sistemas Windows

**PSExec / PsTools:**
- Execução remota de comandos Windows
- Parte do Sysinternals Suite

**PowerShell Remoting:**
- WinRM (Windows Remote Management)
- Execução de scripts remotamente

**WMI (Windows Management Instrumentation):**
- Gerenciamento remoto Windows
- Execução de comandos

**SSH Lateral:**
- Movimento em ambientes Linux/Unix
- Chaves SSH comprometidas

**Pivotagem:**
Usar host comprometido como "ponte":
- Bypass de segmentação de rede
- Acesso a redes isoladas
- Exemplo: DMZ → Rede interna → Servidor de banco de dados

**Exemplo de Pivotagem:**
```
Internet → Servidor Web (DMZ) → Firewall → Rede Interna → Servidor de Aplicação → Database Server
```

**Ferramentas:**
- **Mimikatz:** Credential dumping
- **BloodHound:** Mapeamento de caminhos de ataque em AD
- **CrackMapExec:** Automação de movimento lateral
- **Cobalt Strike:** Framework de C2 avançado
- **Impacket:** Biblioteca Python para protocolos de rede

**Defesa:**
- **Segmentação de rede:** VLANs, micro-segmentação
- **Zero Trust Architecture:** Nunca confie, sempre verifique
- **MFA mesmo internamente:** Não apenas no perímetro
- **Monitoramento de movimento lateral:** NDR (Network Detection and Response)
- **Least privilege:** Minimizar permissões
- **Credential vaulting:** PAM solutions
- **Anomaly detection:** UEBA (User and Entity Behavior Analytics)

---

### **6. Ações Baseadas em Objetivos (Actions on Objectives)**

**Objetivo:**
Executar as ações finais planejadas.

**Para Atacantes:**

**Exfiltração de Dados:**
- Roubo de informações confidenciais
- Propriedade intelectual
- Dados pessoais (PII)
- Credenciais
- Dados financeiros

**Ransomware:**
- Criptografar dados para extorsão
- Double extortion (criptografar + ameaça de vazamento)

**Sabotagem:**
- Destruição ou corrupção de sistemas
- Deletar dados críticos
- Modificar configurações

**Espionagem:**
- Monitoramento contínuo
- Instalação de keyloggers
- Captura de tela

**Cryptojacking:**
- Mineração de criptomoedas usando recursos da vítima

**Fraude Financeira:**
- Transações não autorizadas
- Modificação de dados bancários

**Para Pen Testers:**

**Demonstração de Impacto:**
- Provar que objetivos **poderiam** ser alcançados
- **NÃO executar ações destrutivas reais**

**Documentação:**
- Registrar evidências
- Screenshots de acesso a dados sensíveis
- Demonstração de capacidades

**Exemplos de Demonstração:**
- Screenshot de acesso a arquivos confidenciais
- Hash de senha de administrador (sem usar)
- Evidência de acesso a sistemas críticos
- **Simulação** de exfiltração (sem exfiltrar dados reais)
- Demonstração de que ransomware poderia ser implantado

**⚠️ Crítico para Pen Testers:**
- Não acessar dados reais sensíveis sem autorização específica
- Não exfiltrar dados
- Não deletar ou modificar dados
- Apenas demonstrar capacidade

**Defesa:**
- **DLP (Data Loss Prevention):** Prevenir exfiltração
- **Backup e recovery robustos:** Proteção contra ransomware
- **Monitoramento de transferências:** Alertas em transferências anormais
- **Alertas de comportamento anômalo:** UEBA
- **Network segmentation:** Limitar movimentação
- **Honeypots:** Detectar acesso a recursos falsos

---

### **7. Fase de Limpeza (Cleanup)**

**Para Atacantes:**
- Remover evidências do ataque
- Apagar logs
- Remover backdoors (se necessário)
- Ofuscar rastros para dificultar atribuição

**Para Pen Testers:**

**Obrigatório:**
- Remover **todos** os backdoors e ferramentas
- Garantir que o sistema não está menos seguro
- Retornar ao estado pré-engajamento

**Atividades:**
- Remoção de contas criadas
- Desativação de persistência instalada
- Limpeza de ferramentas instaladas
- Restauração de configurações modificadas
- Remoção de arquivos temporários
- Verificação de que nada foi deixado para trás

**Documentação:**
- Listar todas as mudanças feitas
- Confirmar que todas foram revertidas
- Obter confirmação do cliente

**⚠️ Crítico para Pen Testers:**
Não deixar "portas abertas" após o teste que possam ser exploradas por atacantes reais.

**Verificação:**
- Re-scan para confirmar remoção
- Teste de conectividade
- Validação com equipe cliente

---

## 🛡️ Defesa por Camada da Kill Chain

| Etapa | Controles Defensivos |
|-------|----------------------|
| **Reconhecimento** | Minimizar pegada digital, OSINT defensivo, monitoring de menções |
| **Exploração** | Patch management, email security, web filtering, EDR |
| **Persistência** | Baseline monitoring, EDR, application whitelisting, file integrity |
| **Escalonamento** | PAM, least privilege, hardening, patch management |
| **Lateral Movement** | Segmentação, Zero Trust, NDR, MFA interno, PAM |
| **Objetivos** | DLP, backup, monitoramento, incident response, UEBA |
| **Limpeza** | SIEM, log retention, forensics, immutable logs |

---

## 💡 Conclusão

### **Principais Takeaways**

✅ **Reconhecimento passivo é discreto; ativo é mais detectável**
- Escolha a abordagem adequada ao contexto

✅ **OSINT é legal e poderosa fonte de informações**
- Sempre comece por reconhecimento passivo

✅ **Pen tests devem ser SEMPRE autorizados e éticos**
- Sem autorização = crime

✅ **Kill chain permite entender e interromper ataques**
- Defender em múltiplas etapas aumenta chance de sucesso

✅ **Documentação detalhada é essencial**
- Para remediação eficaz e compliance

✅ **Defesa em profundidade combate ameaças em cada fase**
- Nenhum controle único é suficiente

✅ **Testes periódicos são necessários**
- Segurança é processo contínuo, não evento único

---

## 🎓 Frameworks e Metodologias de Referência

### **Frameworks de Pen Test**

- **PTES (Penetration Testing Execution Standard):** Framework completo de pen test
- **OWASP Testing Guide:** Metodologia para testes de aplicações web
- **OSSTMM (Open Source Security Testing Methodology Manual)**
- **NIST SP 800-115:** Technical Guide to Information Security Testing

### **Frameworks de Ataque**

- **MITRE ATT&CK:** Framework de táticas e técnicas de adversários
- **Cyber Kill Chain (Lockheed Martin):** Modelo de fases de ataque
- **Diamond Model:** Modelo de análise de intrusão

### **Certificações Relevantes**

- **CEH (Certified Ethical Hacker)**
- **OSCP (Offensive Security Certified Professional)**
- **GPEN (GIAC Penetration Tester)**
- **PNPT (Practical Network Penetration Tester)**

---

## 🔗 Conceitos Relacionados

- **Threat Modeling:** Modelagem de ameaças
- **Red Team vs Blue Team:** Exercícios de ataque e defesa
- **Purple Team:** Colaboração entre red e blue teams
- **Bug Bounty Programs:** Programas de recompensa por vulnerabilidades
- **Vulnerability Disclosure:** Divulgação responsável de vulnerabilidades
- **Exploit Development:** Criação de exploits customizados
- **Social Engineering:** Engenharia social avançada
- **Phishing Campaigns:** Campanhas de conscientização via phishing simulado

---

## 📚 Glossário de Termos

| Termo | Definição |
|-------|-----------|
| **Footprinting** | Processo de coletar informações sobre sistemas alvo |
| **Fingerprinting** | Identificação de sistema operacional e serviços |
| **OSINT** | Open Source Intelligence - inteligência de fontes abertas |
| **Exploit** | Código ou técnica que explora uma vulnerabilidade |
| **Payload** | Código malicioso entregue por exploit |
| **Backdoor** | Acesso oculto a sistema comprometido |
| **C2/C&C** | Command and Control - servidor de controle |
| **Pivoting** | Usar sistema comprometido como ponte para outros |
| **PtH** | Pass-the-Hash - técnica de movimento lateral |
| **RAT** | Remote Access Tool/Trojan |
| **Kill Chain** | Modelo de fases sequenciais de ataque |

---

**Autor:** Bruno Neemias
**Data:** Fevereiro 2025  
**Curso:** Fundamentos de Cibersegurança - Módulo 3 - Aula 2  
**Fonte:** Material baseado em GitBook ESR-1 Fundamental Aula 05
