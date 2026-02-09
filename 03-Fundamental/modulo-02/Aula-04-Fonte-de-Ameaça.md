# 🛡️ Módulo 2 – Ameaças, Malwares e Controles  
## Aula 4 – Fontes de Ameaça

---

## 🎯 Objetivos

- Identificar as principais fontes de ameaça  
- Compreender quem são os agentes causadores de ataques  
- Relacionar fontes de ameaça aos riscos cibernéticos  

---

## 📚 Conceitos Abordados

- Fontes de ameaça  
- Agentes internos e externos  
- Motivação dos atacantes  

---

## 🧠 Introdução

As fontes de ameaça representam os **atores ou origens** responsáveis por gerar riscos à segurança da informação.  
Elas podem ser humanas, técnicas ou ambientais, e compreender essas fontes ajuda a prever ataques e fortalecer a defesa.

---

## 👤 Principais Fontes de Ameaça

### 🧑‍💻 Hackers e Cibercriminosos
- Motivação financeira
- Roubo de dados
- Fraudes e extorsão

---

### 🕵️ Hacktivistas
- Motivação ideológica ou política
- Ataques para protesto ou exposição pública

---

### 🏢 Funcionários e Insiders
- Ameaças intencionais ou acidentais
- Uso indevido de acessos
- Falta de conscientização em segurança

---

### 🛠️ Falhas Tecnológicas
- Sistemas desatualizados
- Configurações incorretas
- Vulnerabilidades não corrigidas

---

### 🌪️ Ameaças Ambientais
- Falhas elétricas
- Incêndios
- Desastres naturais

---

## 🎯 Motivação das Fontes de Ameaça

As ameaças podem ter diferentes objetivos:

- Financeiros
- Espionagem
- Sabotagem
- Ideológicos
- Curiosidade ou desafio técnico

---

---

# 🔐 Controles de Segurança

## 🔑 PAM – Privileged Access Management

Gerenciamento de acessos privilegiados (admins, root, etc).

### Objetivo:
- Controlar, monitorar e auditar acessos críticos  
- Reduzir riscos de abuso de privilégios  

### Exemplos de software:
- CyberArk  
- BeyondTrust  
- Delinea  

---

## 🔐 MFA – Multi-Factor Authentication

Autenticação baseada em **mais de um fator**:

- Algo que você sabe (senha)
- Algo que você tem (token, celular)
- Algo que você é (biometria)

📌 Reduz drasticamente riscos de comprometimento de contas.

---

## 📊 SIEM – NG SIEM (ex: Palo Alto)

### O que é:
Plataforma que **coleta, correlaciona e analisa logs** de múltiplas fontes.

### NG SIEM (Next Generation):
- Usa IA e automação
- Correlação avançada
- Detecção de ameaças em tempo real

### Exemplo:
- Palo Alto Cortex XSIAM  

---

## 🔥 Firewall

Dispositivo ou software que **controla o tráfego de rede** com base em regras.

### Função:
- Permitir ou bloquear conexões  
- Monitorar o que entra e sai da rede  

---

## 🖥️ EDR – Endpoint Detection and Response

Proteção avançada para endpoints (PCs, servidores).

### Funções:
- Monitoramento contínuo
- Detecção de comportamento suspeito
- Resposta automática a incidentes

### Diferença entre EDR e Antivírus:
| Antivírus | EDR |
|---------|-----|
| Baseado em assinatura | Baseado em comportamento |
| Reativo | Proativo |
| Detecção básica | Detecção + resposta |

---

## 🌐 UTM – Unified Threat Management

Solução unificada de segurança.

Inclui:
- Firewall
- IDS/IPS
- Antivírus
- VPN

📌 Comum em pequenas e médias empresas.

---

## 🌍 WAF – Web Application Firewall

Firewall focado em **aplicações web**.

### Protege contra:
- SQL Injection
- XSS
- Ataques HTTP/S

📌 Atua na camada de aplicação (Layer 7).

---

## 🧭 Proxy

Servidor intermediário entre usuário e internet.

### Por que não é tão recomendado hoje?
- Pode virar gargalo de rede
- Criptografia HTTPS reduz visibilidade
- Soluções modernas (NGFW, SASE) são mais eficientes

Ainda pode ser usado para:
- Controle de acesso
- Cache
- Auditoria simples

---

# 🛡️ Tipos de Controles de Segurança

## 🚫 Controles Preventivos
Impedem que o incidente ocorra.

**Exemplos:**
- Firewall
- MFA
- Política de senha
- Controle de acesso

---

## 🔍 Controles Detectivos
Identificam incidentes em andamento.

**Exemplos:**
- SIEM
- IDS
- Logs
- Monitoramento

---

## 🔄 Controles Corretivos
Atuam após o incidente.

**Exemplos:**
- Backup
- Plano de resposta a incidentes
- Restauração de sistemas

---

## 🔐 Política de Senhas

Define regras para:
- Complexidade
- Expiração
- Histórico
- Bloqueio por tentativas inválidas

📌 Fundamental para reduzir ataques de força bruta.

---

## 🧩 Controles Técnicos

Implementados por **hardware e software**.

**Exemplos:**
- Firewall
- Antivírus
- EDR
- IDS/IPS

---

## 🚨 DRP – Disaster Recovery Plan

Plano de recuperação de desastres.

### Objetivo:
- Restaurar sistemas após incidentes graves  
- Minimizar tempo de indisponibilidade  

---

## 🔄 Continuidade de Negócios (BCP)

Plano que garante que **serviços essenciais não parem**, mesmo em incidentes.

📌 Foco no negócio, não apenas na TI.

---

## 🏢 Controles Físicos

Protegem o ambiente físico.

**Exemplos:**
- Mantrap
- Alarmes
- Câmeras
- Controle de acesso físico

---

## 🔥 pfSense

Firewall **open source** baseado em FreeBSD.

### Recursos:
- Firewall
- VPN
- IDS/IPS
- Alta personalização

📌 Muito usado em labs, SMBs e estudos de segurança.

---

## 🧯 Controle Compensatório

Controle alternativo usado quando o controle ideal não é possível.

**Exemplo:**
- Sem MFA → monitoramento reforçado + restrição de acesso

---

## 📌 Conclusão

A segurança da informação depende da combinação de:

✔️ Tecnologias  
✔️ Processos  
✔️ Pessoas  

Controles bem definidos reduzem riscos, aumentam visibilidade e fortalecem a resiliência da organização frente às ameaças.

🔐 Segurança eficaz é feita em camadas.

---
