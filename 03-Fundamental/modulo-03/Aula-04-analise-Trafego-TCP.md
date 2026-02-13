# 🌐 Módulo 3 – Técnicas de Identificação de Ameaças
## Aula 4 – Análise de Tráfego TCP/IP

---

## 📋 Resumo Executivo

Esta aula aborda as **ferramentas essenciais de detecção e análise de rede** no contexto TCP/IP. Compreender como utilizar ferramentas de linha de comando, scanners de rede e analisadores de protocolo é fundamental para avaliar a segurança organizacional, identificar vulnerabilidades e detectar atividades suspeitas em redes corporativas.

---

## 🎯 Objetivos de Aprendizagem

- ✅ Entender os conceitos e utilidades de ferramentas de detecção de redes
- ✅ Assimilar o potencial da avaliação da segurança no contexto das redes TCP/IP
- ✅ Compreender o conceito e utilidade de ferramentas como Wireshark
- ✅ Dominar ferramentas de linha de comando para diagnóstico de rede
- ✅ Conhecer técnicas de descoberta de topologia e serviços

---

## 📚 Conceitos Fundamentais

- Ferramentas de detecção de rede no ambiente TCP/IP
- Comandos de linha de comando (ipconfig, ifconfig, ping, arp, route)
- Ferramentas de rastreamento (traceroute, tracert, pathping)
- Scanners IP (Nmap)
- Descoberta de serviços e portas
- Análise de pacotes com Wireshark
- Sniffers e analisadores de protocolo

---

## 🧠 Introdução

Bem-vindos à aula sobre **Análise de Tráfego TCP/IP**.

Hoje abordaremos o tema da segurança organizacional, explorando ferramentas de **detecção de rede no contexto TCP/IP**.

**Contexto atual:**
No cenário atual, entender e proteger as redes torna-se **imperativo** e é exatamente isso que iremos tratar nas próximas seções.

**Analogia:**
A análise de tráfego é como um **raio-x para as redes**, permitindo-nos compreender e avaliar sua saúde e segurança.

---

### **Ferramentas que Exploraremos**

Ao longo desta aula, examinaremos ferramentas essenciais:

**Comandos Básicos:**
- ipconfig / ifconfig
- ping
- arp
- route

**Ferramentas de Rastreamento:**
- traceroute / tracert
- pathping

**Scanners e Descoberta:**
- IP Scanners
- Service Discovery com Nmap
- netstat
- nslookup

**Análise Avançada:**
- Wireshark (análise de pacotes)

**Objetivo:**
Cada uma dessas ferramentas desvendará camadas do tecido complexo que compõe as redes de comunicação.

---

### **Análise de Pacotes**

Além das ferramentas de reconhecimento e varredura, veremos a **análise de pacotes com Wireshark**, entendendo como essa ferramenta nos permite:
- Observar o fluxo de dados em um nível granular
- Decodificar protocolos
- Identificar anomalias
- Investigar incidentes de segurança

**Meta da Aula:**
Ao final desta aula, teremos um entendimento das ferramentas essenciais de detecção de rede e seremos capazes de aplicar esse conhecimento na prática.

---

## 🔍 Avaliação da Segurança Organizacional

### **O Que é Avaliação de Segurança?**

**Definição:**
A avaliação de segurança refere-se a **processos e ferramentas** que avaliam a superfície de ataque.

**Metodologia:**
Com o conhecimento das **táticas e capacidades do adversário**, você pode avaliar se os pontos na superfície de ataque são vetores de ataque potencialmente vulneráveis.

**Resultado:**
O resultado da avaliação são **recomendações** para:
- Implantar controles de segurança
- Aprimorar controles existentes
- Reconfigurar controles
- Mitigar o risco de vulnerabilidades serem exploradas por agentes de ameaças

---

### **Reconhecimento e Descoberta de Rede**

**Definição:**
O processo de mapeamento da superfície de ataque é conhecido como **reconhecimento e descoberta de rede**.

**Quem Usa:**

**Agentes de Ameaças:**
- Para identificar alvos
- Mapear infraestrutura
- Identificar vulnerabilidades

**Profissionais de Segurança:**
- Sondar e testar próprios sistemas de segurança
- Parte de uma avaliação de segurança
- Monitoramento contínuo

---

### **Descoberta de Topologia (Footprinting)**

**Definição:**
Significa verificar hosts, intervalos de IP e rotas entre redes para mapear a **estrutura da rede de destino**.

**Usos:**

**Construir Banco de Dados de Ativos:**
- Inventariar todos os dispositivos
- Documentar configurações
- Rastrear mudanças

**Identificar Hosts Não Autorizados:**
- Detecção de sistema não autorizado (rogue devices)
- Shadow IT
- Dispositivos IoT não gerenciados

**Identificar Erros de Configuração:**
- Serviços expostos indevidamente
- Portas abertas desnecessariamente
- Configurações inseguras

---

## 🛠️ Ferramentas de Detecção de Rede

### **Ferramentas Integradas**

Tarefas básicas de descoberta de topologia podem ser realizadas usando as **ferramentas de linha de comando integradas** ao Windows e ao Linux.

As ferramentas a seguir relatam a **configuração IP** e testam a **conectividade** no segmento ou sub-rede da rede local.

---

### **1. ipconfig (Windows)**

**Função:**
Mostra a configuração atribuída às **interfaces de rede no Windows**.

**Informações Fornecidas:**

| Informação | Descrição |
|------------|-----------|
| **Endereço MAC** | Endereço de hardware ou controle de acesso à mídia |
| **Endereços IPv4** | Endereço IP versão 4 |
| **Endereços IPv6** | Endereço IP versão 6 |
| **Gateway Padrão** | Roteador para acesso externo |
| **Tipo de Atribuição** | Estático ou DHCP |
| **Servidor DHCP** | Se atribuído por DHCP, mostra endereço do servidor |

---

**Comandos Úteis:**

```cmd
# Exibir configuração básica
ipconfig

# Exibir todas as configurações detalhadas
ipconfig /all

# Renovar endereço DHCP
ipconfig /renew

# Liberar endereço DHCP
ipconfig /release

# Limpar cache DNS
ipconfig /flushdns

# Exibir cache DNS
ipconfig /displaydns
```

---

**Exemplo de Saída:**

```
Adaptador Ethernet Local:

   Sufixo DNS específico de conexão . . . . . : empresa.local
   Endereço IPv4. . . . . . . . . . . . . . . : 192.168.1.100
   Máscara de Sub-rede . . . . . . . . . . . : 255.255.255.0
   Gateway Padrão. . . . . . . . . . . . . . : 192.168.1.1
```

---

### **2. ifconfig (Linux)**

**Função:**
Mostra a configuração atribuída às **interfaces de rede no Linux**.

**Nota:**
Comando tradicional, sendo substituído por `ip` em distribuições modernas.

---

**Comandos Úteis:**

```bash
# Exibir todas as interfaces
ifconfig

# Exibir interface específica
ifconfig eth0

# Ativar interface
sudo ifconfig eth0 up

# Desativar interface
sudo ifconfig eth0 down

# Atribuir endereço IP manualmente
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0

# Comando moderno equivalente
ip addr show
ip a
```

---

**Exemplo de Saída:**

```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fe4e:66a1  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:4e:66:a1  txqueuelen 1000  (Ethernet)
```

---

### **3. ping**

**Função:**
Investiga um host em um determinado **endereço IP ou nome de host** usando o Internet Control Message Protocol (ICMP).

**Objetivo:**
- Verificar conectividade
- Testar latência
- Identificar hosts ativos

---

**Uso em Scripts:**

Você pode usar o ping com um **script simples** para realizar uma varredura de todos os endereços IP em uma sub-rede.

**Exemplo de Script (Bash):**
```bash
#!/bin/bash
for ip in 192.168.1.{1..254}; do
    ping -c 1 -W 1 $ip > /dev/null && echo "$ip está ativo"
done
```

---

**Comandos Úteis:**

```bash
# Ping básico (Windows - contínuo)
ping 192.168.1.1

# Ping básico (Linux - 4 pacotes)
ping -c 4 192.168.1.1

# Ping com contagem específica (Windows)
ping -n 10 192.168.1.1

# Ping com tamanho de pacote específico
ping -l 1000 192.168.1.1    # Windows
ping -s 1000 192.168.1.1    # Linux

# Ping flood (teste de stress - requer privilégios)
sudo ping -f 192.168.1.1

# Ping com timeout
ping -w 2000 192.168.1.1    # Windows (ms)
ping -W 2 192.168.1.1       # Linux (s)
```

---

**Interpretação de Resultados:**

```
Resposta de 192.168.1.1: bytes=32 tempo=15ms TTL=64
```

| Métrica | Significado |
|---------|-------------|
| **bytes** | Tamanho do pacote ICMP |
| **tempo** | Latência (RTT - Round Trip Time) |
| **TTL** | Time To Live - saltos restantes |

**Análise de TTL:**
- TTL = 64: Provável Linux/Unix
- TTL = 128: Provável Windows
- TTL = 255: Provável equipamento de rede (Cisco)

---

### **4. arp**

**Função:**
Exibe o cache do **protocolo de resolução de endereço (ARP)** da máquina local.

**O Que Mostra:**
O cache ARP mostra o **endereço MAC** da interface associado a cada endereço IP com o qual o host local se comunicou recentemente.

---

**Utilidade em Segurança:**

Pode ser útil se você estiver investigando uma suspeita de ataque de **falsificação ARP (ARP spoofing)**.

**Exemplo de Ataque:**
Um sinal de ataque **man-in-the-middle** é quando o endereço MAC do IP do gateway padrão listado no cache **não é o endereço MAC do roteador legítimo**.

---

**Comandos Úteis:**

```cmd
# Exibir cache ARP (Windows/Linux)
arp -a

# Adicionar entrada estática ARP
arp -s 192.168.1.1 00-11-22-33-44-55

# Deletar entrada ARP
arp -d 192.168.1.1

# Limpar todo cache ARP (Windows - requer admin)
netsh interface ip delete arpcache

# Limpar todo cache ARP (Linux)
sudo ip -s -s neigh flush all
```

---

**Exemplo de Saída:**

```
Interface: 192.168.1.100 --- 0x2
  Endereço IP       Endereço Físico     Tipo
  192.168.1.1       00-50-56-c0-00-08   dinâmico
  192.168.1.254     00-50-56-ea-5e-7a   dinâmico
```

---

**Detecção de ARP Spoofing:**

**Sinais de alerta:**
1. Múltiplos IPs com o mesmo MAC
2. MAC do gateway mudou inesperadamente
3. Entradas ARP duplicadas

**Verificação:**
```bash
# Comparar MAC real do gateway
ping -c 1 192.168.1.1
arp -a | grep 192.168.1.1

# Comparar com informação do switch
# MAC deve corresponder
```

---

## 🗺️ Configuração de Rotas

As ferramentas a seguir podem ser usadas para testar a **configuração de roteamento** e a **conectividade com hosts e redes remotas**.

---

### **1. route**

**Função:**
Visualize e configure a **tabela de roteamento local** do host.

**Uso Típico:**
A maioria dos sistemas finais usa uma **rota padrão** para encaminhar todo o tráfego para redes remotas através de um roteador gateway.

**Segurança:**
Se o host **não for um roteador**, entradas adicionais na tabela de roteamento poderão ser **suspeitas**.

---

**Comandos Úteis:**

```cmd
# Exibir tabela de roteamento (Windows)
route print

# Exibir tabela de roteamento (Linux)
route -n
ip route show

# Adicionar rota estática (Windows)
route add 10.0.0.0 mask 255.0.0.0 192.168.1.1

# Adicionar rota estática (Linux)
sudo ip route add 10.0.0.0/8 via 192.168.1.1

# Deletar rota
route delete 10.0.0.0
sudo ip route del 10.0.0.0/8

# Tornar rota persistente (Windows)
route -p add 10.0.0.0 mask 255.0.0.0 192.168.1.1
```

---

**Exemplo de Saída:**

```
Tabela de Roteamento IPv4
===========================================================================
Rotas Ativas:
Destino de rede   Máscara de rede    Gateway       Interface       Métrica
          0.0.0.0          0.0.0.0  192.168.1.1  192.168.1.100         25
        127.0.0.0        255.0.0.0   No Link      127.0.0.1            331
```

---

**Análise de Segurança:**

**Rotas Suspeitas:**
- Rotas para redes privadas que não deveriam ser acessíveis
- Múltiplas rotas padrão
- Rotas adicionadas sem autorização
- Gateway apontando para IP desconhecido

---

### **2. tracert (Windows)**

**Função:**
Usa testes **ICMP** para relatar o **tempo de ida e volta (RTT)** para saltos entre o host local e um host em uma rede remota.

**Versão:**
tracert é a versão **Windows** da ferramenta.

---

**Comandos Úteis:**

```cmd
# Traceroute básico
tracert google.com

# Traceroute com máximo de saltos
tracert -h 15 google.com

# Traceroute sem resolução de nomes (mais rápido)
tracert -d google.com

# Traceroute com timeout personalizado
tracert -w 1000 google.com
```

---

**Exemplo de Saída:**

```
Rastreando a rota para google.com [142.250.185.46]
com no máximo 30 saltos:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2     5 ms     5 ms     5 ms  10.0.0.1
  3    10 ms    10 ms    11 ms  172.16.0.1
  4    15 ms    14 ms    15 ms  142.250.185.46

Rastreamento concluído.
```

---

### **3. traceroute (Linux)**

**Função:**
Realiza **descoberta de rotas** a partir de um host Linux.

**Diferença:**
traceroute usa testes **UDP** em vez de ICMP, por padrão.

---

**Comandos Úteis:**

```bash
# Traceroute básico
traceroute google.com

# Traceroute usando ICMP (como Windows)
traceroute -I google.com

# Traceroute usando TCP
traceroute -T -p 80 google.com

# Traceroute com número máximo de saltos
traceroute -m 15 google.com

# Traceroute sem resolução de nomes
traceroute -n google.com

# Traceroute com pacotes maiores
traceroute google.com 1000
```

---

**Protocolos:**

| Opção | Protocolo | Uso |
|-------|-----------|-----|
| **-I** | ICMP | Similar ao Windows |
| **-T** | TCP | Bypass de alguns firewalls |
| **-U** | UDP (padrão) | Comportamento padrão |

---

### **4. pathping (Windows) / mtr (Linux)**

**Função:**
Fornece **estatísticas de latência e perda de pacotes** ao longo de uma rota durante um período de medição mais longo.

**Versões:**
- pathping: Ferramenta do MS-Windows
- mtr: Equivalente no Linux

---

**Comandos Úteis:**

```cmd
# PathPing (Windows)
pathping google.com

# PathPing com duração específica
pathping -q 100 google.com

# MTR (Linux) - interativo
mtr google.com

# MTR - modo relatório
mtr -r -c 100 google.com

# MTR - salvar em arquivo
mtr -r -c 100 google.com > report.txt

# MTR - sem resolução DNS
mtr -n google.com
```

---

**Análise de Segurança:**

**Indicadores de Problemas:**

**Alta latência no gateway padrão:**
- Comparado com baseline
- Pode indicar ataque **man-in-the-middle**

**Alta latência em outros saltos:**
- Pode ser sinal de **negação de serviço**
- Ou simplesmente indicar **congestionamento na rede**

**Perda de pacotes:**
- Pode indicar problemas de conectividade
- Ou ataque de DoS

---

**Exemplo de Análise:**

```
Salto 1 (Gateway): 200ms (baseline: 2ms) → SUSPEITO
Salto 2: 15ms
Salto 3: 20ms
Salto 4: 25ms
```

**Conclusão:** Gateway com latência anormal pode indicar comprometimento.

---

## 🔍 Scanners IP e Nmap

### **Limitações de Ferramentas Básicas**

**Problemas:**
A varredura de uma rede usando ferramentas como ping:
- Consome tempo
- Não é confiável (ICMP pode estar bloqueado)
- Não retorna resultados detalhados

**Solução:**
A maior parte da descoberta de topologia é realizada usando uma **ferramenta de scanner IP dedicada**.

---

### **Scanner IP**

**Função:**
Um scanner IP realiza:
- **Descoberta de hosts:** Identificar hosts ativos
- **Mapeamento de conexões:** Como os hosts estão conectados em uma rede

---

### **Ferramentas Corporativas**

**Para auditoria:**
Existem suítes corporativas, como os produtos **System Center da Microsoft**.

**Capacidades:**
Esses conjuntos podem:
- Receber credenciais para realizar varreduras autorizadas
- Obter informações detalhadas do host
- Usar protocolos de gerenciamento como **SNMP (Simple Network Management Protocol)**

---

### **Nmap Security Scanner**

**O Que É:**
O **Nmap Security Scanner** (nmap.org) é um dos scanners IP de código aberto mais populares.

**Capacidades:**
- Pode usar diversos métodos de descoberta de host
- Alguns métodos podem operar **furtivamente**
- Servir para derrotar mecanismos de segurança:
  - Firewalls
  - Detecção de intrusões

---

**Disponibilidade:**
- Software de **código aberto**
- Pacotes para a maioria das versões de:
  - Windows
  - Linux
  - macOS

**Interfaces:**
- Pode ser operado com **linha de comando**
- Via **GUI (Zenmap)**

---

### **Métodos de Descoberta de Host**

**Varreduras Básicas:**

```bash
# Ping scan (descobrir hosts ativos)
nmap -sn 192.168.1.0/24

# Scan de host específico
nmap 192.168.1.100

# Scan de range de IPs
nmap 192.168.1.1-254

# Scan de múltiplos hosts
nmap 192.168.1.1 192.168.1.100 192.168.1.200

# Scan a partir de arquivo
nmap -iL hosts.txt
```

---

**Técnicas de Scan:**

```bash
# TCP SYN scan (padrão com privilégios)
nmap -sS 192.168.1.100

# TCP Connect scan (sem privilégios)
nmap -sT 192.168.1.100

# UDP scan
nmap -sU 192.168.1.100

# Scan combinado TCP + UDP
nmap -sS -sU 192.168.1.100
```

---

**Detecção de Sistema Operacional:**

```bash
# Detecção de OS
nmap -O 192.168.1.100

# Detecção agressiva de OS
nmap -O --osscan-guess 192.168.1.100

# Scan agressivo (OS + versão + scripts + traceroute)
nmap -A 192.168.1.100
```

---

**Varredura de Portas:**

```bash
# Scan de portas específicas
nmap -p 80,443,22 192.168.1.100

# Scan de range de portas
nmap -p 1-1000 192.168.1.100

# Scan de todas as portas (1-65535)
nmap -p- 192.168.1.100

# Top 100 portas mais comuns
nmap --top-ports 100 192.168.1.100

# Portas TCP e UDP específicas
nmap -p T:80,443,U:53,161 192.168.1.100
```

---

**Timing e Performance:**

```bash
# Templates de timing (-T0 a -T5)
nmap -T4 192.168.1.0/24

# -T0: Paranoid (muito lento, furtivo)
# -T1: Sneaky (lento, furtivo)
# -T2: Polite (mais lento, menos uso de banda)
# -T3: Normal (padrão)
# -T4: Aggressive (rápido)
# -T5: Insane (muito rápido, pode perder dados)

# Scan rápido (top 100 portas)
nmap -F 192.168.1.100

# Scan paralelo
nmap --min-parallelism 100 192.168.1.0/24
```

---

**Evasão e Furtividade:**

```bash
# Fragmentação de pacotes
nmap -f 192.168.1.100

# Usar decoys (múltiplos IPs fonte)
nmap -D RND:10 192.168.1.100

# Spoof de endereço MAC
nmap --spoof-mac Dell 192.168.1.100

# Randomizar ordem de hosts
nmap --randomize-hosts 192.168.1.0/24

# Scan através de proxy
nmap --proxies http://proxy:8080 192.168.1.100
```

---

## 🔬 Descoberta de Serviço e Nmap

**Contexto:**
Tendo identificado **hosts IP ativos** na rede e obtido uma ideia da **topologia da rede**, o próximo passo no reconhecimento é descobrir:

### **Objetivos da Descoberta de Serviço**

1. **Sistemas Operacionais em uso**
2. **Serviços de rede** que cada host está executando
3. **Software aplicativo** que sustenta esses serviços (se possível)

**Processo:**
Este processo é descrito como **descoberta de serviço**.

---

### **Uso Defensivo**

A descoberta de serviços também pode ser usada **defensivamente**:
- Investigar possíveis sistemas não autorizados
- Identificar presença de portas de serviços de rede não autorizadas

---

### **Descoberta de Serviço com Nmap**

**Processo:**
Quando o Nmap conclui uma varredura de descoberta de host, ele reportará o **estado de cada porta** varrida para cada endereço IP no escopo.

**Próximo Passo:**
Neste ponto, você pode executar **verificações adicionais de descoberta de serviço** em um ou mais endereços IP ativos.

---

### **Principais Opções para Descoberta de Serviço**

#### **1. TCP SYN (-sS)**

**Descrição:**
Esta é uma técnica rápida também conhecida como **varredura semiaberta** (half-open scan).

**Como Funciona:**
- O host de varredura **solicita uma conexão sem reconhecê-la**
- Envia SYN
- Aguarda SYN-ACK (porta aberta) ou RST (porta fechada)
- **Não completa** o three-way handshake

**Benefício:**
- Mais furtivo que TCP Connect
- Não registra conexão completa nos logs

**A resposta do alvo ao pacote SYN identifica o estado da porta:**

| Resposta | Estado da Porta |
|----------|-----------------|
| **SYN-ACK** | Aberta |
| **RST** | Fechada |
| **Nenhuma resposta** | Filtrada (firewall) |

---

**Comando:**
```bash
nmap -sS 192.168.1.100
```

---

#### **2. Varreduras UDP (-sU)**

**Descrição:**
Verifica **portas UDP**.

**Desafio:**
Como UDP não usa ACKs, o Nmap precisa:
- Esperar por uma resposta
- Ou tempo limite (timeout) para determinar o estado da porta

**Consequência:**
Varredura UDP pode **demorar muito**.

**Combinação:**
Uma varredura UDP pode ser **combinada com uma varredura TCP**.

---

**Estados de Porta UDP:**

| Resposta | Estado |
|----------|--------|
| **UDP response** | Aberta |
| **ICMP Port Unreachable** | Fechada |
| **Nenhuma resposta** | Aberta\|Filtrada |

---

**Comandos:**
```bash
# Scan UDP apenas
nmap -sU 192.168.1.100

# Scan combinado TCP + UDP
nmap -sS -sU -p T:80,443,U:53,161 192.168.1.100

# Top portas UDP
nmap -sU --top-ports 20 192.168.1.100
```

---

#### **3. Intervalo de Portas (-p)**

**Padrão:**
Por padrão, o Nmap verifica **1.000 portas comumente usadas**, conforme listado em seu arquivo de configuração.

**Personalização:**
Use o argumento **-p** para especificar um intervalo de portas.

---

**Exemplos:**
```bash
# Portas específicas
nmap -p 22,80,443 192.168.1.100

# Range de portas
nmap -p 1-1000 192.168.1.100

# Todas as portas
nmap -p- 192.168.1.100

# Top portas mais comuns
nmap --top-ports 100 192.168.1.100

# Portas TCP e UDP separadamente
nmap -p T:80,443,U:53,161 192.168.1.100
```

---

### **Detecção de Versão de Serviços**

**Objetivo:**
Identificar não apenas que serviço está rodando, mas sua **versão específica**.

**Importância:**
Versões específicas podem ter vulnerabilidades conhecidas (CVEs).

**Comando:**
```bash
# Detecção de versão
nmap -sV 192.168.1.100

# Detecção intensiva de versão
nmap -sV --version-intensity 9 192.168.1.100

# Detecção mais leve
nmap -sV --version-intensity 0 192.168.1.100
```

---

**Exemplo de Saída:**

```
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.4 (protocol 2.0)
80/tcp  open  http    Apache httpd 2.4.6 ((CentOS))
443/tcp open  ssl/http Apache httpd 2.4.6 ((CentOS))
```

---

### **Nmap Scripting Engine (NSE)**

**O Que É:**
Conjunto de scripts que automatizam tarefas:
- Descoberta avançada
- Detecção de vulnerabilidades
- Exploração

**Uso:**
```bash
# Usar scripts padrão
nmap -sC 192.168.1.100

# Script específico
nmap --script http-title 192.168.1.100

# Categoria de scripts
nmap --script vuln 192.168.1.100

# Múltiplos scripts
nmap --script "http-*" 192.168.1.100

# Argumentos para scripts
nmap --script http-brute --script-args userdb=users.txt 192.168.1.100
```

---

**Categorias de Scripts:**

| Categoria | Descrição |
|-----------|-----------|
| **auth** | Autenticação |
| **broadcast** | Descoberta por broadcast |
| **brute** | Força bruta |
| **default** | Scripts padrão |
| **discovery** | Descoberta avançada |
| **dos** | Denial of Service |
| **exploit** | Exploração |
| **fuzzer** | Fuzzing |
| **intrusive** | Intrusivos |
| **malware** | Detecção de malware |
| **safe** | Seguros |
| **version** | Detecção de versão |
| **vuln** | Vulnerabilidades |

---

## 🌐 netstat e nslookup

Tarefas básicas de descoberta de serviços também podem ser executadas usando **ferramentas integradas** aos sistemas operacionais Windows e Linux.

---

### **1. netstat**

**Função:**
Mostra o estado das **portas TCP/UDP** na máquina local.

**Disponibilidade:**
O mesmo comando é usado no **Windows e no Linux**, embora com sintaxe de opções diferentes.

---

**Usos em Segurança:**

**Verificar Configurações Incorretas:**
- Host executando servidor web ou FTP não autorizado
- Usuário instalou serviço sem autorização

**Identificar Conexões Suspeitas:**
- Conexões remotas com serviços no host local
- Conexões do host para endereços IP remotos suspeitos

**Identificar Malware:**
Se você estiver tentando identificar malware, a saída mais útil do netstat é mostrar **qual processo está escutando em quais portas**.

---

**Comandos Úteis (Windows):**

```cmd
# Mostrar todas as conexões e portas listening
netstat -a

# Mostrar estatísticas por protocolo
netstat -s

# Mostrar PID dos processos
netstat -o

# Mostrar executável associado (requer admin)
netstat -b

# Atualizar continuamente
netstat -a 5

# Combinação útil para segurança
netstat -ano
netstat -anb
```

---

**Comandos Úteis (Linux):**

```bash
# Todas as conexões
netstat -a

# Apenas listening
netstat -l

# TCP apenas
netstat -t

# UDP apenas
netstat -u

# Com PIDs e nomes de programas
netstat -p

# Sem resolução de nomes (mais rápido)
netstat -n

# Combinação útil
netstat -tulpn

# Alternativa moderna
ss -tulpn
```

---

**Exemplo de Saída:**

```
Proto  Local Address          Foreign Address        State       PID/Program
tcp    0.0.0.0:22            0.0.0.0:*              LISTEN      1234/sshd
tcp    192.168.1.100:443     93.184.216.34:45678    ESTABLISHED 5678/nginx
tcp    192.168.1.100:3389    192.168.1.50:51234     ESTABLISHED 9012/rdpclip
```

---

**Análise de Segurança:**

**Portas Suspeitas:**
- Portas de backdoor conhecidas (31337, 12345)
- Serviços não autorizados
- Conexões para IPs desconhecidos

**Investigação:**
1. Identificar processo (PID)
2. Verificar executável
3. Validar se é legítimo
4. Investigar conexões estabelecidas

---

### **2. nslookup (Windows) / dig (Linux)**

**Função:**
Consulta **registros de nomes** para um determinado domínio usando um **DNS resolvedor específico**.

---

**Uso em Segurança:**

**Testar Configuração DNS:**
Um invasor pode testar uma rede para descobrir se o serviço DNS está **configurado incorretamente**.

**DNS Mal Configurado:**
Pode permitir uma **transferência de zona (zone transfer)**, o que dará ao invasor:
- Registros completos de cada host no domínio
- Revelando muito sobre a forma como a rede está configurada

---

**nslookup (Windows):**

```cmd
# Consulta básica
nslookup google.com

# Especificar servidor DNS
nslookup google.com 8.8.8.8

# Consulta de tipo específico
nslookup -type=MX google.com

# Consulta reversa
nslookup 8.8.8.8

# Modo interativo
nslookup
> server 8.8.8.8
> set type=ANY
> google.com
> exit

# Tentativa de zone transfer
nslookup
> server dns.example.com
> ls -d example.com
```

---

**dig (Linux):**

```bash
# Consulta básica
dig google.com

# Resposta curta
dig google.com +short

# Especificar servidor DNS
dig @8.8.8.8 google.com

# Consulta de tipo específico
dig MX google.com
dig NS google.com
dig TXT google.com

# Todos os registros
dig ANY google.com

# Consulta reversa
dig -x 8.8.8.8

# Trace completo da resolução
dig +trace google.com

# Tentativa de zone transfer
dig @ns1.example.com example.com AXFR
```

---

**Tipos de Registros DNS:**

| Tipo | Descrição | Uso |
|------|-----------|-----|
| **A** | IPv4 address | Resolução de nome para IP |
| **AAAA** | IPv6 address | Resolução de nome para IPv6 |
| **MX** | Mail exchange | Servidores de e-mail |
| **NS** | Name server | Servidores DNS autoritativos |
| **CNAME** | Canonical name | Alias de domínio |
| **TXT** | Text | Informações variadas, SPF, DKIM |
| **SOA** | Start of authority | Informações sobre zona |
| **PTR** | Pointer | Resolução reversa |

---

## 📦 Análise de Pacotes e Wireshark

### **Analisador de Protocolo (Packet Analyzer)**

**Definição:**
Um analisador de protocolo (ou analisador de pacotes) funciona em conjunto com um **sniffer** para realizar **análise de tráfego**.

**Capacidade:**
Você pode:
- Analisar uma **captura ao vivo**
- Abrir um **arquivo de captura salva** (.pcap)

---

### **Funcionalidades**

**Decodificação:**
Os analisadores de protocolo podem **decodificar um quadro capturado** para revelar seu conteúdo em um **formato legível**.

**Visualizações:**
Você pode optar por visualizar:
- **Resumo do quadro:** Visão geral
- **Visualização mais detalhada:** Informações sobre:
  - Camada OSI
  - Protocolo
  - Função
  - Dados

---

### **Wireshark**

**O Que É:**
**Wireshark** (wireshark.org) é um utilitário **gráfico de captura e análise de pacotes** de código aberto.

**Disponibilidade:**
Pacotes de instalação para a maioria dos sistemas operacionais:
- Windows
- Linux
- macOS

---

### **Interface do Wireshark**

**Escolha de Interface:**
Tendo escolhido a **interface para escutar**, a saída é exibida em uma **visualização de três painéis**.

---

#### **1. Painel da Lista de Pacotes**

**Função:**
Mostra um **resumo de rolagem** dos quadros capturados.

**Informações:**
- Número do pacote
- Timestamp
- Endereço de origem
- Endereço de destino
- Protocolo
- Comprimento
- Informação resumida

---

#### **2. Painel de Detalhes do Pacote**

**Função:**
Mostra **campos expansíveis** no quadro atualmente selecionado na lista de pacotes.

**Camadas Expandíveis:**
- Frame (informações do quadro)
- Ethernet II (camada 2)
- Internet Protocol (camada 3)
- Transmission Control Protocol (camada 4)
- Application Data (camada 7)

---

#### **3. Painel de Bytes de Pacote**

**Função:**
Mostra os **dados brutos** do quadro em:
- **Hexadecimal**
- **ASCII**

**Destaque:**
Ao clicar em um campo no painel de detalhes, os bytes correspondentes são destacados neste painel.

---

### **Capacidades de Análise**

**Protocolos Suportados:**
O Wireshark é capaz de **analisar (interpretar)** os cabeçalhos e payloads de **centenas de protocolos de rede**.

**Exemplos:**
- HTTP, HTTPS
- DNS
- SMTP, POP3, IMAP
- FTP
- SSH, Telnet
- SMB
- ICMP
- ARP
- E muitos outros

---

### **Funcionalidades Principais**

#### **1. Captura de Tráfego**

**Captura ao Vivo:**
```
Capture > Options
Selecionar interface
Start
```

**Opções de Captura:**
- Interface específica
- Filtro de captura (BPF)
- Tamanho máximo de arquivo
- Rotação de arquivos

---

#### **2. Filtros de Exibição**

**Filtros Comuns:**

```
# Filtrar por protocolo
http
dns
ssh
arp

# Filtrar por IP
ip.addr == 192.168.1.100
ip.src == 192.168.1.100
ip.dst == 192.168.1.100

# Filtrar por porta
tcp.port == 80
tcp.dstport == 443

# Combinações (AND/OR)
ip.addr == 192.168.1.100 && tcp.port == 80
http || dns

# Filtrar por substring
http.request.uri contains "login"
frame contains "password"

# Filtrar por flags TCP
tcp.flags.syn == 1
tcp.flags.reset == 1
```

---

#### **3. Seguir Streams**

**TCP Stream:**
```
Clique direito no pacote > Follow > TCP Stream
```

**Uso:**
- Ver conversa completa TCP
- Identificar dados transmitidos
- Reconstruir sessões HTTP

**Outros Streams:**
- UDP Stream
- SSL Stream (se descriptografado)
- HTTP Stream

---

#### **4. Estatísticas**

**Menus de Estatísticas:**

**Statistics > Protocol Hierarchy:**
- Distribuição de protocolos capturados

**Statistics > Conversations:**
- Conversas entre hosts
- Volume de dados

**Statistics > Endpoints:**
- Hosts mais ativos

**Statistics > IO Graphs:**
- Gráficos de tráfego ao longo do tempo

---

### **Casos de Uso em Segurança**

#### **1. Detecção de Varreduras**

**Indicadores:**
- Múltiplas conexões SYN para portas diferentes
- SYN sem ACK subsequente
- Muitas tentativas de conexão em curto período

**Filtro:**
```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

---

#### **2. Detecção de ARP Spoofing**

**Indicadores:**
- Múltiplas respostas ARP para o mesmo IP
- MAC address mudando para o mesmo IP

**Filtro:**
```
arp
```

**Análise:**
Verificar se respostas ARP são consistentes.

---

#### **3. Análise de Credenciais**

**Protocolos Inseguros:**
- HTTP (credenciais em texto claro)
- FTP
- Telnet
- SMTP

**Filtros:**
```
http.request.method == "POST"
ftp.request.command == "PASS"
```

**Ação:**
Seguir stream para ver credenciais.

---

#### **4. Detecção de Exfiltração**

**Indicadores:**
- Transferências grandes de dados
- Conexões para IPs externos suspeitos
- Protocolos incomuns

**Filtros:**
```
ip.dst != 192.168.0.0/16 && tcp
dns && dns.qry.name contains "pastebin"
```

---

#### **5. Análise de Malware**

**Indicadores:**
- Conexões para C2 (Command & Control)
- Tráfego DNS anômalo (DNS tunneling)
- Beaconing (conexões regulares)

**Filtros:**
```
http.request.uri contains "php"
dns.qry.name.len > 50
tcp.stream eq 1
```

---

### **Boas Práticas com Wireshark**

✅ **Usar filtros de captura** para reduzir volume  
✅ **Salvar capturas** para análise posterior  
✅ **Documentar descobertas** com screenshots  
✅ **Comparar com baseline** de tráfego normal  
✅ **Cuidado com privacidade** - capturas podem ter dados sensíveis  
✅ **Descriptografar SSL/TLS** apenas quando autorizado  

---

## 💡 Conclusão

### **Principais Takeaways**

✅ **Ferramentas de linha de comando** são fundamentais para diagnóstico  
✅ **Nmap é poderoso** para descoberta e análise de rede  
✅ **Wireshark permite análise granular** de tráfego  
✅ **Combinação de ferramentas** fornece visão completa  
✅ **Uso defensivo** identifica problemas antes de atacantes  
✅ **Documentação** de topologia é essencial  
✅ **Análise de pacotes** é crucial para investigações  

---

### **Mensagem Final**

Ao encerrarmos esta aula sobre **Análise de Tráfego TCP/IP**, é gratificante refletir sobre os conhecimentos adquiridos:

**Importância:**
Começando pela importância da segurança organizacional em um cenário digital em constante evolução.

**Ferramentas Essenciais:**
Ao longo da aula, buscamos compreender o papel vital de ferramentas como:
- ipconfig, ifconfig
- Ping, Arp
- Route, Traceroute, Tracert, Pathping
- IP Scanners
- Service Discovery com Nmap
- Netstat, Nslookup

**Cada ferramenta:**
Se revelou uma **peça-chave no quebra-cabeça** da análise de tráfego.

**Wireshark:**
Aprofundamos nosso entendimento na análise de pacotes, destacando o poderoso **Wireshark** como uma ferramenta que permite:
- Observar fluxo de dados em nível granular
- Decodificar protocolos
- Identificar anomalias

**Aplicação Prática:**
É importante ressaltar que o conhecimento adquirido hoje não é apenas teórico. Esperamos que tenham conseguido aplicar essas ferramentas e conceitos de forma significativa.

**Futuro:**
Que esta aula tenha sido uma ponte para um **entendimento mais profundo** e para um futuro mais seguro no mundo das redes TCP/IP.

Agradecemos pela participação e parabenizamos por mais uma etapa vencida. **Bom trabalho e sucesso** em suas futuras explorações digitais!

---

## 🎓 Comandos de Referência Rápida

### **Windows**

```cmd
ipconfig /all
ping -n 10 192.168.1.1
arp -a
route print
tracert google.com
pathping google.com
netstat -ano
nslookup google.com
```

### **Linux**

```bash
ifconfig / ip addr
ping -c 4 192.168.1.1
arp -a / ip neigh
route -n / ip route
traceroute google.com
mtr google.com
netstat -tulpn / ss -tulpn
dig google.com
```

### **Nmap**

```bash
nmap -sn 192.168.1.0/24          # Host discovery
nmap -sS -sV 192.168.1.100       # Port + version scan
nmap -A 192.168.1.100            # Aggressive scan
nmap -p- 192.168.1.100           # All ports
nmap --script vuln 192.168.1.100 # Vulnerability scan
```

---

## 🔗 Conceitos Relacionados

- **Network Mapping:** Mapeamento de topologia de rede
- **Asset Discovery:** Descoberta de ativos
- **Vulnerability Assessment:** Avaliação de vulnerabilidades
- **Network Forensics:** Forense de rede
- **Packet Analysis:** Análise de pacotes
- **Network Monitoring:** Monitoramento de rede
- **Intrusion Detection:** Detecção de intrusão

---

## 📚 Glossário de Termos

| Termo | Definição |
|-------|-----------|
| **ICMP** | Internet Control Message Protocol - Protocolo para mensagens de controle |
| **ARP** | Address Resolution Protocol - Resolve IP para MAC |
| **RTT** | Round Trip Time - Tempo de ida e volta |
| **TTL** | Time To Live - Número de saltos permitidos |
| **MAC** | Media Access Control - Endereço físico de hardware |
| **DHCP** | Dynamic Host Configuration Protocol - Atribuição automática de IP |
| **DNS** | Domain Name System - Sistema de nomes de domínio |
| **Sniffer** | Ferramenta de captura de pacotes |
| **PCAP** | Packet Capture - Formato de arquivo de captura |
| **BPF** | Berkeley Packet Filter - Filtro de captura de pacotes |

---

**Autor:** [Seu Nome]  
**Data:** Fevereiro 2025  
**Curso:** Fundamentos de Cibersegurança - Módulo 3 - Aula 4  
**Fonte:** Material baseado em GitBook ESR-1 Fundamental Aula 06
