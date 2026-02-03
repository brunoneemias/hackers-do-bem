# 🛡️ Hackers do Bem — Módulo 1  
## Princípios de Segurança da Informação & Engenharia Social

---

## 📌 Objetivos

- Compreender os fundamentos da Segurança da Informação  
- Entender a Tríade CID (Confidencialidade, Integridade e Disponibilidade)  
- Relacionar vulnerabilidade, ameaça e risco  
- Conhecer as principais funções da cibersegurança segundo o NIST Framework  

---

## 📚 Conceitos Básicos

### 🔐 Segurança da Informação

Proteção dos dados contra:

- Acesso não autorizado  
- Alterações indevidas  
- Roubo ou destruição  

Os dados precisam estar seguros durante:

- Armazenamento  
- Transmissão  
- Processamento  

---

## 📊 Tríade CID

### Confidencialidade  
Somente usuários autorizados podem acessar os dados.  

**Controles comuns:** senhas, MFA, criptografia  

### Integridade  
Os dados não podem ser alterados sem permissão.  

**Controles comuns:** hash, assinaturas digitais, versionamento  

### Disponibilidade  
Dados e sistemas acessíveis quando necessários.  

**Práticas comuns:** backup, redundância, plano de continuidade  

---

## ➕ Não Repúdio

Garante que um usuário não possa negar uma ação realizada digitalmente.

**Exemplo:** assinatura digital em contratos ou transações online.

---

## 🚨 Vulnerabilidade, Ameaça e Risco

| Conceito | Definição simples | Exemplo |
|--------|----------------|--------|
| Vulnerabilidade | Fraqueza do sistema | Senha fraca |
| Ameaça | Quem explora a fraqueza | Hacker, malware |
| Risco | Dano possível | Vazamento de dados |

**Fórmula:**  
`Risco = Probabilidade × Impacto`

---

## 🛡️ Estratégias de Tratamento de Riscos

- **Aceitar** — risco baixo  
- **Mitigar** — aplicar controles de segurança  
- **Transferir** — seguro ou terceiros  
- **Evitar** — eliminar a atividade vulnerável  

---

## 📈 Matriz de Risco

Ferramenta para análise de segurança com:

- Ameaças  
- Vulnerabilidades  
- Probabilidade  
- Impacto  
- Medidas de mitigação  

---

## 🧩 NIST Cybersecurity Framework

Modelo de referência para gestão de segurança cibernética.

### Estrutura:

- Funções  
- Categorias  
- Subcategorias  
- Referências técnicas  

---

## 🔁 Cinco Funções do NIST

1. **Identify** — conhecer ativos e riscos  
2. **Protect** — implementar controles  
3. **Detect** — monitorar incidentes  
4. **Respond** — conter ataques  
5. **Recover** — restaurar operações  

---

## ⚡ Resumo Rápido

- Segurança protege dados em todas as etapas  
- Tríade CID sustenta a proteção  
- Vulnerabilidade = fraqueza  
- Ameaça = quem explora  
- Risco = dano possível  
- NIST organiza a defesa cibernética em 5 funções  

---

## 🧰 Ferramentas e Conceitos Importantes em Cibersegurança

---

### 🌐 Tailscale (VPN moderna)

Ferramenta de VPN baseada em WireGuard que cria uma rede privada segura entre dispositivos.

**Como funciona:**
- Conecta PCs, servidores e celulares como se estivessem na mesma rede local  
- Usa criptografia forte ponta a ponta  
- Não exige configuração complexa de firewall  

**Uso comum:** acesso remoto seguro, laboratórios, ambientes corporativos.

---

### 📋 CIS Controls

Conjunto de boas práticas de segurança criado pelo Center for Internet Security.

**Como funciona:**
- Lista controles prioritários de proteção  
- Organiza ações práticas para reduzir riscos  
- Serve como guia de maturidade em segurança  

**Exemplo de controles:**
- Gerenciamento de ativos  
- Atualizações de sistemas  
- Monitoramento de logs  
- Controle de acessos  

---

### 🏢 MSSP (Managed Security Service Provider)

Empresas que prestam serviços de segurança gerenciados.

**Como funciona:**
- Monitoram ambientes 24/7  
- Gerenciam SIEM, firewalls, resposta a incidentes  
- Atuam como time de segurança terceirizado  

**Uso comum:** empresas que não têm SOC interno.

---

### 📊 UEBA (User and Entity Behavior Analytics)

Tecnologia que analisa o comportamento de usuários e sistemas para detectar anomalias.

**Como funciona:**
- Aprende padrões normais de uso  
- Identifica ações suspeitas (ex: login fora do horário, acesso estranho)  
- Usa IA e machine learning  

**Objetivo:** detectar ameaças internas e ataques sofisticados.

---

## 🛡️ Tecnologias de Monitoramento e Resposta

### 📈 SIEM (Security Information and Event Management)

Centraliza e analisa logs de segurança.

**Função principal:**
- Coletar eventos de sistemas  
- Correlacionar alertas  
- Detectar incidentes  

**Exemplo:** Elastic SIEM, Splunk, QRadar

---

### 🤖 SOAR (Security Orchestration, Automation and Response)

Automatiza respostas a incidentes.

**Função principal:**
- Executar playbooks automáticos  
- Responder rapidamente a alertas do SIEM  
- Reduzir tempo de resposta  

---

### 💻 EDR (Endpoint Detection and Response)

Proteção focada em dispositivos (PCs, servidores).

**Função principal:**
- Monitorar atividades suspeitas  
- Detectar malware e ataques  
- Responder em tempo real  

---

### 🌐 XDR (Extended Detection and Response)

Evolução do EDR, integrando múltiplas fontes.

**Função principal:**
- Unifica dados de endpoints, rede, email, cloud  
- Visão completa de ataques  
- Detecção mais inteligente  

---

## 📌 Resumo rápido das diferenças

| Tecnologia | Foco |
|-----------|-----|
| SIEM | Logs e eventos |
| SOAR | Automação de resposta |
| EDR | Proteção de endpoints |
| XDR | Visão integrada de tudo |
| UEBA | Comportamento anômalo |


