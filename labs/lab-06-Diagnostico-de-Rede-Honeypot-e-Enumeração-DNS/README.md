# 🛡️ Lab 06 — Diagnóstico de Rede, Honeypot e Enumeração DNS no Kali Linux

---

## 📁 Estrutura do Repositório

```
lab06-diagnostico-rede-honeypot-dns/
│
├── README.md
└── screenshots/
    ├── atividade3_6_netstat_anptu.png
    ├── atividade3_7_honeypot_intrusao.png
    ├── atividade3_8_host_mx.png
    ├── atividade3_9_nslookup_txt.png
    └── atividade3_10_dig_cname.png
```

---

## 📋 Sobre este laboratório

Neste laboratório são exploradas ferramentas essenciais para diagnóstico de redes, detecção de intrusos e coleta de informações sobre infraestrutura DNS. O foco está em entender o comportamento da rede sob a perspectiva do Blue Team e aplicar técnicas de reconhecimento passivo e ativo em ambientes controlados, com fins estritamente acadêmicos.

---

## 📑 Índice

- [Atividade 3.6 — Ferramentas de detecção de rede](#-atividade-36--ferramentas-de-detecção-de-rede)
- [Atividade 3.7 — Honeypot com PentBox](#-atividade-37--honeypot-com-pentbox)
- [Atividade 3.8 — Enumeração DNS com host](#-atividade-38--enumeração-dns-com-host)
- [Atividade 3.9 — Enumeração DNS com nslookup](#-atividade-39--enumeração-dns-com-nslookup)
- [Atividade 3.10 — Enumeração DNS com dig](#-atividade-310--enumeração-dns-com-dig)
- [Ferramentas utilizadas](#-ferramentas-utilizadas)
- [Aprendizados](#-aprendizados)

---

## 🌐 Atividade 3.6 — Ferramentas de detecção de rede

### O que é?
Conjunto de comandos nativos do Linux para diagnosticar o estado da rede local: interfaces ativas, conectividade, roteamento, estatísticas de protocolo e serviços em escuta. São ferramentas fundamentais para qualquer analista de redes ou SOC.

### O que foi feito?
- Verificação das interfaces de rede com `ifconfig` (docker0, eth0, lo)
- Teste de conectividade e resolução de DNS com `ping www.google.com`
- Mapeamento de rota até um destino externo com `traceroute -I`, identificando os saltos e passagem pela infraestrutura da Cloudflare
- Visualização das estatísticas de interface com `netstat -i` (pacotes RX/TX, erros, drops)
- Consulta à tabela de roteamento com `netstat -rn` (gateway padrão, rotas diretas)
- Análise de estatísticas por protocolo com `netstat -s` (IP, ICMP, TCP, UDP)
- Listagem de todas as conexões ativas e serviços em execução com `netstat -anptu`

### Comandos principais
```bash
ifconfig                                 # Interfaces e IPs
ping www.google.com                      # Teste de conectividade e resolução DNS
traceroute -I grancursos.com.br          # Mapeamento de rota com ICMP
netstat -i                               # Estatísticas de interfaces
netstat -rn                              # Tabela de roteamento
netstat -s                               # Estatísticas por protocolo
netstat -anptu                           # Conexões ativas e serviços em escuta
```

> 📸 **Print solicitado — Passo 8:** Terminal exibindo o resultado do `netstat -anptu` com as conexões ativas (SSH, XRDP, DHCP) e seus respectivos PIDs e programas

---

## 🍯 Atividade 3.7 — Honeypot com PentBox

### O que é?
Um **Honeypot** é um sistema ou serviço falso criado intencionalmente para atrair e registrar tentativas de acesso não autorizado. O **PentBox** é uma ferramenta Ruby de código aberto que, entre outras funções, permite configurar um honeypot de forma rápida e simples.

### O que foi feito?
- Acesso à pasta do PentBox e execução do script `./pentbox.rb`
- Navegação pelo menu: `2 - Network tools` → `3 - Honeypot` → `1 - Fast Auto Configuration`
- Honeypot ativado automaticamente na **porta 80** do Kali Linux
- Acesso ao IP do Kali via Microsoft Edge no **Windows Server 2022**
- Registro automático da tentativa de intrusão no terminal do Kali, capturando IP de origem, horário, método HTTP e headers completos do navegador (User-Agent, Accept, etc.)

### Fluxo do ataque detectado
```
Windows Server 2022 (Edge)
        ↓  HTTP GET /
Kali Linux — PentBox Honeypot (porta 80)
        ↓
  INTRUSION ATTEMPT DETECTED! → log no terminal
```

### Comandos principais
```bash
cd /curso/pentbox/pentbox-1.8
./pentbox.rb    # Menu: 2 → 3 → 1
```

> 📸 **Print solicitado — Passo 10:** Terminal do Kali Linux exibindo a mensagem `INTRUSION ATTEMPT DETECTED!` com IP de origem, timestamp e headers HTTP capturados

---

## 🔍 Atividade 3.8 — Enumeração DNS com host

### O que é?
O comando `host` é uma ferramenta de consulta DNS simples e direta, disponível nativamente no Linux. Permite obter registros A (IPv4), AAAA (IPv6), MX (e-mail) e NS (servidores de nome) de qualquer domínio.

### O que foi feito?
- Consulta completa ao domínio `grancursos.com.br` — identificação de IPs (Cloudflare), endereços IPv6 e servidores de e-mail (Google Workspace)
- Consulta de Name Servers (`-t ns`) ao domínio `esr.rnp.br` — resultado: nenhum registro NS encontrado
- Consulta de Name Servers (`-t ns`) ao domínio `grancursosonline.com.br` — identificados dois NS da Cloudflare
- Enumeração dos servidores de e-mail MX (`-t mx`) de `grancursosonline.com.br`, revelando a hierarquia de prioridade dos servidores do Google

### Comandos principais
```bash
host grancursos.com.br               # Consulta completa (A, AAAA, MX)
host -t ns esr.rnp.br                # Name Servers do domínio
host -t ns grancursosonline.com.br   # Name Servers com Cloudflare
host -t mx grancursosonline.com.br   # Servidores de e-mail MX
```

> 📸 **Print solicitado — Passo 5:** Terminal exibindo o resultado do `host -t mx grancursosonline.com.br` com a lista de servidores de e-mail e suas prioridades

---

## 🔎 Atividade 3.9 — Enumeração DNS com nslookup

### O que é?
O `nslookup` é uma ferramenta interativa de consulta DNS disponível tanto em Linux quanto em Windows. Permite consultar diferentes tipos de registros DNS de forma sequencial dentro de uma sessão interativa, o que o torna útil para análise aprofundada de domínios.

### O que foi feito?
- Consulta padrão (registro A) ao domínio `grancursosonline.com.br` — retornou dois IPs IPv4 e dois IPv6, todos da Cloudflare
- Dentro do modo interativo, alteração do tipo para `NS` (`set type=ns`) e consulta dos servidores de nomes autoritativos
- Alteração do tipo para `MX` (`set type=mx`) e consulta à hierarquia de servidores de e-mail (Google Workspace)
- Consulta de registros `TXT` com `nslookup -type=txt`, revelando verificações de domínio do Google, Atlassian, Microsoft e regras SPF (Sender Policy Framework)

### Comandos principais
```bash
nslookup grancursosonline.com.br         # Registro A (IPv4/IPv6)
nslookup                                 # Modo interativo
> set type=ns                            # Altera para Name Servers
> grancursosonline.com.br
> set type=mx                            # Altera para servidores de e-mail
> grancursosonline.com.br
nslookup -type=txt grancursosonline.com.br  # Registros TXT (SPF, verificações)
```

> 📸 **Print solicitado — Passo 5:** Terminal exibindo o resultado do `nslookup -type=txt grancursosonline.com.br` com os registros TXT, incluindo SPF e verificações de domínio

---

## ⚙️ Atividade 3.10 — Enumeração DNS com dig

### O que é?
O `dig` (Domain Information Groper) é a ferramenta de consulta DNS mais completa e detalhada disponível no Linux. Exibe todas as seções de uma resposta DNS (QUESTION, ANSWER, AUTHORITY, ADDITIONAL), tempo de consulta, servidor utilizado e tamanho da mensagem — sendo a preferida por profissionais de segurança e administradores de rede.

### O que foi feito?
- Consulta da sintaxe com `dig -h`
- Consulta padrão (registro A) ao domínio `grancursosonline.com.br` — exibição completa com TTL, flags, servidor DNS e tempo de resposta
- Consulta de Name Servers (`-t ns`) — identificados `rita.ns.cloudflare.com` e `dan.ns.cloudflare.com`
- Consulta de servidores de e-mail (`-t mx`) — listagem completa com prioridades
- Consulta de endereços IPv6 (`AAAA`) — dois endereços da Cloudflare retornados
- Consulta de registro CNAME — ausência de CNAME confirmada pela seção AUTHORITY com registro SOA da Cloudflare

### Comandos principais
```bash
dig -h                                   # Exibe sintaxe e opções
dig grancursosonline.com.br              # Registro A (padrão)
dig grancursosonline.com.br -t ns        # Name Servers
dig grancursosonline.com.br -t mx        # Servidores de e-mail
dig grancursosonline.com.br AAAA         # Endereços IPv6
dig grancursosonline.com.br CNAME        # Nome canônico
```

> 📸 **Print solicitado — Passo 7:** Terminal exibindo o resultado do `dig grancursosonline.com.br CNAME` com a seção AUTHORITY mostrando o registro SOA da Cloudflare

---

## 🛠️ Ferramentas utilizadas

| Ferramenta | Função |
|---|---|
| `ifconfig` / `ping` / `traceroute` | Diagnóstico de interfaces, conectividade e roteamento |
| `netstat` | Estatísticas de rede, tabela de roteamento e conexões ativas |
| PentBox | Criação e monitoramento de Honeypot na porta 80 |
| `host` | Consulta DNS simplificada (A, AAAA, MX, NS) |
| `nslookup` | Consulta DNS interativa com múltiplos tipos de registro |
| `dig` | Consulta DNS avançada com resposta detalhada completa |

---

## 📚 Aprendizados

- Como usar ferramentas nativas do Linux para mapear o estado da rede e identificar serviços em execução
- Como configurar e monitorar um Honeypot simples para detectar e registrar tentativas de acesso não autorizado
- Como enumerar informações DNS de domínios com três ferramentas diferentes (`host`, `nslookup`, `dig`), entendendo os registros A, AAAA, MX, NS, TXT, CNAME e SOA
- Como identificar o uso de CDN (Cloudflare) e serviços de e-mail (Google Workspace) através de registros DNS públicos
- Como interpretar registros SPF e TXT para mapear os serviços utilizados por uma organização

---

> ⚠️ **Aviso:** Todo o conteúdo deste repositório foi desenvolvido exclusivamente para fins acadêmicos em ambientes controlados. O uso dessas técnicas em sistemas sem autorização expressa é ilegal.
