# 🧪 Laboratório 7 - Ferramentas de Detecção de Rede e Enumeração DNS

## 📋 Informações do Laboratório

**Ambiente:** Kali Linux + Windows Server 2022  
**Objetivo:** Explorar ferramentas de detecção de rede, honeypots e enumeração DNS

---

## 🛠️ Atividade 3.6 – Ferramentas de Detecção de Rede no Kali Linux

### **Objetivo:**
Conhecer os principais comandos de diagnóstico de rede no Linux.

### **📍 Ambiente:**
Kali Linux 

---

### **Passo 1: Tornar-se Super Usuário**

```bash
sudo -i
```

**💡 Explicação:**
- `sudo -i`: Inicia uma shell de root (super usuário)
- Necessário para comandos que requerem privilégios elevados

---

### **Passo 2: Verificar Configuração de Rede**

```bash
ifconfig
```

**💡 Explicação do `ifconfig`:**
Mostra informações detalhadas sobre as interfaces de rede do sistema.

**Saída esperada:**

```
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet "000.00.0.0"  netmask 255.255.0.0  broadcast 000.00.255.255
        
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
```

**🔍 Interfaces identificadas:**

| Interface | Descrição | Uso |
|-----------|-----------|-----|
| **docker0** | Interface virtual do Docker | Rede de containers |
| **eth0** | Interface Ethernet principal | Conexão de rede real |
| **lo** | Interface de loopback | Comunicação local (localhost) |

**📊 Informações importantes:**
- **inet**: Endereço IPv4
- **netmask**: Máscara de sub-rede
- **broadcast**: Endereço de broadcast
- **MTU**: Maximum Transmission Unit (tamanho máximo de pacote)

---

### **Passo 3: Testar Conectividade com Ping**

```bash
ping www.google.com
```

**Para parar:** Pressione `Ctrl + C`

**💡 Explicação do `ping`:**
Envia pacotes ICMP Echo Request para verificar conectividade e medir latência.

**Saída esperada:**

```
PING www.google.com (172.253.63.106) 56(84) bytes of data.
64 bytes from bi-in-f106.1e100.net (172.253.63.106): icmp_seq=1 ttl=109 time=1.42 ms
```

**📊 Análise dos campos:**

| Campo | Significado | Exemplo |
|-------|-------------|---------|
| **bytes** | Tamanho do pacote ICMP | 64 bytes |
| **time** | RTT (Round Trip Time) - latência | 1.42 ms |
| **ttl** | Time To Live - saltos restantes | 109 |
| **icmp_seq** | Número de sequência do pacote | 1 |

**🔍 Identificação de Sistema Operacional pelo TTL:**
- **TTL = 64:** Linux/Unix
- **TTL = 128:** Windows
- **TTL = 255:** Equipamento de rede (Cisco)

---

### **Passo 4: Rastrear Rota com Traceroute**

```bash
traceroute -I grancursos.com.br
```

**💡 Explicação do `traceroute`:**
Mapeia a rota que os pacotes fazem da origem até o destino, mostrando cada salto (hop).

**Parâmetros:**
- `-I`: Usa ICMP em vez de UDP (similar ao Windows)

**Saída esperada:**

```
traceroute to grancursos.com.br (172.67.175.92), 30 hops max, 60 byte packets
 1  244.5.7.59 (244.5.7.59)  2.953 ms  2.920 ms *
 2  240.4.116.42 (240.4.116.42)  0.305 ms  0.299 ms  0.318 ms
 3  242.12.75.131 (242.12.75.131)  1.596 ms  1.589 ms  1.584 ms
 ...
 9  172.67.175.92 (172.67.175.92)  0.901 ms  0.889 ms  0.870 ms
```

**📊 Análise de cada hop:**

**Hop 1-2:** Rede local e gateway  
**Hop 3-5:** Backbone do provedor  
**Hop 6-8:** Infraestrutura Cloudflare  
**Hop 9:** Destino final  

**🔍 Interpretação:**
- **3 valores de tempo:** 3 pacotes enviados por hop
- **Asterisco (*):** Pacote perdido ou sem resposta
- **ms (milissegundos):** Latência até aquele hop

**⚠️ Indicadores de Problemas:**
- Latência alta (>100ms) em hop próximo
- Muitos asteriscos (perda de pacotes)
- Aumento súbito de latência

---

### **Passo 5: Estatísticas de Interface - netstat -i**

```bash
netstat -i
```

**💡 Explicação do `netstat -i`:**
Exibe estatísticas de interface de rede do kernel.

**Saída esperada:**

```
Tabela de Interfaces do Kernel
Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
docker0   1500        0      0      0      0        0      0      0      0 BMU
eth0      9001     8055      0      0      0     9143      0      0      0 BMRU
lo       65536       23      0      0      0       23      0      0      0 LRU
```

**📊 Significado das colunas:**

| Coluna | Descrição | Valores normais |
|--------|-----------|-----------------|
| **Iface** | Nome da interface | eth0, lo, docker0 |
| **MTU** | Maximum Transmission Unit | 1500 (padrão), 9001 (jumbo frames) |
| **RX-OK** | Pacotes recebidos com sucesso | Crescente |
| **RX-ERR** | Erros de recepção | 0 (ideal) |
| **RX-DRP** | Pacotes recebidos descartados | 0 (ideal) |
| **RX-OVR** | Buffer overflow de recepção | 0 (ideal) |
| **TX-OK** | Pacotes transmitidos com sucesso | Crescente |
| **TX-ERR** | Erros de transmissão | 0 (ideal) |
| **TX-DRP** | Pacotes transmitidos descartados | 0 (ideal) |
| **TX-OVR** | Buffer overflow de transmissão | 0 (ideal) |
| **Flg** | Flags da interface | BMRU (detalhado abaixo) |

**🔍 Flags da Interface:**
- **B:** Broadcast (interface suporta broadcast)
- **M:** Multicast (interface suporta multicast)
- **R:** Running (interface está ativa)
- **U:** Up (interface está ligada)
- **L:** Loopback (interface de loopback)

---

### **Passo 6: Visualizar Tabela de Roteamento**

```bash
netstat -rn
```

**💡 Explicação do `netstat -rn`:**
Exibe a tabela de roteamento IP do kernel.

**Parâmetros:**
- `-r`: Routing table (tabela de roteamento)
- `-n`: Numeric (não resolve nomes, mais rápido)

**Saída esperada:**

```
Tabela de Roteamento IP do Kernel
Destino         Roteador        MáscaraGen.    Opções   MSS Janela  irtt Iface
0.0.0.0         192.168.98.1    0.0.0.0         UG        0 0          0 eth0
172.17.0.0      0.0.0.0         255.255.0.0     U         0 0          0 docker0
192.168.98.0    0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

**📊 Análise das rotas:**

| Destino | Roteador | Máscara | Significado |
|---------|----------|---------|-------------|
| **0.0.0.0** | 192.168.98.1 | 0.0.0.0 | Rota padrão (default gateway) |
| **172.17.0.0** | 0.0.0.0 | 255.255.0.0 | Rede Docker (diretamente conectada) |
| **192.168.98.0** | 0.0.0.0 | 255.255.255.0 | Rede local (diretamente conectada) |

**🔍 Flags de Roteamento:**
- **U:** Up (rota ativa)
- **G:** Gateway (usa um roteador)

**💡 Termos importantes:**
- **Destino 0.0.0.0:** "Qualquer rede" - rota padrão
- **Roteador 0.0.0.0:** Rede diretamente conectada (sem gateway intermediário)
- **Default Gateway:** Roteador usado para alcançar redes externas

---

### **Passo 7: Estatísticas de Protocolos**

```bash
netstat -s
```

**💡 Explicação do `netstat -s`:**
Exibe estatísticas detalhadas por protocolo de rede.

**Saída resumida (principais seções):**

```
Ip:
    Forwarding: 1
    9136 total packets received
    0 incoming packets discarded
    9132 incoming packets delivered
    
Icmp:
    29 ICMP messages received
    56 ICMP messages sent
    
Tcp:
    68 active connection openings
    3 passive connection openings
    1 connections established
    
Udp:
    43 packets received
    48 packets sent
```

**📊 Protocolos e Estatísticas:**

### **IP (Internet Protocol)**
- **Forwarding:** Roteamento habilitado (1) ou desabilitado (0)
- **Total packets received:** Total de pacotes IP recebidos
- **Incoming packets discarded:** Pacotes descartados
- **Requests sent out:** Solicitações enviadas

### **ICMP (Internet Control Message Protocol)**
- **Messages received/sent:** Mensagens ICMP (ping, traceroute)
- **Echo requests/replies:** Pings enviados/recebidos

**💡 Tipos de mensagem ICMP:**
- **Type 0:** Echo Reply (resposta de ping)
- **Type 3:** Destination Unreachable (destino inalcançável)
- **Type 8:** Echo Request (solicitação de ping)
- **Type 11:** Time Exceeded (tempo excedido - usado no traceroute)

### **TCP (Transmission Control Protocol)**
- **Active connection openings:** Conexões iniciadas localmente
- **Passive connection openings:** Conexões aceitas de fora
- **Segments received/sent:** Pacotes TCP
- **Segments retransmitted:** Retransmissões (indicativo de problemas de rede)

### **UDP (User Datagram Protocol)**
- **Packets received/sent:** Pacotes UDP
- **Packets to unknown port:** Pacotes para portas fechadas

---

### **Passo 8: Conexões Ativas e Portas Abertas** 

```bash
netstat -anptu
```

**💡 Explicação do `netstat -anptu`:**
Mostra conexões de rede ativas e processos associados.

**Parâmetros:**
- `-a`: All (todas as conexões e portas listening)
- `-n`: Numeric (endereços numéricos, não resolve nomes)
- `-p`: Program (mostra PID e nome do programa)
- `-t`: TCP (conexões TCP)
- `-u`: UDP (conexões UDP)

**Saída esperada:**

```
Proto  Recv-Q Send-Q Endereço Local          Endereço Remoto         Estado      PID/Program
tcp        0      0 127.0.0.1:36367         0.0.0.0:*               OUÇA       576/containerd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               OUÇA       618/sshd
tcp6       0      0 :::22                   :::*                    OUÇA       618/sshd
tcp6       0      0 :::3389                 :::*                    OUÇA       641/xrdp
tcp6       0      0 192.168.98.40:3389      192.168.98.201:49732    ESTABELECIDA 2206/xrdp
udp        0      0 0.0.0.0:68              0.0.0.0:*                           441/dhclient
```

**📊 Análise das colunas:**

| Coluna | Descrição | Exemplo |
|--------|-----------|---------|
| **Proto** | Protocolo | tcp, tcp6, udp |
| **Recv-Q** | Fila de recebimento | 0 (ideal) |
| **Send-Q** | Fila de envio | 0 (ideal) |
| **Endereço Local** | IP:Porta local | 0.0.0.0:22, 192.168.98.40:3389 |
| **Endereço Remoto** | IP:Porta remoto | 192.168.98.201:49732 |
| **Estado** | Estado da conexão TCP | OUÇA, ESTABELECIDA |
| **PID/Program** | ID do processo / Nome | 618/sshd |

**🔍 Estados de Conexão TCP:**
- **OUÇA (LISTEN):** Aguardando conexões (servidor)
- **ESTABELECIDA (ESTABLISHED):** Conexão ativa
- **TIME_WAIT:** Aguardando fechamento completo
- **CLOSE_WAIT:** Aguardando fechamento da aplicação

**💡 Endereços especiais:**
- **0.0.0.0:** Escutando em todas as interfaces
- **127.0.0.1:** Localhost (apenas acesso local)
- **:::** Escutando em todas as interfaces IPv6

**🔍 Portas importantes identificadas:**
- **22:** SSH (Secure Shell)
- **68:** DHCP Client
- **3389:** RDP (Remote Desktop Protocol)
- **36367:** containerd (Docker)

---

### **Passo 9: Fechar Terminal**

```bash
exit
```

---

## 🍯 Atividade 3.7 – Criando Honeypot com PentBox

### **Objetivo:**
Configurar e testar um honeypot básico usando PentBox.

### **📍 Ambientes:**
- Kali Linux - Servidor Honeypot
- Windows Server 2022 - Cliente

---

### **🔍 O que é um Honeypot?**

**Definição:**
Sistema ou serviço intencionalmente vulnerável usado para atrair e estudar atacantes.

**Objetivos:**
- 🎯 Desviar atenção de sistemas reais
- 🔍 Coletar informações sobre TTPs (Tactics, Techniques, Procedures) de atacantes
- ⚠️ Detectar tentativas de intrusão precocemente
- 📊 Gerar inteligência de ameaças

**Tipos:**
- **Baixa interação:** Emula serviços (mais seguro, menos informação)
- **Alta interação:** Sistema real (mais arriscado, mais informação)

---

### **Passo 1: Tornar-se Super Usuário**

```bash
sudo -i
```

### **Passo 2: Verificar IP do Kali**

```bash
ifconfig
```

**💡 Por quê?**
Precisamos do IP para que o Windows Server saiba onde tentar acessar o honeypot.

---

### **Passo 3: Iniciar PentBox**

```bash
cd "/diretório-do-pentbox/pentbox/pentbox-1.8"
./pentbox.rb
```

**💡 Sobre o PentBox:**
Suite de ferramentas de segurança em Ruby que inclui:
- Testes de DoS
- Scanner de portas
- **Honeypot** ← Usaremos este
- Fuzzer
- DNS gathering

---

### **Passo 4: Selecionar Network Tools**

```
   -> 2
```

**Menu exibido:**
```
1- Net DoS Tester
2- TCP port scanner
3- Honeypot          ← Selecionar esta
4- Fuzzer
5- DNS and host gathering
6- MAC address geolocation
```

---

### **Passo 5: Selecionar Honeypot**

```
   -> 3
```

**Menu exibido:**
```
1- Fast Auto Configuration      ← Configuração rápida
2- Manual Configuration          ← Configuração avançada
```

---

### **Passo 6: Configuração Rápida**

```
   -> 1
```

**Resultado:**
```
HONEYPOT ACTIVATED ON PORT 80 (2024-01-24 16:52:52 -0500)
```

**💡 O que aconteceu:**
- Honeypot configurado automaticamente na **porta 80** (HTTP)
- Aguardando tentativas de acesso
- Qualquer conexão será registrada

**🔍 Por que porta 80?**
- Porta padrão do HTTP (web)
- Muito alvo de ataques automatizados
- Fácil de testar com navegador

---

### **Passo 7: Iniciar Windows Server 2022**

**Da máquina Landing:**
- Minimizar o Kali
- Conectar ao Windows Server 2022

---

### **Passo 8: Abrir Microsoft Edge**

No Windows Server 2022:
1. Clicar na barra de tarefas
2. Abrir **Microsoft Edge**

---

### **Passo 9: Acessar o Honeypot**

**No navegador, digitar:**
```
http://ip-do-honey-pot
```

**Resultado esperado:**
Página de erro com mensagem do honeypot:

```
Access denied
HTTP Referrer login failed
IP Address login failed
2025-09-06 11:44:50 -0300
```

**💡 Explicação:**
- O honeypot retorna uma página falsa
- Registra a tentativa de acesso
- Data/hora da tentativa é exibida

---

### **Passo 10: Verificar Logs no Kali** 

**Voltar ao Terminal do Kali**

**Log exibido:**

```
INTRUSION ATTEMPT DETECTED! from 192.168.98.30:49736 (2025-09-06 11:45:58 -0300)
-----------------------------
GET / HTTP/1.1
Host: 192.168.98.40
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36...
Accept: text/html,application/xhtml+xml,application/xml;q=0.9...
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
```

**📊 Informações capturadas:**

| Campo | Valor | Significado |
|-------|-------|-------------|
| **IP de origem** | 192.168.98.30 | Windows Server atacante |
| **Porta origem** | 49736 | Porta aleatória do cliente |
| **Timestamp** | 2025-09-06 11:45:58 | Data/hora da tentativa |
| **Método HTTP** | GET | Tipo de requisição |
| **Host** | 192.168.98.40 | IP do honeypot |
| **User-Agent** | Mozilla/5.0... | Navegador usado (Edge) |

**🔍 Análise de Segurança:**
- **User-Agent:** Identifica o navegador/OS do atacante
- **Accept-Language:** Idioma preferencial (en-US = inglês americano)
- **Connection:** Tipo de conexão (keep-alive)

---

### **Passo 11: Encerrar**

1. Fechar Microsoft Edge no Windows Server
2. Desconectar RDP do Windows Server
3. No Kali: `Ctrl+C` para parar o honeypot
4. Fechar Terminal

---

## 🔍 Atividade 3.8 – Enumeração DNS com `host`

### **Objetivo:**
Enumerar informações DNS usando a ferramenta `host`.

### **📍 Ambiente:**
Kali Linux

---

### **🌐 O que é DNS?**

**DNS (Domain Name System):**
Sistema que traduz nomes de domínio em endereços IP.

**Exemplo:**
```
google.com → 142.250.185.46
```

**Por que enumerar DNS?**
- 🔍 Descobrir infraestrutura de rede
- 📧 Identificar servidores de e-mail
- 🌐 Mapear subdomínios
- 🔐 Avaliar configuração de segurança

---

### **Passo 1: Tornar-se Super Usuário**

```bash
sudo -i
```

---

### **Passo 2: Consulta DNS Completa**

```bash
host grancursos.com.br
```

**Saída esperada:**

```
grancursos.com.br has address 172.67.175.92
grancursos.com.br has address 104.21.35.137
grancursos.com.br has IPv6 address 2606:4700:3034::6815:2389
grancursos.com.br has IPv6 address 2606:4700:3037::ac43:af5c
grancursos.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursos.com.br mail is handled by 1 aspmx.l.google.com.
...
```

**📊 Informações obtidas:**

### **Registros A (IPv4):**
```
172.67.175.92
104.21.35.137
```
- Múltiplos IPs = Balanceamento de carga
- IPs da **Cloudflare** (CDN/Proxy)

### **Registros AAAA (IPv6):**
```
2606:4700:3034::6815:2389
2606:4700:3037::ac43:af5c
```
- Suporte a IPv6
- Também Cloudflare

### **Registros MX (Mail Exchange):**
```
Priority 1: aspmx.l.google.com.
Priority 5: alt1.aspmx.l.google.com.
Priority 5: alt2.aspmx.l.google.com.
Priority 10: alt3.aspmx.l.google.com.
Priority 10: alt4.aspmx.l.google.com.
```

**💡 Prioridade MX:**
- **Menor número = Maior prioridade**
- Servidor com prioridade 1 é tentado primeiro
- Se falhar, tenta prioridade 5, depois 10

**🔍 Observação:**
E-mails gerenciados pelo **Google Workspace** (Gmail corporativo)

### **HTTP Service Bindings:**
```
alpn="h3,h2"
```
- Suporte a **HTTP/3** (h3) e **HTTP/2** (h2)
- Protocolos modernos e rápidos

```
ech=...
```
- **ECH (Encrypted Client Hello):** Maior privacidade TLS

---

### **Passo 3: Consultar Name Servers (NS)**

```bash
host -t ns esr.rnp.br
```

**Saída esperada:**
```
esr.rnp.br has no NS record
```

**💡 Significado:**
O domínio não possui registros NS configurados ou acessíveis publicamente.

**🔍 O que são NS Records?**
- Indicam servidores DNS autoritativos para o domínio
- Essenciais para resolução DNS

---

### **Passo 4: Consultar NS de Outro Domínio**

```bash
host -t ns grancursosonline.com.br
```

**Saída esperada:**
```
grancursosonline.com.br name server rachel.ns.cloudflare.com.
grancursosonline.com.br name server josh.ns.cloudflare.com.
```

**📊 Análise:**
- 2 name servers configurados (redundância)
- Ambos da **Cloudflare**
- DNS gerenciado por CDN

**💡 Por que 2 name servers?**
- **Redundância:** Se um falhar, o outro responde
- **Balanceamento:** Distribui consultas DNS
- **Resiliência:** Maior disponibilidade

---

### **Passo 5: Consultar Servidores de E-mail** 

```bash
host -t mx grancursosonline.com.br
```

**Saída esperada:**
```
grancursosonline.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt1.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 1 aspmx.l.google.com.
```

**📊 Hierarquia de Servidores:**

```
Prioridade 1 (Principal):
  └─ aspmx.l.google.com

Prioridade 5 (Secundários):
  ├─ alt1.aspmx.l.google.com
  └─ alt2.aspmx.l.google.com

Prioridade 10 (Terciários):
  ├─ alt3.aspmx.l.google.com
  └─ alt4.aspmx.l.google.com
```

**💡 Funcionamento:**
1. E-mail tenta ser entregue ao servidor prioridade 1
2. Se falhar, tenta servidores prioridade 5
3. Se falhar, tenta servidores prioridade 10
4. Múltiplos servidores com mesma prioridade = balanceamento

**🔍 Prefixos ASPMX:**
- **aspmx:** Anti-Spam Mail Exchanger (Google)
- **alt:** Alternative (servidores alternativos)

---

### **Passo 6: Fechar Terminal**

```bash
exit
```

---

## 🔎 Atividade 3.9 – Enumeração DNS com `nslookup`

### **Objetivo:**
Enumerar informações DNS usando `nslookup` de forma interativa.

### **📍 Ambiente:**
Kali Linux 

---

### **🔍 O que é nslookup?**

**nslookup (Name Server Lookup):**
Ferramenta interativa para consultar DNS.

**Diferenças do `host`:**
- **Modo interativo:** Permite múltiplas consultas
- **Mais verboso:** Mostra mais detalhes
- **Servidor DNS:** Exibe qual servidor respondeu

---

### **Passo 1: Tornar-se Super Usuário**

```bash
sudo -i
```
---

### **Passo 2: Consulta DNS Básica**

```bash
nslookup grancursosonline.com.br
```

**Saída esperada:**

```
Server:	192.168.98.2
Address:	192.168.98.2#53

Non-authoritative answer:
Name:   grancursosonline.com.br
Address: 104.18.99.225
Address: 104.18.100.225
Address: 2606:4700::6812:63e1
Address: 2606:4700::6812:64e1
```

**📊 Análise da resposta:**

### **Servidor DNS usado:**
```
Server: 192.168.98.2
Address: 192.168.98.2#53
```
- **192.168.98.2:** DNS resolver (provavelmente gateway/roteador)
- **#53:** Porta padrão do DNS

### **Tipo de resposta:**
```
Non-authoritative answer
```

**💡 Autoridade DNS:**
- **Authoritative:** Resposta direta do servidor autoritativo do domínio
- **Non-authoritative:** Resposta de cache ou servidor intermediário

**Quando esperar resposta autoritativa?**
- Consultando diretamente o NS do domínio
- Zone transfers (AXFR)

### **Endereços retornados:**
```
IPv4:
  104.18.99.225
  104.18.100.225

IPv6:
  2606:4700::6812:63e1
  2606:4700::6812:64e1
```

**🔍 Múltiplos IPs:**
- Cloudflare CDN
- Balanceamento de carga
- Alta disponibilidade
- Distribuição geográfica

---

### **Passo 3: Modo Interativo - Name Servers**

```bash
nslookup
> set type=ns
> grancursosonline.com.br
```

**Saída esperada:**

```
Server:	192.168.98.2
Address:	192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br nameserver = dan.ns.cloudflare.com.
grancursosonline.com.br nameserver = rita.ns.cloudflare.com.

Authoritative answers can be found from:
>
```

**💡 Comandos no modo interativo:**
- `set type=ns`: Define tipo de consulta (Name Servers)
- `set type=mx`: Mail servers
- `set type=a`: IPv4
- `set type=aaaa`: IPv6
- `set type=txt`: Registros TXT
- `exit`: Sair do modo interativo

**📊 Name Servers identificados:**
- dan.ns.cloudflare.com
- rita.ns.cloudflare.com

**🔍 Nomes humanizados:**
Cloudflare usa nomes de pessoas para seus name servers (dan, rita, rachel, josh, etc.)

---

### **Passo 4: Consultar Servidores de E-mail**

```bash
> set type=mx
> grancursosonline.com.br
```

**Saída esperada:**

```
Server:	192.168.98.2
Address:	192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br mail exchanger = 1 aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 10 alt3.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 10 alt4.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 5 alt1.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 5 alt2.aspmx.l.google.com.
```

**📊 Estrutura de MX Records:**

| Prioridade | Servidor | Função |
|------------|----------|--------|
| 1 | aspmx.l.google.com | Principal |
| 5 | alt1.aspmx.l.google.com | Secundário 1 |
| 5 | alt2.aspmx.l.google.com | Secundário 2 |
| 10 | alt3.aspmx.l.google.com | Backup 1 |
| 10 | alt4.aspmx.l.google.com | Backup 2 |

**💡 Interpretação de prioridades:**
- Sistema tenta primeiro prioridade **1**
- Se falhar, tenta prioridade **5** (escolhe aleatoriamente entre alt1 e alt2)
- Se ambos falharem, tenta prioridade **10**

---

### **Passo 5: Consultar Registros TXT** 📸

**Sair do modo interativo:** `Ctrl+C`

```bash
nslookup -type=txt grancursosonline.com.br
```

**Saída esperada:**

```
;; Truncated, retrying in TCP mode.
Server:	192.168.98.2
Address:	192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br	text = "google-site-verification=bJj3VTcb9ZUQDOPT5SbS_5nkfsr-Raw9oh8ptw01MRM"
grancursosonline.com.br	text = "google-site-verification=xiBkOcAELpzCJlFjzARMpyCQpajShwRZ0RwuDQY3V2U"
grancursosonline.com.br	text = "atlassian-domain-verification=8xiJYcQ1gnysutOmpxf6x8cvLNZyaARmLpR2YqL3Dz6Stz0PwHXZczMQxR6vF9Vx"
grancursosonline.com.br	text = "v=spf1 include:amazonses.com include:_spf.google.com include:mail.zendesk.com include:302036.spf06.hubspotemail.net include:_spf.salesforce.com ip4:168.245.107.217 ip4:168.245.71.19 ~all"
```

**🔍 O que são registros TXT?**
Registros de texto usados para diversos propósitos: verificações, políticas, configurações.

**📊 Análise dos registros TXT:**

### **1. Google Site Verification**
```
google-site-verification=...
```
- **Propósito:** Verificar propriedade do domínio no Google Search Console
- **Uso:** SEO, Analytics, AdWords

### **2. Atlassian Domain Verification**
```
atlassian-domain-verification=...
```
- **Propósito:** Verificar domínio para produtos Atlassian (Jira, Confluence)
- **Uso:** SSO (Single Sign-On)

### **3. SPF (Sender Policy Framework)**
```
v=spf1 include:amazonses.com include:_spf.google.com ...
```

**💡 O que é SPF?**
Política que especifica quais servidores podem enviar e-mail em nome do domínio.

**Componentes do SPF:**
- `v=spf1`: Versão do SPF
- `include:`: Incluir política de outro domínio
- `ip4:`: Endereços IP autorizados
- `~all`: Soft fail (aceitar mas marcar como suspeito)

**🔍 Servidores autorizados a enviar e-mail:**
- **amazonses.com:** Amazon SES (Simple Email Service)
- **_spf.google.com:** Google Workspace
- **mail.zendesk.com:** Zendesk (suporte)
- **302036.spf06.hubspotemail.net:** HubSpot (marketing)
- **_spf.salesforce.com:** Salesforce (CRM)
- **IPs específicos:** 168.245.107.217 e 168.245.71.19

**💡 Por que SPF é importante?**
- Previne **spoofing** (falsificação de remetente)
- Melhora **deliverability** (entrega de e-mails)
- Reduz e-mails marcados como **spam**

---

### **Passo 6: Fechar Terminal**

```bash
exit
```

---

## 🔬 Atividade 3.10 – Enumeração DNS com `dig`

### **Objetivo:**
Enumerar DNS com a ferramenta `dig` (mais poderosa e detalhada).

### **📍 Ambiente:**
Kali Linux 

---

### **🔍 O que é dig?**

**dig (Domain Information Groper):**
Ferramenta avançada de consulta DNS.

**Por que usar dig?**
- 📊 **Mais detalhes:** Exibe informações técnicas completas
- 🎯 **Mais controle:** Sintaxe flexível
- 🔧 **Debugging:** Ideal para troubleshooting DNS
- 📈 **Performance:** Mostra tempos de query

**Comparação:**
- `host`: Simples, output limpo
- `nslookup`: Interativo, médio detalhe
- `dig`: Máximo detalhe, preferido por profissionais

---

### **Passo 1: Tornar-se Super Usuário**

```bash
sudo -i
```

---

### **Passo 2: Ver Sintaxe do dig**

```bash
dig -h
```

**Sintaxe básica:**
```
dig [@server] [domain] [query-type] [options]
```

**Exemplos de uso:**
```bash
dig google.com                    # Consulta A (IPv4)
dig google.com AAAA              # Consulta AAAA (IPv6)
dig google.com MX                # Mail servers
dig google.com NS                # Name servers
dig google.com ANY               # Todos os registros
dig @8.8.8.8 google.com          # Usa DNS específico (Google)
```

---

### **Passo 3: Consulta DNS Padrão**

```bash
dig grancursosonline.com.br
```

**Saída esperada (formatada):**

```
; <<>> DiG 9.20.11-4+b1-Debian <<>> grancursosonline.com.br
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47611
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096

;; QUESTION SECTION:
;grancursosonline.com.br.	IN	A

;; ANSWER SECTION:
grancursosonline.com.br. 300	IN	A	104.18.100.225
grancursosonline.com.br. 300	IN	A	104.18.99.225

;; Query time: 4 msec
;; SERVER: 192.168.98.2#53(192.168.98.2) (UDP)
;; WHEN: Fri Feb 09 16:16:08 -03 2024
;; MSG SIZE  rcvd: 84
```

**📊 Análise detalhada da resposta:**

### **Header Section:**
```
; <<>> DiG 9.20.11-4+b1-Debian <<>> grancursosonline.com.br
```
- Versão do dig
- Comando executado

### **Response Header:**
```
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47611
```

**Campos importantes:**
- **opcode: QUERY:** Tipo de operação (consulta padrão)
- **status: NOERROR:** Consulta bem-sucedida
- **id: 47611:** Identificador único da consulta

**Outros status possíveis:**
- **NXDOMAIN:** Domínio não existe
- **SERVFAIL:** Servidor DNS falhou
- **REFUSED:** Consulta recusada

### **Flags:**
```
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1
```

**Flags explicados:**
- **qr:** Query Response (é uma resposta)
- **rd:** Recursion Desired (recursão solicitada)
- **ra:** Recursion Available (recursão disponível)

**Contadores:**
- **QUERY: 1:** 1 pergunta
- **ANSWER: 2:** 2 respostas
- **AUTHORITY: 0:** 0 registros de autoridade
- **ADDITIONAL: 1:** 1 registro adicional

### **OPT PSEUDOSECTION:**
```
; EDNS: version: 0, flags:; udp: 4096
```

**💡 EDNS (Extension Mechanisms for DNS):**
- Permite pacotes DNS maiores que 512 bytes
- **udp: 4096:** Tamanho máximo de pacote UDP

### **QUESTION SECTION:**
```
;grancursosonline.com.br.	IN	A
```
- **IN:** Internet class
- **A:** Tipo de registro (IPv4)

### **ANSWER SECTION:**
```
grancursosonline.com.br. 300	IN	A	104.18.100.225
grancursosonline.com.br. 300	IN	A	104.18.99.225
```

**Campos:**
- **grancursosonline.com.br.:** Nome (note o ponto final)
- **300:** TTL (Time To Live) em segundos
- **IN:** Internet class
- **A:** Tipo de registro
- **104.18.100.225:** Valor (endereço IP)

**💡 TTL de 300 segundos = 5 minutos:**
Resultado pode ser cacheado por 5 minutos.

### **Query Statistics:**
```
;; Query time: 4 msec
;; SERVER: 192.168.98.2#53(192.168.98.2) (UDP)
;; WHEN: Fri Feb 09 16:16:08 -03 2024
;; MSG SIZE  rcvd: 84
```

- **Query time:** Latência da consulta (4ms é excelente)
- **SERVER:** DNS usado
- **WHEN:** Timestamp
- **MSG SIZE:** Tamanho da resposta em bytes

---

### **Passo 4: Consultar Name Servers**

```bash
dig grancursosonline.com.br -t ns
```

**Ou:**
```bash
dig grancursosonline.com.br NS
```

**Saída esperada (seção de resposta):**

```
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	NS

;; ANSWER SECTION:
grancursosonline.com.br. 300	IN	NS	rita.ns.cloudflare.com.
grancursosonline.com.br. 300	IN	NS	dan.ns.cloudflare.com.
```

**📊 Análise:**
- 2 name servers (redundância)
- Ambos Cloudflare
- TTL de 300 segundos

---

### **Passo 5: Consultar Mail Servers**

```bash
dig grancursosonline.com.br -t mx
```

**Saída esperada (seção de resposta):**

```
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	MX

;; ANSWER SECTION:
grancursosonline.com.br. 300	IN	MX	1 aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt1.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt2.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt3.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt4.aspmx.l.google.com.
```

**📊 Estrutura MX:**
```
┌─ 1 → aspmx.l.google.com         (Principal)
├─ 5 → alt1.aspmx.l.google.com    (Secundário A)
├─ 5 → alt2.aspmx.l.google.com    (Secundário B)
├─10 → alt3.aspmx.l.google.com    (Backup A)
└─10 → alt4.aspmx.l.google.com    (Backup B)
```

---

### **Passo 6: Consultar IPv6**

```bash
dig grancursosonline.com.br AAAA
```

**Saída esperada (seção de resposta):**

```
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	AAAA

;; ANSWER SECTION:
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:64e1
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:63e1
```

**📊 Análise IPv6:**
- 2 endereços IPv6
- Prefixo `2606:4700::` = Cloudflare
- Suporte dual-stack (IPv4 + IPv6)

---

### **Passo 7: Consultar CNAME (Canonical Name)** 📸

```bash
dig grancursosonline.com.br CNAME
```

**Saída esperada:**

```
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	CNAME

;; AUTHORITY SECTION:
grancursosonline.com.br. 300	IN	SOA	dan.ns.cloudflare.com. dns.cloudflare.com. 2332988706 10000 2400 604800 1800
```

**🔍 O que é CNAME?**
**Canonical Name:** Alias para outro nome de domínio.

**Exemplo de CNAME:**
```
www.example.com → example.com
blog.example.com → example.com
```

**Neste caso:**
Domínio não possui CNAME, então retorna registro **SOA** (Start of Authority).

**📊 Análise do SOA:**
```
dan.ns.cloudflare.com.           → Primary name server
dns.cloudflare.com.              → E-mail do admin (dns@cloudflare.com)
2332988706                       → Serial number
10000                            → Refresh (10.000 seg = ~2.7 horas)
2400                             → Retry (2.400 seg = 40 min)
604800                           → Expire (604.800 seg = 7 dias)
1800                             → Minimum TTL (1.800 seg = 30 min)
```

**💡 SOA (Start of Authority):**
Registro principal que contém informações administrativas sobre a zona DNS.

**Campos do SOA:**
- **Primary NS:** Servidor DNS primário
- **Admin email:** E-mail do administrador (@ vira ponto)
- **Serial:** Número de versão da zona
- **Refresh:** Intervalo de atualização para secundários
- **Retry:** Tempo de espera antes de retry
- **Expire:** Quando dados secundários expiram
- **Minimum TTL:** TTL padrão para registros negativos

---

### **Passo 8: Fechar Terminal**

```bash
exit
```

---

## 🎓 Resumo de Comandos DNS

### **Comparação: host vs nslookup vs dig**

| Característica | host | nslookup | dig |
|----------------|------|----------|-----|
| **Output** | Limpo | Médio | Detalhado |
| **Interativo** | Não | Sim | Não (mas pode) |
| **Debugging** | Básico | Médio | Avançado |
| **Verbosidade** | Baixa | Média | Alta |
| **Uso comum** | Scripts rápidos | Troubleshooting | Análise profunda |
| **Performance** | Rápido | Médio | Rápido |

### **Quando usar cada ferramenta:**

**Use `host` quando:**
- Precisa de resposta rápida e limpa
- Vai usar em scripts
- Quer apenas o essencial

**Use `nslookup` quando:**
- Quer modo interativo
- Precisa fazer várias consultas seguidas
- Familiar com sintaxe Windows

**Use `dig` quando:**
- Precisa de máximo detalhe
- Debugging de problemas DNS
- Análise de TTLs e timing
- Trabalho profissional

---

## 📊 Tipos de Registros DNS - Resumo Completo

| Tipo | Nome | Propósito | Exemplo |
|------|------|-----------|---------|
| **A** | Address | Mapeia nome → IPv4 | example.com → 1.2.3.4 |
| **AAAA** | IPv6 Address | Mapeia nome → IPv6 | example.com → 2001:db8::1 |
| **CNAME** | Canonical Name | Alias de nome | www → example.com |
| **MX** | Mail Exchange | Servidores de e-mail | Priority 10: mail.example.com |
| **NS** | Name Server | Servidores DNS autoritativos | ns1.example.com |
| **TXT** | Text | Texto arbitrário | SPF, DKIM, verificações |
| **SOA** | Start of Authority | Info administrativa da zona | Serial, refresh, retry |
| **PTR** | Pointer | Resolução reversa (IP→nome) | 1.2.3.4 → example.com |
| **SRV** | Service | Localização de serviços | _sip._tcp.example.com |
| **CAA** | Certification Authority | CAs autorizadas | 0 issue "letsencrypt.org" |

---

## 🔒 Conceitos de Segurança em DNS

### **Zone Transfer (AXFR)**
Transferência completa de zona DNS (geralmente bloqueada).

**Teste:**
```bash
dig @ns1.example.com example.com AXFR
```

**Risco:** Se permitido, revela toda infraestrutura.

### **DNS Spoofing**
Falsificação de respostas DNS.

**Prevenção:**
- DNSSEC (DNS Security Extensions)
- DNS over HTTPS (DoH)
- DNS over TLS (DoT)

### **DNS Enumeration**
O que fizemos neste lab! Coletar informações DNS.

**Info obtida:**
- Infraestrutura de rede
- Servidores de e-mail
- Subdomínios
- Serviços em uso (SPF, verificações)

---


## 📚 Glossário de Termos

### **Termos de Rede**

| Termo | Significado |
|-------|-------------|
| **DNS** | Domain Name System - Sistema de nomes de domínio |
| **IP** | Internet Protocol - Protocolo de internet |
| **IPv4** | IP versão 4 (32 bits) - ex: 192.168.1.1 |
| **IPv6** | IP versão 6 (128 bits) - ex: 2001:db8::1 |
| **TTL** | Time To Live - Tempo de vida (saltos ou segundos) |
| **RTT** | Round Trip Time - Tempo de ida e volta |
| **MTU** | Maximum Transmission Unit - Tamanho máximo de pacote |
| **Gateway** | Roteador de saída para outras redes |
| **Loopback** | Interface virtual para comunicação local (127.0.0.1) |

### **Termos de DNS**

| Termo | Significado |
|-------|-------------|
| **Name Server** | Servidor DNS que responde consultas |
| **Zone Transfer** | Cópia completa de zona DNS |
| **Authoritative** | Resposta oficial do servidor do domínio |
| **Recursive** | Consulta que resolve completamente o nome |
| **FQDN** | Fully Qualified Domain Name - Nome completo |
| **Subdomain** | Domínio filho (www.example.com) |
| **TLD** | Top Level Domain (.com, .br, .org) |

### **Termos de Segurança**

| Termo | Significado |
|-------|-------------|
| **Honeypot** | Sistema isca para atrair atacantes |
| **Enumeration** | Coleta sistemática de informações |
| **Reconnaissance** | Reconhecimento, primeira fase de ataque |
| **OSINT** | Open Source Intelligence - Inteligência de fontes abertas |
| **Footprinting** | Mapeamento de pegada digital |
| **SPF** | Sender Policy Framework - Política de remetentes autorizados |
| **CDN** | Content Delivery Network - Rede de distribuição de conteúdo |

---

## 🎯 Objetivos de Aprendizagem Alcançados

✅ Dominio comandos básicos de diagnóstico de rede Linux  
✅ Configurar e teste de um honeypot funcional  
✅ Enumerar DNS usando três ferramentas diferentes  
✅ Interpretação de registros DNS (A, AAAA, MX, NS, TXT, SOA)  
✅ Compreenção de conceitos de enumeração e reconhecimento  
✅ Analise de infraestrutura de rede via DNS  
✅ Identificação de servidores de e-mail e suas prioridades  
✅ Entendimento de políticas SPF e verificações de domínio  

---

## 🔗 Referências

- **Kali Linux Documentation:** https://www.kali.org/docs/
- **PentBox Project:** https://github.com/technicaldada/pentbox
- **DNS RFC 1035:** https://tools.ietf.org/html/rfc1035
- **SPF RFC 7208:** https://tools.ietf.org/html/rfc7208
- **Cloudflare Learning:** https://www.cloudflare.com/learning/

---

**Autor:** Bruno Neemias   
**Data:** Fevereiro 2025   
**Laboratório:** 7 - Ferramentas de Detecção de Rede e Enumeração DNS
