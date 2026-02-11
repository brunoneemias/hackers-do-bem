# 🛡️ Módulo 2 – Ameaças, Malwares e Controles
## Aula 4 – Fontes de Ameaça e Controles de Segurança

---

## 📋 Resumo Executivo

Esta aula aborda as principais **fontes de ameaça** na segurança cibernética e os **controles de segurança** utilizados para mitigá-las. Compreender quem são os atacantes, suas motivações e as tecnologias de defesa é fundamental para construir uma estratégia de segurança eficaz em camadas.

---

## 🎯 Objetivos de Aprendizagem

- ✅ Identificar as principais fontes de ameaça à segurança da informação
- ✅ Compreender os perfis e motivações dos agentes causadores de ataques
- ✅ Relacionar fontes de ameaça aos riscos cibernéticos organizacionais
- ✅ Conhecer os principais controles de segurança e suas aplicações

---

## 👥 Principais Fontes de Ameaça

### 1. **Hackers e Cibercriminosos**
- **Motivação:** Financeira (roubo de dados, fraudes, extorsão)
- **Táticas:** Ransomware, phishing, exploração de vulnerabilidades
- **Impacto:** Alto risco financeiro e reputacional

### 2. **Hacktivistas**
- **Motivação:** Ideológica ou política
- **Táticas:** DDoS, defacement, vazamento de dados
- **Objetivo:** Protesto, exposição pública, ativismo digital

### 3. **Insiders (Funcionários)**
- **Tipos:**
  - Ameaças intencionais (sabotagem, espionagem)
  - Ameaças acidentais (erro humano, falta de conscientização)
- **Risco:** Acesso privilegiado e conhecimento interno
- **Impacto:** Pode causar danos graves antes da detecção

### 4. **Falhas Tecnológicas**
- Sistemas desatualizados ou mal configurados
- Vulnerabilidades não corrigidas
- Erros de desenvolvimento (bugs, backdoors)

### 5. **Ameaças Ambientais**
- Desastres naturais (incêndios, inundações, terremotos)
- Falhas elétricas e de infraestrutura
- Requerem controles físicos e planos de contingência

---

## 🎭 Motivações dos Atacantes

| Motivação | Descrição | Exemplo |
|-----------|-----------|---------|
| **Financeira** | Lucro direto através de crimes cibernéticos | Ransomware, fraude bancária |
| **Espionagem** | Roubo de informações estratégicas | APTs, espionagem industrial |
| **Sabotagem** | Causar danos operacionais | Ataques a infraestruturas críticas |
| **Ideológica** | Protesto ou ativismo | Hacktivismo, vazamentos políticos |
| **Curiosidade/Desafio** | Teste de habilidades técnicas | Script kiddies, white hats |

---

## 🔐 Controles de Segurança

### **PAM – Privileged Access Management**
**Objetivo:** Gerenciar e monitorar acessos privilegiados (admins, root, contas de serviço)

**Funcionalidades:**
- Controle centralizado de credenciais privilegiadas
- Monitoramento e auditoria de sessões
- Rotação automática de senhas
- Acesso just-in-time

**Ferramentas:**
- CyberArk
- BeyondTrust
- Delinea (Thycotic)

---

### **MFA – Multi-Factor Authentication**
**Conceito:** Autenticação baseada em múltiplos fatores

**Fatores:**
1. **Algo que você sabe:** Senha, PIN
2. **Algo que você tem:** Token, smartphone, smart card
3. **Algo que você é:** Biometria (digital, facial, íris)

**Benefício:** Reduz drasticamente o risco de comprometimento de contas, mesmo com senha vazada

---

### **SIEM / NG SIEM**
**Security Information and Event Management**

**Função:**
- Coleta e correlação de logs de múltiplas fontes
- Análise em tempo real de eventos de segurança
- Alertas automatizados baseados em regras

**NG SIEM (Next Generation):**
- Utiliza Inteligência Artificial e Machine Learning
- Correlação avançada de ameaças
- Automação de resposta a incidentes
- Análise comportamental (UEBA)

**Exemplo:** Palo Alto Cortex XSIAM

---

### **Firewall**
**Função:** Controlar o tráfego de rede baseado em regras de segurança

**Tipos:**
- **Tradicional:** Filtragem por IP, porta e protocolo
- **NGFW (Next-Gen):** Inspeção profunda de pacotes, controle de aplicações
- **Stateful:** Mantém estado das conexões

**Aplicação:** Perímetro de rede, segmentação interna

---

### **EDR – Endpoint Detection and Response**
**Função:** Proteção avançada para endpoints (estações de trabalho, servidores)

**Capacidades:**
- Monitoramento contínuo de comportamento
- Detecção de ameaças baseada em IA
- Resposta automática a incidentes
- Análise forense e hunting

**Diferença chave:**

| Antivírus Tradicional | EDR |
|-----------------------|-----|
| Baseado em assinaturas | Baseado em comportamento |
| Reativo | Proativo e preditivo |
| Detecção básica | Detecção + resposta + investigação |
| Proteção limitada | Visibilidade completa do endpoint |

---

### **UTM – Unified Threat Management**
**Conceito:** Solução de segurança "tudo-em-um"

**Componentes integrados:**
- Firewall
- IDS/IPS (Detecção/Prevenção de Intrusões)
- Antivírus/Antimalware
- VPN
- Filtragem de conteúdo web
- Anti-spam

**Público-alvo:** Pequenas e médias empresas que precisam de segurança consolidada

---

### **WAF – Web Application Firewall**
**Função:** Proteção específica para aplicações web (camada 7 do modelo OSI)

**Protege contra:**
- SQL Injection
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Ataques DDoS em aplicações
- Exploração de APIs

**Diferencial:** Opera na camada de aplicação, entendendo requisições HTTP/HTTPS

---

### **Proxy**
**Função:** Servidor intermediário entre usuário e internet

**Limitações atuais:**
- Pode se tornar gargalo de rede
- Criptografia TLS/HTTPS reduz visibilidade
- Soluções modernas (NGFW, SASE) são mais eficientes

**Uso recomendado:**
- Controle de acesso à internet
- Cache de conteúdo
- Auditoria básica de navegação
- Ambientes legados

---

## 📊 Classificação de Controles de Segurança

### **1. Controles Preventivos**
**Objetivo:** Impedir que o incidente ocorra

**Exemplos:**
- Firewall
- MFA
- Políticas de senha forte
- Controle de acesso (RBAC)
- Criptografia de dados
- Hardening de sistemas

---

### **2. Controles Detectivos**
**Objetivo:** Identificar incidentes em andamento ou ocorridos

**Exemplos:**
- SIEM
- IDS (Intrusion Detection System)
- Análise de logs
- Monitoramento de rede
- Alertas de segurança
- Security Analytics

---

### **3. Controles Corretivos**
**Objetivo:** Remediar e restaurar após um incidente

**Exemplos:**
- Backup e restore
- Plano de resposta a incidentes (IRP)
- Patches e atualizações
- Restauração de sistemas
- Recuperação de dados

---

### **4. Controles Compensatórios**
**Conceito:** Controles alternativos quando o controle ideal não é viável

**Exemplo prático:**
- **Situação:** MFA não pode ser implementado em sistema legado
- **Compensação:** Monitoramento reforçado + restrição de acesso por IP + auditoria frequente

---

## 🔐 Políticas de Segurança Essenciais

### **Política de Senhas**
**Requisitos comuns:**
- Comprimento mínimo (12+ caracteres)
- Complexidade (maiúsculas, minúsculas, números, símbolos)
- Expiração periódica (controverso, tendência atual é remover)
- Histórico de senhas (evitar reutilização)
- Bloqueio após tentativas inválidas
- Proibição de senhas comuns/fracas

**Tendências modernas:**
- Uso de passphrases
- Foco em MFA ao invés de complexidade extrema
- Detecção de senhas comprometidas (Have I Been Pwned)

---

## 🏗️ Controles por Categoria

### **Controles Técnicos**
Implementados por hardware e software

**Exemplos:**
- Firewalls, IDS/IPS
- Antivírus, EDR
- Criptografia
- Sistemas de autenticação
- DLP (Data Loss Prevention)

### **Controles Físicos**
Protegem o ambiente físico da infraestrutura

**Exemplos:**
- Mantrap (porta dupla de segurança)
- Controle de acesso biométrico
- Câmeras de vigilância (CCTV)
- Alarmes
- Salas-cofre para servidores
- Detecção de incêndio/inundação

---

## 🔄 Continuidade de Negócios

### **DRP – Disaster Recovery Plan**
**Foco:** Recuperação técnica de sistemas de TI

**Elementos:**
- RTOs (Recovery Time Objectives)
- RPOs (Recovery Point Objectives)
- Procedimentos de backup e restore
- Infraestrutura alternativa
- Testes periódicos

### **BCP – Business Continuity Plan**
**Foco:** Manutenção de operações críticas do negócio

**Elementos:**
- Processos alternativos
- Comunicação de crise
- Locais alternativos de trabalho
- Priorização de serviços essenciais
- Coordenação entre áreas

**Diferença chave:** BCP é mais amplo que DRP; DRP é um componente técnico do BCP

---

## 🔧 Ferramentas Open Source em Destaque

### **pfSense**
**Descrição:** Firewall/roteador open source baseado em FreeBSD

**Recursos:**
- Firewall stateful
- VPN (IPsec, OpenVPN)
- IDS/IPS (Snort, Suricata)
- Proxy, DNS, DHCP
- Alta customização

**Uso:** Labs, SMBs, ambientes educacionais, projetos de segurança

**Vantagem:** Custo zero, comunidade ativa, ótimo para aprendizado

---

## 💡 Princípios Fundamentais

### **Defesa em Profundidade (Defense in Depth)**
Múltiplas camadas de segurança:
1. Perímetro (Firewall, WAF)
2. Rede (Segmentação, IDS/IPS)
3. Endpoint (EDR, Antivírus)
4. Aplicação (Secure coding, WAF)
5. Dados (Criptografia, DLP)
6. Usuário (MFA, Treinamento)

### **Princípio do Menor Privilégio**
Usuários e sistemas devem ter apenas os acessos necessários para suas funções

### **Zero Trust**
"Nunca confie, sempre verifique" - Verificação contínua mesmo dentro do perímetro

---

## 📝 Conclusão

A segurança da informação eficaz requer:

✅ **Tecnologias:** Ferramentas e soluções adequadas  
✅ **Processos:** Políticas, procedimentos e governança  
✅ **Pessoas:** Conscientização e treinamento contínuo  

**Princípio central:** 🔐 **Segurança em camadas**

Nenhum controle único é suficiente. A combinação estratégica de controles preventivos, detectivos e corretivos cria uma postura de segurança resiliente e adaptativa às ameaças em constante evolução.

---

## 🔗 Conceitos Relacionados
- CIA Triad (Confidencialidade, Integridade, Disponibilidade)
- Risk Management
- Incident Response
- Security Operations Center (SOC)
- Threat Intelligence

---

**Autor:** Bruno Neemias 
**Data:** Fevereiro 2025  
**Curso:** Fundamentos de Cibersegurança - Módulo 2
