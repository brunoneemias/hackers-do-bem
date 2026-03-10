# 🔁 Módulo 7, Aula 1: Redundância e Replicação
> **Foco:** Redundância em redes, RAID, Rsync, replicação síncrona, assíncrona e em nuvem

---

## 📌 Objetivos

- Compreender os conceitos de redundância e replicação para garantir a resiliência e a recuperação de dados em caso de falhas ou desastres

---

## 1. 🛡️ Redundância

Redundância é o princípio de **duplicar componentes ou sistemas** para evitar perda de dados ou interrupções no serviço. É um dos pilares da **disponibilidade** — um dos três atributos fundamentais da segurança da informação (CID).

### Benefícios da Redundância

| Benefício | Descrição |
|---|---|
| **Disponibilidade Contínua** | Se um componente falhar, outro assume automaticamente sem interromper o serviço |
| **Tolerância a Falhas** | Reduz a probabilidade de perda de dados ou interrupções — a carga é redistribuída entre os componentes restantes |
| **Recuperação Rápida** | O **failover** transfere automaticamente o tráfego de um componente falho para um redundante via balanceador de carga |
| **Proteção contra Desastres** | Backups em locais geograficamente separados protegem dados contra incêndios, inundações e outros desastres |
| **Escalabilidade** | Novos componentes redundantes podem ser adicionados conforme a demanda cresce |

### Exemplo Prático — Cluster de Servidores Web

```
[Usuários] → [Balanceador de Carga]
                      ↓
        ┌─────────────┼─────────────┐
   [Servidor 1]  [Servidor 2]  [Servidor N]
```

- Se um servidor falhar, o balanceador de carga redireciona o tráfego para os demais
- Permite manutenção programada sem downtime — um servidor é retirado enquanto os outros atendem

### Redundância Geográfica

Backups replicados em **dois locais fisicamente separados** (ex: data center local + nuvem em outra cidade), garantindo recuperação mesmo em caso de desastre catastrófico no local principal.

---

## 2. 💽 RAID — Redundant Array of Independent Disks

Tecnologia que combina múltiplos discos rígidos para melhorar **desempenho, capacidade e confiabilidade** do armazenamento.

### Implementação

| Tipo | Descrição | Prós | Contras |
|---|---|---|---|
| **Via Software** | Gerenciado pelo SO ou software dedicado | Mais barato, portável entre sistemas | Usa CPU do sistema; menor desempenho |
| **Via Hardware** | Controladora RAID dedicada (placa PCI-e) | Alto desempenho, processador próprio, cache dedicado | Mais caro; pode ter suporte limitado a SOs |

### Níveis de RAID

| Nível | Nome | Como Funciona | Tolerância a Falhas | Capacidade Efetiva |
|---|---|---|---|---|
| **RAID 0** | Striping | Dados divididos igualmente entre os discos em paralelo | ❌ Nenhuma — 1 disco falho = todos os dados perdidos | 100% dos discos |
| **RAID 1** | Espelhamento | Cópia idêntica em 2+ discos simultaneamente | ✅ Alta — 1 disco falho, dados no espelho | 50% dos discos |
| **RAID 5** | Striping com paridade | Dados + paridade distribuídos em 3+ discos | ✅ Tolera falha de 1 disco (reconstrução pela paridade) | N-1 discos |
| **RAID 6** | Striping com paridade dupla | Paridade dupla em 4+ discos | ✅ Tolera falha de 2 discos simultâneos | N-2 discos |
| **RAID 10 (1+0)** | Espelhamento + Striping | RAID 1 aplicado sobre RAID 0 | ✅ Alta — combina redundância e desempenho | 50% dos discos |
| **RAID 01 (0+1)** | Striping + Espelhamento | RAID 0 espelhado em RAID 1 | ✅ Alta — semelhante ao RAID 10 | 50% dos discos |

> 💡 **Quando usar cada nível:**
> - **RAID 0:** máximo desempenho, sem necessidade de redundância (ex: edição de vídeo temporária)
> - **RAID 1:** simplicidade e alta confiabilidade (ex: servidor de arquivos pequeno)
> - **RAID 5:** equilíbrio entre desempenho, capacidade e redundância (uso geral)
> - **RAID 6:** ambientes críticos que não toleram perda de dados (ex: banco de dados)
> - **RAID 10:** alto desempenho + alta confiabilidade (ex: servidores de banco de dados transacionais)

---

## 3. 🔄 Rsync — Remote Synchronization

Protocolo e ferramenta para **sincronização eficiente de dados em rede**, transferindo apenas as partes modificadas dos arquivos (delta transfer).

### Como Funciona

```
[Origem]                          [Destino]
   │                                  │
   ├── Compara atributos (tamanho,     │
   │   timestamp, checksum por bloco) │
   │                                  │
   ├── Identifica blocos modificados ──┤
   │                                  │
   └── Transfere APENAS os deltas ────→ Reconstrói arquivo atualizado
```

### Etapas do Processo

1. **Comparação:** compara atributos e gera checksums de blocos em ambos os lados
2. **Transferência delta:** envia apenas os blocos modificados ou ausentes — economiza largura de banda
3. **Reconstrução:** o destino aplica as mudanças, adiciona novos blocos e descarta os obsoletos

> ✅ **Ideal para:** sincronização de grandes arquivos em redes lentas, backups incrementais e replicação de diretórios

---

## 4. 🔃 Tipos de Replicação

### Replicação Síncrona

Os dados são replicados **em tempo real** — a gravação só é considerada concluída após confirmação do destino.

```
[Sistema Origem] ──gravar──→ [Confirma réplica no destino] ──→ Operação concluída
```

| Característica | Detalhe |
|---|---|
| **Consistência** | ✅ Total — dados sempre sincronizados |
| **Desempenho** | ⚠️ Pode impactar — aguarda confirmação antes de concluir |
| **Ideal para** | Bancos de dados transacionais críticos |
| **Exemplo** | Oracle Data Guard |

---

### Replicação Assíncrona

Os dados são replicados em **intervalos de tempo definidos**, sem aguardar confirmação do destino.

```
[Sistema Origem] ──gravar──→ Operação concluída imediatamente
                                      ↓ (depois, em intervalo definido)
                              [Réplica no destino]
```

| Característica | Detalhe |
|---|---|
| **Consistência** | ⚠️ Pequeno atraso aceitável (lag) |
| **Desempenho** | ✅ Melhor — não bloqueia a operação |
| **Ideal para** | Recuperação de desastres, replicação entre locais distantes |
| **Exemplo** | Azure Blob Geo-Replication |

---

### Replicação em Nuvem

Criação de cópias de dados em **diferentes servidores ou data centers na nuvem**, garantindo disponibilidade, durabilidade e escalabilidade.

| Método | Descrição | Exemplos |
|---|---|---|
| **Síncrona em nuvem** | Dados replicados em tempo real entre regiões | Amazon S3 Replication, Google Cloud Cross-Region Replication |
| **Assíncrona em nuvem** | Replicação em intervalos definidos com pequeno atraso | Azure Blob Geo-Replication, Google Cloud Object Versioning |
| **Híbrida em nuvem** | Combinação: síncrona para dados críticos + assíncrona para dados menos sensíveis | Configurável nos principais provedores (AWS, Azure, GCP) |

---

## 📊 Comparativo — Tipos de Replicação

| Critério | Síncrona | Assíncrona | Em Nuvem |
|---|---|---|---|
| **Latência** | Alta (aguarda confirmação) | Baixa (não bloqueia) | Variável |
| **Consistência** | Total | Eventual (pequeno lag) | Depende do método |
| **Desempenho** | Pode ser impactado | Melhor | Escalável |
| **Ideal para** | Dados críticos/transacionais | Recuperação de desastres | Alta disponibilidade global |
| **Custo** | Maior (infraestrutura local) | Menor | Pay-as-you-go |

---

## 📊 Resumo dos Tópicos — Aula 1

| Tópico | Conceito-chave | Ponto Essencial |
|---|---|---|
| **Redundância** | Duplicar componentes para garantir disponibilidade | Failover, balanceamento de carga, redundância geográfica |
| **RAID 0** | Striping — desempenho máximo | Sem tolerância a falhas |
| **RAID 1** | Espelhamento — alta confiabilidade | Metade da capacidade usada |
| **RAID 5** | Striping com paridade — equilíbrio | Tolera 1 disco falho |
| **RAID 6** | Paridade dupla — máxima segurança | Tolera 2 discos falhos simultâneos |
| **RAID 10** | Espelhamento + Striping | Desempenho + redundância combinados |
| **Rsync** | Sincronização incremental via delta transfer | Economiza banda — transfere só o que mudou |
| **Replicação Síncrona** | Tempo real com confirmação | Consistência total, pode impactar desempenho |
| **Replicação Assíncrona** | Intervalo definido sem confirmação | Melhor desempenho, pequeno atraso aceitável |
| **Replicação em Nuvem** | Cópias distribuídas em data centers na nuvem | Escalabilidade e disponibilidade global |

---

> ⚠️ **Lembre-se:** RAID **não é backup**. RAID protege contra falha de hardware, mas não contra exclusão acidental, ransomware ou desastres. Combine RAID com uma estratégia de backup robusta (regra 3-2-1).

---
