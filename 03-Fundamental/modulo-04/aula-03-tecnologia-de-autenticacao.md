# 🛡️ Módulo 4 – Controles de Acesso  
## Aula 3 – Tecnologias de Autenticação

---

## 🎯 Objetivos

- Compreender as principais tecnologias de autenticação  
- Entender mecanismos de controle de acesso  
- Conhecer métodos modernos de autenticação segura  

---

## 🧠 Introdução

A autenticação é o processo de verificar a identidade de um usuário ou dispositivo antes de conceder acesso a sistemas e recursos.

Ela é baseada em fatores como:

- Algo que você sabe (senha)
- Algo que você tem (token)
- Algo que você é (biometria)

📌 Quanto mais fatores combinados, maior a segurança.

---

# 🔐 Tecnologias de Autenticação

## 💳 Smart Cards

Cartões físicos com chip usados para autenticação segura.

### Características:
- Armazenam credenciais e certificados  
- Usados em bancos e controle de acesso físico  
- Alta segurança com criptografia  

---

## 🔑 Dispositivos de Gerenciamento de Chaves

Hardware dedicado para operações criptográficas.

### Funções:
- Gerar e armazenar chaves criptográficas  
- Criar certificados digitais  
- Proteger informações sensíveis  

---

## 🌐 IEEE 802.1X

Protocolo de autenticação de rede.

### Componentes:
- Suplicante (usuário/dispositivo)
- Autenticador (switch/AP)
- Servidor de autenticação

📌 Usado para controlar acesso a redes corporativas. 

---

## 📡 RADIUS

Protocolo de autenticação centralizada.

### Funcionamento:
- Cliente envia solicitação  
- Servidor valida credenciais  
- Retorna acesso permitido ou negado  

📌 Muito usado em redes corporativas e Wi-Fi.

---

## 🖥️ Controle de Acesso Terminal

Gerencia acesso a sistemas e dispositivos.

### Aplicações:
- Ambientes industriais  
- Cloud  
- Infraestruturas críticas  

---

# 🔢 Tokens e Códigos

## 🔐 Tokens

Dispositivos ou apps que geram códigos de autenticação.

### Exemplos:
- Google Authenticator  
- RSA SecurID 

---

## 🔑 Códigos Estáticos

- Senhas fixas  
- Menos seguros  
- Usados como backup  

---

## ⏱️ HOTP e TOTP

### HOTP (Counter-based)
- Baseado em contador  

### TOTP (Time-based)
- Baseado no tempo  
- Mais seguro e comum  

📌 Amplamente usados em autenticação em dois fatores (2FA). :contentReference[oaicite:3]{index=3}  

---

# 🔐 Autenticação em Dois Fatores (2FA)

Combinação de dois métodos de autenticação.

### Exemplos:
- Senha + código do celular  
- Senha + biometria  

### Benefícios:
- Reduz risco de invasão  
- Protege contas mesmo com senha vazada  

---

# 📌 Boas Práticas

- Usar MFA sempre que possível  
- Evitar senhas fracas  
- Proteger dispositivos de autenticação  
- Implementar autenticação forte em ambientes críticos  

---

## 📌 Conclusão

As tecnologias de autenticação são fundamentais para proteger acessos em sistemas modernos.

✔️ Smart cards e tokens aumentam a segurança  
✔️ Protocolos como RADIUS e 802.1X controlam redes  
✔️ 2FA/MFA reduzem drasticamente riscos de invasão  

🔐 Autenticação forte é a primeira linha de defesa contra ataques.

---
