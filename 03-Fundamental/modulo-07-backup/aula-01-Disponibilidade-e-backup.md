# 🔐 Segurança da Informação — Módulo 7: Disponibilidade e Backup

> **Foco:** Redundância de armazenamento, replicação de dados e backup em nuvem

---

## 📌 Conceitos Essenciais

### 🛡️ Pilar da Disponibilidade (Availability)

A **disponibilidade** é um dos três pilares da segurança da informação (CID — Confidencialidade, Integridade e **Disponibilidade**). Ela garante que dados e sistemas estejam acessíveis quando necessário. As práticas deste módulo têm como objetivo direto proteger esse pilar por meio de:

- Redundância de armazenamento (RAID)
- Replicação de dados (Rsync)
- Backup em nuvem (OneDrive)

---

## 💾 RAID — Redundant Array of Independent Disks

RAID é uma tecnologia que combina múltiplos discos físicos (ou partições) em uma única unidade lógica. Existem diferentes níveis com objetivos distintos.

### RAID 0 — Striping (Desempenho)

| Característica | Detalhe |
|---|---|
| **Objetivo** | Aumentar velocidade de leitura/escrita |
| **Funcionamento** | Dados são divididos (*striped*) entre os discos em paralelo |
| **Tolerância a falhas** | ❌ Nenhuma — se um disco falhar, todos os dados são perdidos |
| **Espaço total** | Soma dos discos (2 × 100M = ~196M utilizáveis) |
| **Uso típico** | Ambientes de alto desempenho onde perda de dados é aceitável |

**Implementação no Linux (mdadm):**
```bash
# Criar array RAID 0 com 2 partições
mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme1n1p1 /dev/nvme1n1p2

# Formatar e montar
mkfs.ext4 /dev/md0
mkdir /mnt/raid0
mount /dev/md0 /mnt/raid0

# Verificar
df -h
```

> ⚠️ **Atenção de segurança:** RAID 0 **não é** backup. A perda de qualquer disco destrói todos os dados.

---

### RAID 1 — Mirroring (Redundância)

| Característica | Detalhe |
|---|---|
| **Objetivo** | Tolerância a falhas por espelhamento |
| **Funcionamento** | Dados são escritos simultaneamente em dois discos |
| **Tolerância a falhas** | ✅ Sim — se um disco falhar, o outro mantém os dados intactos |
| **Espaço total** | Igual ao menor disco (100M → ~88M utilizáveis) |
| **Uso típico** | Ambientes críticos onde a perda de dados é inaceitável |

**Implementação no Linux (mdadm):**
```bash
# Criar array RAID 1 com 2 partições
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/nvme1n1p3 /dev/nvme1n1p4

# Verificar status de todos os arrays
cat /proc/mdstat

# Formatar e montar
mkfs.ext4 /dev/md1
mkdir /mnt/raid1
mount /dev/md1 /mnt/raid1
```

> ✅ **Boa prática:** RAID 1 é ideal para aumentar a resiliência de dados críticos em servidores.

---

## 🔄 Rsync — Replicação de Dados

O `rsync` é uma ferramenta poderosa para sincronização eficiente de arquivos e diretórios, transferindo apenas as diferenças entre origem e destino.

### Flags principais

| Flag | Significado |
|---|---|
| `-a` | Modo arquivo: preserva permissões, timestamps, links simbólicos e replica recursivamente |
| `-v` | Verbose: exibe detalhes da operação |
| `-z` | Compressão durante a transferência (útil em redes lentas) |

### Replicação manual

```bash
# Copiar arquivo específico de PastaA para PastaB
rsync -avz /home/aluno/Documentos/PastaA/Teste.txt /home/aluno/Documentos/PastaB

# Sincronizar diretório completo
rsync -avz /home/aluno/Documentos/PastaA/ /home/aluno/Documentos/PastaB/
```

### Replicação automática com Cron

O `cron` é o agendador de tarefas nativo do Linux. Permite executar scripts em intervalos definidos.

**1. Criar o script de sincronização:**
```bash
nano /home/aluno/Documentos/sync_script.sh
```

```bash
#!/bin/bash
rsync -avz /home/aluno/Documentos/PastaA/ /home/aluno/Documentos/PastaB/
```

**2. Tornar o script executável:**
```bash
chmod +x sync_script.sh
```

**3. Agendar execução a cada minuto com crontab:**
```bash
crontab -e
```
```
* * * * * /home/aluno/Documentos/sync_script.sh
```

> 💡 **Sintaxe do cron:** `minuto hora dia mês dia-da-semana comando`  
> Referência: https://cron.help/

---

## ☁️ Backup em Nuvem — OneDrive (Windows Server)

A **replicação síncrona em nuvem** garante que arquivos locais sejam automaticamente espelhados em um servidor remoto, protegendo contra perda por falha de hardware local.

### Conceito: Replicação Síncrona vs. Backup Tradicional

| | Replicação Síncrona | Backup Tradicional |
|---|---|---|
| **Frequência** | Contínua (em tempo real) | Agendada (diária, semanal) |
| **Velocidade de recuperação** | Imediata | Depende do agendamento |
| **Proteção contra ransomware** | Menor (arquivos corrompidos são sincronizados) | Maior (versões anteriores preservadas) |

### Configuração do OneDrive no Windows Server 2022

1. Instalar o **OneDriveSetup**
2. Adicionar `https://odc.officeapps.live.com` aos **Trusted Sites** (Internet Options > Security)
3. Autenticar com conta Microsoft
4. Selecionar pastas para backup automático (ex.: Desktop)
5. Sincronização ocorre em tempo real após configuração

---

## 🗂️ Estrutura de Partições Linux (Referência)

| Partição | Descrição |
|---|---|
| `/dev/nvme0n1p1` | Sistema de arquivos principal (Kali Linux) |
| `/dev/nvme0n1p14` | BIOS boot — bootloader GRUB2 (3 MiB) |
| `/dev/nvme0n1p15` | EFI System — boot UEFI (124 MiB) |
| `/dev/nvme1n1` | Disco secundário para laboratório (2 GiB) |
| `/dev/md0` | Array RAID 0 criado (196 MiB) |
| `/dev/md1` | Array RAID 1 criado (88 MiB utilizáveis) |

**Tabelas de partição:**
- **MBR (DOS):** Legado, máximo 4 partições primárias, discos até 2 TB
- **GPT:** Moderno, necessário para UEFI, suporta mais partições e discos maiores que 2 TB

---

## 🧰 Ferramentas Utilizadas

| Ferramenta | Função |
|---|---|
| `fdisk` | Gerenciamento de partições em disco |
| `partprobe` | Atualiza o kernel com nova tabela de partições |
| `mdadm` | Criação e gerenciamento de arrays RAID via software |
| `mkfs.ext4` | Formata partição com sistema de arquivos ext4 |
| `mount` | Monta dispositivos em pontos do sistema de arquivos |
| `df -h` | Exibe uso de espaço em disco de forma legível |
| `rsync` | Sincronização eficiente de arquivos e diretórios |
| `crontab` | Agendador de tarefas do Linux |
| `cat /proc/mdstat` | Exibe status dos arrays RAID ativos |

---

## 📊 Comparativo: Estratégias de Proteção de Dados

| Estratégia | Proteção | Desempenho | Complexidade | Custo |
|---|---|---|---|---|
| **RAID 0** | ❌ Nenhuma | ⬆️ Alto | Baixa | Baixo |
| **RAID 1** | ✅ Alta | Normal | Baixa | Médio (2x disco) |
| **Rsync + Cron** | ✅ Alta | Normal | Média | Baixo |
| **Backup em Nuvem** | ✅ Alta | Depende da rede | Baixa | Variável |

---

## ⚠️ Boas Práticas de Segurança

- **RAID não substitui backup** — RAID protege contra falha de hardware, não contra exclusão acidental, ransomware ou desastres.
- **Regra 3-2-1:** Mantenha 3 cópias dos dados, em 2 mídias diferentes, com 1 cópia offsite (nuvem).
- **Teste seus backups** — Um backup nunca testado pode ser inútil na hora da recuperação.
- **Automatize a replicação** — Processos manuais são sujeitos a falha humana; use cron ou ferramentas de backup.
- **Privilégio mínimo** — Use `sudo` apenas quando necessário e não opere como root por padrão.

---
