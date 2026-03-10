# 💾 Módulo 7, Aula 3: Backup
> **Foco:** Tipos de backup, ferramentas e mídias de armazenamento

---

## 📌 Objetivos

- Conhecer os tipos de Backup
- Explorar as ferramentas de replicação e backup

---

## 🎯 Por que fazer Backup?

Backup é a criação de **cópias de dados importantes** para preservar sua integridade e disponibilidade em caso de:

- Perda ou exclusão acidental
- Corrupção de dados
- Falha de hardware
- Ataques (ex: ransomware)
- Desastres naturais

> Os dados são ativos vitais — sua perda pode causar prejuízos financeiros, interrupção de serviços, danos à reputação e riscos legais.

---

## 1. 📦 Tipos de Backup

### Backup Completo (Full Backup)

Copia **todos** os arquivos e dados selecionados, independentemente de terem sido modificados.

| Característica | Detalhe |
|---|---|
| **O que copia** | Tudo — arquivos, SO, aplicativos, configurações |
| **Restauração** | Simples e rápida — apenas um conjunto |
| **Espaço necessário** | Alto — cópia integral a cada execução |
| **Tempo de backup** | Longo |
| **Dependência** | Nenhuma — independente de outros backups |

> ✅ **Ideal para:** base periódica combinada com backups incrementais ou diferenciais.

---

### Backup Incremental

Copia apenas os arquivos **modificados ou adicionados desde o último backup** (completo ou incremental).

```
Dia 1: Backup Completo (todos os arquivos)
Dia 2: Incremental → apenas arquivos alterados desde o Dia 1
Dia 3: Incremental → apenas arquivos alterados desde o Dia 2
...
```

| Característica | Detalhe |
|---|---|
| **O que copia** | Apenas as alterações desde o último backup |
| **Restauração** | Complexa — exige backup completo + TODOS os incrementais |
| **Espaço necessário** | Baixo |
| **Tempo de backup** | Rápido |

> ✅ **Ideal para:** ambientes com grandes volumes de dados onde espaço e velocidade são prioritários.

---

### Backup Diferencial

Copia todos os arquivos **modificados desde o último backup completo**, independentemente dos incrementais realizados entre eles.

```
Dia 1: Backup Completo
Dia 2: Diferencial → tudo alterado desde Dia 1
Dia 3: Diferencial → tudo alterado desde Dia 1 (acumula)
Dia 4: Diferencial → tudo alterado desde Dia 1 (acumula mais)
```

| Característica | Detalhe |
|---|---|
| **O que copia** | Tudo alterado desde o último backup completo |
| **Restauração** | Simples — exige apenas backup completo + último diferencial |
| **Espaço necessário** | Médio e crescente (acumula alterações) |
| **Tempo de backup** | Médio |

> ✅ **Ideal para:** quando a restauração rápida é prioridade e há espaço disponível suficiente.

---

### Comparativo: Completo × Incremental × Diferencial

| Critério | Completo | Incremental | Diferencial |
|---|---|---|---|
| **O que copia** | Tudo | Só o que mudou desde o último backup | Tudo desde o último completo |
| **Velocidade de backup** | Lenta | Rápida | Média |
| **Espaço usado** | Alto | Baixo | Médio (cresce) |
| **Restauração** | Simples (1 conjunto) | Complexa (completo + todos incrementais) | Simples (completo + último diferencial) |

---

### Backup Contínuo (Continuous Backup)

Captura alterações **em tempo real**, assim que os dados são modificados.

- Usa monitoramento de arquivos em nível de bloco ou sistema de arquivos
- **Minimiza a perda de dados** — qualquer modificação é imediatamente protegida
- **Reduz o tempo de recuperação** — restauração a partir do momento mais recente
- **Desafio:** alto consumo de espaço de armazenamento e processamento

> ✅ **Ideal para:** sistemas críticos onde qualquer perda de dados é inaceitável.

---

### Backup Espelhado (Mirrored Backup)

Mantém uma **cópia exata e sincronizada** dos dados em local separado ou dispositivo diferente em tempo real.

- Qualquer alteração no original é **imediatamente refletida** no espelho
- Frequentemente implementado com RAID
- Oferece **alta disponibilidade** — se o sistema principal falha, o espelho assume
- ⚠️ **Não protege contra erros do usuário** — exclusões acidentais são espelhadas também

> ✅ **Ideal para:** alta disponibilidade; sempre combinado com outros tipos de backup para proteção completa.

---

### Backup de Imagem (Image Backup)

Cria uma **cópia exata setor a setor** de um disco ou partição inteira, incluindo SO, aplicativos, configurações e dados.

**Softwares comuns:** Acronis True Image, Clonezilla, Norton Ghost, Windows Backup

**Processo:**
1. Escolha do software de backup
2. Seleção dos discos/partições
3. Definição do local de armazenamento (HD externo, rede, nuvem)
4. Execução do backup setor a setor
5. Verificação da integridade do arquivo de imagem
6. Armazenamento seguro fora do sistema original
7. Restauração quando necessário — retorna ao estado exato do momento do backup

> ✅ **Ideal para:** recuperação completa de sistema após falha grave de hardware ou corrupção do SO.

---

### Backup em Nuvem (Cloud Backup)

Dados enviados pela rede para **servidores remotos em data centers na nuvem**.

| Característica | Detalhe |
|---|---|
| **Segurança** | Criptografia em trânsito e em repouso, controles de acesso e auditoria |
| **Escalabilidade** | Capacidade ajustável conforme necessidade, sem hardware adicional |
| **Acesso remoto** | Dados acessíveis de qualquer lugar com internet |
| **Redundância** | Dados replicados em servidores geograficamente distribuídos |
| **Automação** | Backups configurados para ocorrer automaticamente |
| **Recuperação de desastres** | Dados protegidos fora do local físico |

**Provedores populares:** Amazon S3, Google Cloud Storage, Microsoft Azure Backup, Dropbox

---

### Backup Local (Local Backup)

Cópias armazenadas em **dispositivos físicos locais** — HDs externos, servidores locais ou fitas.

- Controle direto e acesso rápido aos dados
- Sem dependência de conexão à internet
- Requer estratégia de armazenamento seguro (proteção contra incêndio, roubo, etc.)
- Ideal quando combinado com backup remoto (regra 3-2-1)

---

### Backup Remoto / Offsite Backup

Cópias armazenadas em **local geograficamente separado** das instalações principais.

- Protege contra desastres que afetam o local físico (incêndio, inundação, roubo)
- Dados criptografados durante transferência e armazenamento (SSL/TLS)
- Pode ser automatizado com rotinas regulares de sincronização
- Complementa o backup local para cobertura completa

---

### Backup de Ponto de Verificação (Checkpoint Backup)

Captura um **instantâneo (snapshot) do estado dos dados** em um momento específico, permitindo restaurar para aquele ponto exato.

**Processo:**
1. Captura do instantâneo em um ponto no tempo
2. Garantia de consistência dos dados (congelamento de operações de gravação)
3. Armazenamento seguro do snapshot
4. Restauração granular quando necessário

**Benefícios:**
- Restauração de arquivos específicos de um momento anterior
- Proteção contra corrupção ou erros de dados
- Útil para testes e desenvolvimento em ambientes isolados

> ⚠️ Múltiplos snapshots ao longo do tempo consomem espaço significativo de armazenamento.

---

## 2. 🛠️ Ferramentas de Backup (Hardware)

| Ferramenta | Descrição | Uso Típico |
|---|---|---|
| **Unidades de Fita** | Fitas magnéticas com alta capacidade e durabilidade | Backups de longo prazo e arquivamento |
| **Discos Rígidos Externos** | HDs ou SSDs externos, alta velocidade de transferência | Backups rápidos e portáteis |
| **Bibliotecas de Fita** | Sistemas automatizados com múltiplas unidades de fita | Grandes volumes de dados corporativos |
| **Armazenamento em Nuvem** | Servidores remotos acessíveis pela internet | Backup offsite escalável |
| **Appliances de Backup** | Hardware + software em solução única | Ambientes corporativos, fácil gestão |
| **NAS (Network Attached Storage)** | Servidor de armazenamento dedicado em rede | Backup centralizado em rede local |
| **VTL (Virtual Tape Library)** | Emula fitas usando armazenamento em disco | Compatibilidade com sistemas legados de fita |

---

## 3. 💿 Mídias de Backup

| Mídia | Características | Melhor Uso |
|---|---|---|
| **Fitas Magnéticas** | Alta capacidade, duráveis, econômicas por GB | Arquivamento de longo prazo |
| **Discos Rígidos (HDD)** | Alta velocidade, capacidade generosa | Backups rápidos e recuperação ágil |
| **Armazenamento em Nuvem** | Escalável, acessível remotamente, gerenciado | Backup offsite e recuperação de desastres |
| **Discos Ópticos (CD/DVD/Blu-ray)** | Menor capacidade, menor custo por unidade | Backups de pequena escala |
| **SSDs** | Velocidade máxima, resistência a choques | Backups rápidos onde desempenho é crítico |

---

## 📊 Resumo Geral — Tipos de Backup

| Tipo | Copia | Restauração | Espaço | Velocidade |
|---|---|---|---|---|
| **Completo** | Tudo | Simples | Alto | Lenta |
| **Incremental** | Mudanças desde último backup | Complexa | Baixo | Rápida |
| **Diferencial** | Mudanças desde último completo | Simples | Médio | Média |
| **Contínuo** | Alterações em tempo real | Rápida | Alto | Contínua |
| **Espelhado** | Réplica exata em tempo real | Imediata | 2x os dados | Contínua |
| **Imagem** | Disco/partição inteira setor a setor | Completa e rápida | Alto | Lenta |
| **Nuvem** | Dados enviados remotamente | Remota, via internet | Escalável | Variável |
| **Local** | Dados em dispositivo físico local | Rápida | Limitado ao hardware | Rápida |
| **Remoto/Offsite** | Cópias em local separado fisicamente | Remota | Escalável | Variável |
| **Checkpoint** | Snapshot de um ponto no tempo | Granular por ponto | Acumulativo | Variável |

---

## 🛡️ Boa Prática — Regra 3-2-1

> Mantenha **3 cópias** dos dados, em **2 mídias diferentes**, com **1 cópia offsite** (remota ou em nuvem).

```
3 cópias → Original + Backup Local + Backup Remoto
2 mídias → Ex: HD externo + Nuvem
1 offsite → 1 cópia sempre fora do local físico principal
```

---

