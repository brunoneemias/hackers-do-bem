# 🔍 Módulo 3 – Técnicas de Identificação de Ameaças
## Aula 1 – Gerenciamento de Vulnerabilidades

---

## 📋 Resumo Executivo

Esta aula aborda as **técnicas e metodologias** para gerenciamento de vulnerabilidades em sistemas e redes. Compreender como realizar avaliações de segurança, interpretar resultados de varreduras e validar descobertas é essencial para manter uma postura defensiva robusta contra ameaças cibernéticas.

---

## 🎯 Objetivos de Aprendizagem

- ✅ Compreender os conceitos-chave do gerenciamento de vulnerabilidades
- ✅ Assimilar técnicas e métodos de verificação de segurança
- ✅ Conhecer e interpretar resultados de varreduras de segurança
- ✅ Diferenciar tipos de varredura e seus contextos de aplicação
- ✅ Entender falsos positivos, falsos negativos e análise de logs

---

## 📚 Conceitos Fundamentais

- Verificação de vulnerabilidades (técnicas e tipos)
- Avaliação de segurança
- Varredura credenciada vs. não credenciada
- Varredura intrusiva vs. não intrusiva
- Falsos positivos e falsos negativos
- CVE (Common Vulnerabilities and Exposures)
- Análise de logs
- Revisão de configurações

---

## 🛡️ Introdução ao Gerenciamento de Vulnerabilidades

### **O Que São Vulnerabilidades?**

Vulnerabilidades são **falhas ou fraquezas** em sistemas, aplicações ou configurações que podem ser exploradas por atacantes para:
- Comprometer a segurança
- Acessar informações confidenciais
- Causar indisponibilidade de serviços
- Executar código malicioso

**Importância:** 
A exploração de vulnerabilidades é um dos métodos mais comuns usados por cibercriminosos para comprometer sistemas e causar danos. Em um cenário onde a cibersegurança desempenha um papel crucial na proteção de informações sensíveis, compreender e gerenciar vulnerabilidades é essencial.

---

## 🔎 Avaliações de Segurança

### **Framework NIST SP 800-115**

Baseadas no framework **NIST SP 800-115**, as avaliações de segurança envolvem três atividades principais:

1. **Testar:** Descobrir vulnerabilidades ou comprovar eficácia dos controles de segurança
2. **Examinar:** Compreender o sistema de segurança e identificar pontos fracos lógicos, configurações incorretas comuns ou falta de controles
3. **Entrevistar:** Recolher informações e sondar atitudes e compreensão da segurança do pessoal

### **Tipos de Avaliação de Segurança**

| Tipo | Descrição | Abordagem |
|------|-----------|-----------|
| **Verificação de Vulnerabilidade** | Avaliação da configuração vs. baseline ideal | Automatizada/Manual |
| **Caça a Ameaças (Threat Hunting)** | Busca proativa por indicadores de comprometimento | Investigativa |
| **Teste de Penetração** | Simulação de ataque real | Ofensiva controlada |

---

### **Verificação de Vulnerabilidade**

**Definição:** 
Avaliação da segurança e da capacidade de um sistema de atender aos requisitos de conformidade com base no estado de configuração do sistema. Essencialmente, determina se a configuração atual corresponde à configuração ideal (a linha de base/baseline).

**Características:**
- Pode envolver inspeção manual, mas é mais frequente através de scanners automatizados
- Parte essencial da gestão de riscos de segurança cibernética
- Ajuda organizações a entender e reduzir riscos
- Mantém integridade e confidencialidade de sistemas e dados

**Uso das descobertas:**
As descobertas são usadas para priorizar implementação de medidas de segurança:
- Correções de software (patches)
- Configurações seguras
- Políticas de acesso

---

## 🔧 Técnicas de Verificação de Vulnerabilidades

A verificação é o processo de identificação, avaliação e análise das fraquezas e falhas de segurança em sistemas, redes, aplicativos ou infraestrutura de TI.

**Objetivo:**
Identificar e documentar vulnerabilidades existentes, avaliar seu impacto e probabilidade de exploração, e recomendar medidas para mitigar ou corrigir essas falhas.

### **Duas Abordagens Principais**

As técnicas podem ser categorizadas em dois grupos principais, frequentemente usadas em conjunto:

---

### **1. Varreduras Automatizadas**

**Características:**
- Uso de software especializado
- Examina sistemas e redes em busca de vulnerabilidades conhecidas
- Identifica ampla gama de vulnerabilidades em curto espaço de tempo
- Eficientes para cobertura ampla
- Baseadas em assinaturas e scripts

**Como funcionam:**
Uma varredura automatizada deve ser configurada com assinaturas e scripts que possam correlacionar software conhecido e vulnerabilidades de configuração com dados coletados de cada host.

**Variedade de scanners:**
Existem vários tipos de scanners de vulnerabilidade otimizados para diferentes tarefas. A seleção da ferramenta adequada depende dos requisitos específicos de verificação e do ambiente.

**Ferramentas Populares:**

| Ferramenta | Tipo | Uso Principal |
|------------|------|---------------|
| **Nmap (Network Mapper)** | Scanner de rede | Descoberta de dispositivos, portas abertas e serviços |
| **OpenVAS** | Scanner de vulnerabilidades | Framework open source completo de varredura |
| **Nessus** | Scanner comercial | Varredura abrangente de vulnerabilidades |
| **Burp Suite** | Web scanner | Teste de segurança de aplicações web |
| **Wireshark** | Analisador de tráfego | Análise de pacotes e potenciais vulnerabilidades |

**Limitações:**
❌ Podem não detectar vulnerabilidades novas ou customizadas  
❌ Requerem atualização constante de assinaturas  
❌ Falsos positivos são comuns  

**Manutenção:**
É importante manter essas ferramentas atualizadas, pois novas vulnerabilidades são descobertas regularmente.

---

### **2. Testes Manuais**

**Características:**
- Análise minuciosa por profissionais de segurança cibernética
- Usam habilidades e conhecimentos para identificar vulnerabilidades
- Detectam falhas que ferramentas automatizadas podem perder
- Contexto e expertise humana

**Quando usar:**
- Particularmente úteis para avaliar segurança de sistemas complexos e personalizados
- Lógica de negócio complexa
- Aplicações customizadas
- Validação de falsos positivos
- Testes de engenharia social

---

## 🌐 CVE – Common Vulnerabilities and Exposures

### **O que é CVE?**

**Definição:**
Sistema internacional de identificação e nomeação padronizada de vulnerabilidades de segurança cibernética em sistemas de software e hardware.

**Organização:**
Mantido e gerenciado pela **MITRE Corporation**, em colaboração com diversas entidades de segurança cibernética em todo o mundo.

**Objetivo principal:**
Fornecer uma lista padronizada de identificadores únicos para vulnerabilidades conhecidas, facilitando:
- Compartilhamento de informações entre organizações
- Coordenação de esforços de correção
- Integração em sistemas de segurança
- Uso em ferramentas de verificação de vulnerabilidades

---

### **Estrutura de um CVE**

**Formato do identificador:**
```
CVE-YYYY-####

Onde:
- CVE = Common Vulnerabilities and Exposures
- YYYY = Ano de descoberta
- #### = Número sequencial (mínimo 4 dígitos)
```

**Exemplo real:**
```
CVE-2021-44228 (Log4Shell)
- Ano: 2021
- Número: 44228
- Severidade: Crítica (CVSS 10.0)
- Descrição: Vulnerabilidade de execução remota de código no Apache Log4j
```

---

### **Componentes de uma Entrada CVE**

Cada entrada CVE contém os seguintes elementos:

1. **Identificador único** no formato CVE-YYYY-####
2. **Descrição da vulnerabilidade:** Explicação do problema
3. **Impacto potencial:** Consequências da exploração
4. **Versões afetadas:** Softwares/hardwares vulneráveis
5. **Soluções ou correções disponíveis:** Patches, workarounds
6. **Lista de referência de URLs:** Mais informações sobre a vulnerabilidade
7. **Data de criação:** Quando a entrada foi registrada

---

### **Características do Sistema CVE**

**Sistema de nomeação padronizado:**
Segue um padrão bem definido, facilitando a comunicação e referência a vulnerabilidades de forma consistente em todo o setor de segurança cibernética.

**Acesso público:**
As informações listadas no CVE são de acesso público e podem ser consultadas por qualquer pessoa, incluindo:
- Profissionais de segurança
- Desenvolvedores de software
- Pesquisadores

**Colaboração global:**
Iniciativa que conta com a colaboração de muitos especialistas em segurança cibernética em todo o mundo para identificar, nomear e documentar vulnerabilidades.

**Fonte oficial:**
[cve.mitre.org](https://cve.mitre.org)

**Bancos de dados relacionados:**
- National Vulnerability Database (NVD) - NIST
- Bancos de dados de vendors específicos

---

## 🔍 Tipos de Varredura por Intrusividade

### **Varredura Intrusiva (Ativa)**

**Definição:**
Varreduras que envolvem ações que podem impactar o sistema ou rede verificados.

**Características:**
- Interage ativamente com o alvo
- Pode interromper funcionamento normal dos sistemas
- Pode causar quedas de serviço
- Potencialmente explora vulnerabilidades de maneira ativa
- Consome mais largura de banda da rede
- Corre o risco de travar o alvo da varredura
- Pode causar algum tipo de interrupção

**Técnicas:**
A varredura ativa significa testar a configuração do dispositivo usando algum tipo de conexão de rede com o alvo. A varredura baseada em agente também é uma técnica ativa.

**Nível máximo de intrusão:**
O tipo mais intrusivo de scanner de vulnerabilidade não para na detecção de uma vulnerabilidade. As estruturas de exploração (exploit frameworks) contêm scripts padrão para tentar usar uma vulnerabilidade para executar código ou obter acesso ao sistema.

**Exemplos práticos:**
- Tentativa de autenticação com credenciais incorretas para testar resistência a login não autorizado
- Uso de exploits ou técnicas de invasão para verificar se vulnerabilidade é explorável
- Testes que podem interromper serviços

**Vantagens:**
✅ Identifica vulnerabilidades que varreduras passivas podem perder  
✅ Exploram ativamente as fraquezas  
✅ Úteis para verificar exploração real de vulnerabilidades  
✅ Avaliam resistência a ataques  

**Desvantagens:**
❌ Potencial para causar impacto adverso nos sistemas verificados  
❌ Risco de interrupções de serviço  
❌ Devem ser realizadas com cautela  
❌ Geralmente apenas em ambientes controlados  

---

### **Varredura Não Intrusiva (Passiva)**

**Definição:**
Projetadas para serem não perturbadoras e não causar impacto nos sistemas verificados.

**Características:**
- Observam sistemas e redes de fora
- Não tentam explorar ativamente vulnerabilidades
- Analisam evidências indiretas
- Menor impacto na rede e nos hosts
- Menos provável de identificar vulnerabilidades de forma abrangente

**Técnicas:**
A varredura passiva significa analisar evidências indiretas, como os tipos de tráfego gerados por um dispositivo. Um scanner passivo analisa uma captura de rede e tenta identificar desvios de política ou correspondências de CVE.

**Ferramenta exemplo:**
**Zeek Network Security Monitor** (zeek.org) - analisa captura de rede e identifica desvios de política ou correspondências de CVE.

**Exemplos práticos:**
- Coleta de informações por meio de análise de tráfego de rede
- Pesquisa de informações publicamente disponíveis
- Análise de configurações de sistemas
- Verificação de portas abertas (sem conexão ativa)

**Quando usar varredura passiva:**
Use esta técnica onde a varredura ativa representa sério risco à estabilidade do sistema:
- Dispositivos de impressão
- Dispositivos VoIP
- Sistemas de rede integrados (embedded)
- Sistemas industriais (ICS/SCADA)

**Vantagens:**
✅ Seguras e não causam interrupções  
✅ Ideais para monitorar superfície de ataque  
✅ Identificam vulnerabilidades sem perturbar funcionamento  
✅ Não são detectadas pelo alvo  

**Desvantagens:**
❌ Podem não detectar vulnerabilidades que requerem exploração ativa  
❌ Informações limitadas podem estar disponíveis  
❌ Não avaliam completamente o risco  
❌ Pode ser usada por agentes de ameaça para verificar rede furtivamente  

---

### **Comparação: Intrusiva vs. Não Intrusiva**

| Aspecto | Intrusiva (Ativa) | Não Intrusiva (Passiva) |
|---------|-------------------|-------------------------|
| **Interação** | Direta com o alvo | Observação externa |
| **Impacto** | Pode causar interrupções | Sem perturbação |
| **Detecção** | Alta probabilidade | Muito baixa |
| **Informações** | Detalhadas e validadas | Limitadas e indiretas |
| **Risco** | Alto (crashes, downtime) | Muito baixo |
| **Uso ideal** | Ambientes de teste | Sistemas críticos |
| **Largura de banda** | Consome mais | Consome menos |

---

## 🔐 Tipos de Varredura por Autenticação

### **Varredura Credenciada (Authenticated Scan)**

**Definição:**
Processo de verificação que envolve o uso de credenciais válidas (nomes de usuário e senhas) para autenticar-se nos sistemas ou dispositivos sendo analisados.

**Características:**
- Usa credenciais válidas
- Acesso com permissões apropriadas para as rotinas de teste
- Permite acesso a áreas mais profundas e restritas dos sistemas
- Acessa arquivos e configurações sensíveis
- Resulta em verificação mais completa e precisa
- Tipo de verificação mais intrusiva que a não credenciada

**O que mostra:**
Demonstra o que um ataque interno, ou aquele em que o invasor comprometeu uma conta de usuário, pode conseguir.

**Vantagens:**
✅ Resultados mais detalhados e precisos  
✅ Identifica vulnerabilidades não visíveis externamente  
✅ Eficaz para identificar problemas de configuração e atualização  
✅ Verifica patches instalados  
✅ Valida compliance e hardening  
✅ Menor taxa de falsos negativos  

**Desvantagens:**
❌ Exige cooperação dos proprietários dos sistemas  
❌ Acesso com credenciais deve ser concedido  
❌ Mais demorada e complexa de configurar  
❌ Requer gerenciamento de credenciais  

---

### **Varredura Não Credenciada (Unauthenticated Scan)**

**Definição:**
Ferramenta de verificação não faz uso de credenciais válidas. Direciona pacotes de teste para um host sem ser capaz de fazer logon no sistema operacional ou no aplicativo.

**Características:**
- Examina sistemas e redes de fora
- Como um observador externo
- Ausência de credenciais restringe acesso
- Limitada a informações e configurações disponíveis publicamente
- Visão que o host expõe a usuário sem privilégios na rede

**Rotinas de teste:**
Podem incluir coisas como:
- Uso de senhas padrão para contas de serviço
- Interfaces de gerenciamento de dispositivos
- Não recebem acesso privilegiado

**Técnica apropriada para:**
- Avaliação externa do perímetro da rede
- Executar verificação de aplicativos da web
- Pensar como invasor sem permissões específicas de alto nível
- Quando não há acesso administrativo total

**Vantagens:**
✅ Rápidas e fáceis de implementar  
✅ Não exigem cooperação dos proprietários  
✅ Úteis para identificar vulnerabilidades exploráveis por invasores externos  
✅ Perspectiva de atacante externo  
✅ Identificam exposição pública  

**Desvantagens:**
❌ Não detectam vulnerabilidades internas  
❌ Falta de acesso com credenciais  
❌ Não identificam problemas de configuração interna  
❌ Não verificam atualizações instaladas  
❌ Alta taxa de falsos negativos  

---

### **Escolha Entre Credenciada e Não Credenciada**

**Recomendação geral:**
Em muitos casos, é recomendável usar **ambas as abordagens**, permitindo análise abrangente que aborde vulnerabilidades internas e externas.

**Fatores de decisão:**
- Objetivos da avaliação de segurança
- Circunstâncias específicas do ambiente
- Tipo de ameaças a considerar (internas vs. externas)
- Requisitos de compliance

---

## ⚠️ Falsos Positivos, Falsos Negativos e Análise de Log

### **Relatórios de Varredura**

Após conclusão da varredura, a ferramenta gera um relatório resumido de todas as vulnerabilidades descobertas.

**Características do relatório:**
- Vulnerabilidades codificadas por cores em termos de criticidade
- Vermelho normalmente denota fraqueza que requer atenção imediata
- Visualização por escopo (mais críticas em todos os hosts) ou por host
- Inclui ou vincula detalhes específicos sobre cada vulnerabilidade
- Como os hosts podem ser corrigidos

---

### **Falso Positivo**

**Definição:**
A ferramenta de verificação identifica erroneamente uma vulnerabilidade que **na realidade não existe** no sistema ou rede.

**Causas:**
- Falsas interpretações
- Configurações inadequadas da ferramenta
- Limitações da ferramenta de verificação
- Heurísticas muito agressivas
- Banner grabbing impreciso

**Impacto:**
- Tempo desperdiçado na investigação
- Correção de problemas inexistentes
- Recursos gastos desnecessariamente
- Fadiga de alertas (alert fatigue)
- Perda de confiança na ferramenta

**Exemplo prático:**
```
Scanner reporta: "Apache 2.2.x vulnerável a CVE-2014-0160 (Heartbleed)"
Realidade: Versão foi atualizada para 2.4.x, mas banner não foi alterado
Resultado: Falso positivo
```

---

### **Verdadeiro Positivo**

**Definição:**
Ocorre em um teste de detecção quando o resultado indica corretamente a presença de uma condição ou característica que está presente de fato.

**Exemplo:**
Num teste de detecção de um antivírus, se o software identifica corretamente um arquivo malicioso como sendo malicioso, isso é considerado um verdadeiro positivo.

**Ação necessária:**
✅ **Remediar imediatamente** conforme criticidade

---

### **Falso Negativo**

**Definição:**
A ferramenta de verificação **não detecta** uma vulnerabilidade real que está presente no sistema ou rede.

**Causas:**
- Falhas na detecção da ferramenta
- Configurações inadequadas
- Falta de visibilidade na varredura
- Assinaturas desatualizadas
- Vulnerabilidades zero-day
- Varredura não credenciada quando necessário

**Impacto:**
⚠️ **Particularmente perigosos:**
- Vulnerabilidades reais não estão sendo tratadas
- Colocam em risco a segurança
- Falsa sensação de segurança
- Sistema pode ser comprometido

**Mitigação:**
Para reduzir este risco:
- Executar varreduras repetidas periodicamente
- Usar scanners de mais de um fornecedor
- Complementar com testes manuais
- Realizar threat hunting
- Correlacionar com logs

---

### **Verdadeiro Negativo**

**Definição:**
Ocorre quando um teste indica corretamente a ausência de uma condição ou característica que realmente não está presente.

**Exemplo:**
Num teste de detecção de um antivírus, se o software corretamente determina que um arquivo não possui ameaças, isso é considerado um verdadeiro negativo.

**Resultado:**
✅ Sistema está seguro em relação àquela verificação específica

---

### **Matriz de Resultados**

| Resultado | Vulnerabilidade Existe? | Scanner Detecta? | Ação |
|-----------|------------------------|------------------|------|
| **Verdadeiro Positivo** | ✅ Sim | ✅ Sim | Remediar |
| **Verdadeiro Negativo** | ❌ Não | ❌ Não | Manter |
| **Falso Positivo** | ❌ Não | ✅ Sim (erro) | Investigar e descartar |
| **Falso Negativo** | ✅ Sim | ❌ Não (erro) | ⚠️ **Maior risco!** |

---

### **Análise de Logs**

**Objetivo:**
A revisão dos logs de rede e do sistema relacionados pode aprimorar o processo de validação do relatório de vulnerabilidade.

**Como auxilia:**
A análise de logs ajuda na confirmação dos resultados de varreduras. Envolve revisão de registros de eventos e atividades de sistemas, aplicativos e redes para verificar se as vulnerabilidades identificadas são genuínas ou não.

**Distinguindo falsos positivos:**
Ao examinar registros de eventos, os administradores de segurança podem rastrear a atividade que levou à identificação da vulnerabilidade. Se não houver evidências nos logs de que a vulnerabilidade foi explorada, pode ser um falso positivo.

**Revelando falsos negativos:**
Se os registros mostrarem tentativas ou atividades suspeitas que não foram identificadas pela ferramenta de verificação, isso pode indicar a presença de vulnerabilidades não detectadas.

---

### **Vantagens da Análise de Logs**

✅ Distingue entre falsos positivos e vulnerabilidades reais  
✅ Revela possíveis falsos negativos  
✅ Fornece contexto temporal dos eventos  
✅ Correlaciona eventos de segurança  
✅ Evidências forenses para investigação  
✅ Valida descobertas do scanner  

---

### **Desvantagens da Análise de Logs**

❌ **Volume massivo de dados:**
- Requer recursos significativos de hardware e software
- Armazenamento
- Capacidade de processamento
- Ferramentas de análise

❌ **Ruído (informações irrelevantes):**
- Grande quantidade de eventos de rotina
- Dificulta identificação de eventos importantes

❌ **Falta de padronização:**
- Logs de diferentes sistemas usam formatos diferentes
- Estruturas variadas
- Torna análise mais desafiadora

❌ **Retenção inadequada:**
- Pode limitar capacidade de análise histórica
- Logs podem ser sobrescritos

❌ **Correlação complexa:**
- Correlacionar eventos de múltiplas fontes
- Pode se tornar complicada

❌ **Expertise necessária:**
- Requer conhecimento e habilidades especializadas
- Treinamento específico em análise de logs

---

### **Requisitos para Análise Eficaz**

Para realizar uma análise de logs eficaz:

1. **Sistemas bem configurados:**
   - Registrar informações relevantes de maneira adequada
   - Nível apropriado de logging

2. **Habilidades necessárias:**
   - Administradores com expertise para interpretar registros
   - Conhecimento de SIEM e ferramentas de análise

3. **Ferramentas adequadas:**
   - SIEM (Security Information and Event Management)
   - Log aggregation
   - Análise comportamental

---

## 🔧 Revisão de Configurações

### **O Que É?**

**Definição:**
Prática que envolve a análise e aprimoramento das configurações de sistemas, aplicativos e redes para garantir que atendam a padrões de segurança e estejam protegidos contra ameaças cibernéticas.

---

### **Etapas do Processo de Revisão**

### **1. Identificação das Configurações**

Identificar as configurações que precisam ser revisadas:
- Políticas de segurança
- Configurações de firewall
- Permissões de acesso
- Configurações de criptografia
- Configurações de aplicativos
- Parâmetros do sistema operacional

---

### **2. Avaliação de Conformidade**

Avaliar conformidade com:
- Políticas de segurança organizacionais
- Regulamentações (LGPD, PCI-DSS, HIPAA)
- Melhores práticas da indústria
- Baselines de segurança

**Ferramentas:**
Ferramentas de avaliação de conformidade podem ser úteis nesse processo.

---

### **3. Análise de Vulnerabilidades**

A revisão deve incluir análise de vulnerabilidades potenciais devido a configurações inadequadas:
- Identificação de portas abertas desnecessárias
- Protocolos fracos ou desatualizados
- Permissões excessivas
- Serviços desnecessários habilitados
- Senhas padrão
- Criptografia fraca ou ausente

---

### **4. Documentação e Registro**

**Importância:**
Manter registros detalhados é essencial.

**O que documentar:**
- Configurações existentes
- Alterações realizadas
- Justificativas por trás das alterações
- Histórico de mudanças
- Baseline de configuração

**Benefícios:**
- Ajuda a rastrear histórico de configurações
- Simplifica solução de problemas futuros
- Facilita auditorias
- Permite rollback se necessário

---

### **5. Implementação de Correções**

Com base na análise realizada, implementar correções e melhorias:
- Reconfiguração de sistemas
- Aplicação de patches
- Atualização de políticas
- Outras ações corretivas
- Hardening de sistemas

---

### **6. Teste e Validação**

Após implementar correções:
- Testar novas configurações
- Validar que não causam problemas de funcionalidade
- Verificar que não introduzem problemas de segurança não intencionais

**Métodos de validação:**
- Testes de penetração
- Verificações de vulnerabilidade
- Testes funcionais
- Testes de regressão

---

### **Frameworks de Referência para Configuração Segura**

- **CIS Benchmarks:** Guias detalhados por tecnologia
- **NIST Cybersecurity Framework:** Framework abrangente
- **DISA STIGs:** Security Technical Implementation Guides
- **OWASP:** Para aplicações web
- **PCI-DSS:** Para ambientes de pagamento

---

## 💡 Conclusão

### **Principais Takeaways**

✅ **Gerenciamento contínuo:** Vulnerabilidades são processo contínuo, não pontual  
✅ **Complementaridade:** Scanners automatizados são eficientes, mas não substituem análise humana  
✅ **Profundidade:** Varreduras credenciadas fornecem visão mais profunda que não credenciadas  
✅ **Validação:** Falsos positivos/negativos exigem validação e correlação com logs  
✅ **Padronização:** CVE é padrão universal para identificação de vulnerabilidades  
✅ **Configuração:** Configurações seguras são tão importantes quanto patches  
✅ **Múltiplas abordagens:** Combine varreduras ativas/passivas, credenciadas/não credenciadas  

---

### **Processo Completo de Gerenciamento**

```
┌─────────────────────────┐
│  1. Identificar Ativos  │
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│   2. Varrer (Scan)      │ ← Automatizado + Manual
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│  3. Analisar Resultados │ ← Validar falsos +/-
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│  4. Priorizar Riscos    │ ← CVSS, impacto negócio
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│    5. Remediar          │ ← Patches, config
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│   6. Verificar Fix      │ ← Re-scan
└───────────┬─────────────┘
            ↓
┌─────────────────────────┐
│  7. Documentar          │
└───────────┬─────────────┘
            ↓
        (Repetir ciclo)
```

---

## 🎓 Frameworks e Metodologias de Referência

- **NIST SP 800-115:** Technical Guide to Information Security Testing
- **CIS Controls:** Controles prioritizados de segurança cibernética
- **OWASP Testing Guide:** Metodologia para testes de aplicações web
- **CVSS (Common Vulnerability Scoring System):** Sistema de pontuação de vulnerabilidades
- **ISO 27001:** Padrão internacional de gestão de segurança da informação

---

## 🔗 Conceitos Relacionados

- **Patch Management:** Gerenciamento de atualizações de segurança
- **Asset Management:** Inventário e gerenciamento de ativos
- **Configuration Management:** Gerenciamento de configurações
- **Threat Intelligence:** Inteligência de ameaças
- **Risk Assessment:** Avaliação de riscos
- **Compliance Management:** Gestão de conformidade
- **Security Operations Center (SOC):** Centro de operações de segurança

---

## 📚 Glossário de Termos

| Termo | Definição |
|-------|-----------|
| **CVE** | Common Vulnerabilities and Exposures - Sistema de identificação de vulnerabilidades |
| **CVSS** | Common Vulnerability Scoring System - Sistema de pontuação de severidade |
| **Baseline** | Configuração padrão segura de referência |
| **Hardening** | Processo de tornar sistema mais seguro reduzindo superfície de ataque |
| **Zero-day** | Vulnerabilidade desconhecida pelo vendor sem patch disponível |
| **Exploit** | Código ou técnica que explora uma vulnerabilidade |
| **Banner grabbing** | Técnica de coletar informações de serviços através de banners |

---

**Autor:** [Seu Nome]  
**Data:** Fevereiro 2025  
**Curso:** Fundamentos de Cibersegurança - Módulo 3 - Aula 1  
**Fonte:** Material baseado em GitBook ESR-1 Fundamental Aula 05
