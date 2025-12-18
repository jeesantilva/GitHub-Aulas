

# 🚀 Guia Prático de Git & GitHub

> Anotações pessoais para uso diário como desenvolvedor Frontend

---

## 📌 Antes de tudo: `.gitignore` (NÃO ESQUEÇA ❗)

### 🧠 O que é?

O `.gitignore` é um arquivo que diz ao Git **quais arquivos ou pastas NÃO devem ser versionados**.

👉 Fundamental para evitar subir:

* `node_modules`
* arquivos `.env`
* builds (`dist`, `build`)
* arquivos de sistema (`.DS_Store`)

### 📄 Criando o `.gitignore`

```bash
touch .gitignore
```

### ✍️ Exemplo de `.gitignore` para Frontend

```gitignore
# Dependências
node_modules/

# Build
dist/
build/

# Variáveis de ambiente
.env
.env.local

# Logs
npm-debug.log*
yarn-debug.log*

# Sistema
.DS_Store
```

📌 **Dica:**
Depois de criar ou alterar o `.gitignore`, faça:

```bash
git status
```

---

## 🧩 Conceitos Importantes

* **Working Directory** → seus arquivos locais
* **Staging Area** → arquivos preparados (`git add`)
* **Repository** → histórico salvo (`git commit`)

---

## 🛠️ Comandos Básicos do Git

```bash
# Inicializar um repositório local
git init

# Ver o status do repositório
git status

# Ver histórico de commits
git log
git log --oneline --graph --all

# Adicionar arquivos para staging
git add .
git add <arquivo>

# Criar commit
git commit -m "mensagem do commit"
```

---

## 🌿 Trabalhando com Branches

```bash
# Listar branches locais
git branch

# Criar uma nova branch
git branch <nome-da-branch>

# Criar e já mudar para a branch
git checkout -b <nome-da-branch>

# Mudar de branch
git checkout <nome-da-branch>

# Renomear branch
git branch -M <nome-atual> <novo-nome>

# Deletar branch local
git branch -d <nome-da-branch>
```

---

## 🌐 Repositório Remoto (GitHub)

```bash
# Listar repositórios remotos
git remote
git remote -v

# Adicionar repositório remoto
git remote add origin <URL-do-repositorio>

# Alterar URL do remoto
git remote set-url origin <nova-url>
```

---

## 🔐 Autenticação SSH com GitHub (Repositórios Privados)

Para clonar e trabalhar com **repositórios privados** no GitHub sem precisar digitar usuário e senha, utilizamos **chaves SSH**.

Este guia usa **RSA 4096**, compatível com GitHub e ideal para ambientes Windows.

---

### 🧩 O que é uma chave SSH?

* Uma chave SSH é um **par de arquivos**:

  * 🔑 **Chave privada** → fica **somente na sua máquina**
  * 🔓 **Chave pública** → é cadastrada no GitHub
* O GitHub usa a chave pública para validar que você é realmente você

⚠️ **Nunca compartilhe sua chave privada**.

---

## 🖥️ Gerando uma chave SSH RSA 4096 (Windows + Git Bash)

### 1️⃣ Abrir o Git Bash

```bash
cd ~
```

---

### 2️⃣ Gerar a chave RSA 4096

```bash
ssh-keygen -t rsa -b 4096 -C "email@email.com"
```

Quando solicitado:

```text
Enter file in which to save the key (/c/Users/SEU_USUARIO/.ssh/id_rsa):
```

👉 Pressione **Enter**

```text
Enter passphrase (empty for no passphrase):
```

👉 Pode pressionar **Enter** para não usar senha (opcional).

Arquivos gerados:

* `~/.ssh/id_rsa` → **chave privada**
* `~/.ssh/id_rsa.pub` → **chave pública**

---

## 🔑 Adicionando a chave pública no GitHub

### 3️⃣ Copiar a chave pública

```bash
cat ~/.ssh/id_rsa.pub
```

Copie **toda a linha**, algo como:

```text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQ... email@email.com
```

---

### 4️⃣ Cadastrar no GitHub

1. Acesse: 👉 [https://github.com/settings/keys](https://github.com/settings/keys)
2. Clique em **New SSH key**
3. Preencha:

   * **Title:** Windows - RSA 4096
   * **Key:** cole a chave pública
4. Clique em **Add SSH key**

---

## 🔄 Testando a conexão com o GitHub

### 5️⃣ Testar autenticação SSH

```bash
ssh -T git@github.com
```

Resposta esperada:

```text
Hi SEU-USUARIO! You've successfully authenticated, but GitHub does not provide shell access.
```

📌 Se essa mensagem aparecer, sua chave está configurada corretamente.

---

## 📥 Clonando um repositório privado

### 6️⃣ Clonar usando SSH

```bash
git clone git@github.com:usuario/nome-do-repositorio.git <nome do diretorio>
```

---

## ⚠️ Problemas comuns (SSH)

### ❌ `Permission denied (publickey)`

Normalmente significa que:

* A chave não foi adicionada ao GitHub
* A chave não está carregada no `ssh-agent`
* Você não tem permissão no repositório

Verificar chave carregada:

```bash
ssh-add -l
```

Se necessário:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

---

## 🔄 Sincronização (Pull, Push, Fetch)

```bash
# Enviar código para o repositório remoto
git push origin main

# Primeiro push de uma branch nova
git push -u origin <nome-da-branch>

# Atualizar repositório local
git pull origin main

# Evitar merge commit (mais limpo)
git pull --rebase origin main

# Buscar alterações SEM alterar seu código
git fetch origin
```

📌 **Diferença importante:**

* `git fetch` → só baixa as mudanças
* `git pull` → baixa **e mescla**

---

## ⚔️ Conflitos de Merge (💥 quando dá ruim)

```bash
git status
```

Depois de resolver manualmente:

```bash
git add .
git commit -m "resolvendo conflitos"
```

Se estiver usando rebase:

```bash
git rebase --continue
```

❌ Cancelar merge ou rebase:

```bash
git merge --abort
git rebase --abort
```

---

## ⏪ Desfazer Coisas (Muito Usado!)

```bash
# Remover arquivo do staging
git restore --staged <arquivo>

# Desfazer alterações locais
git restore <arquivo>

# Voltar para o último commit
git reset --hard HEAD

# Voltar para um commit específico
git reset --hard <hash-do-commit>
```

⚠️ **Cuidado:** `--hard` apaga alterações locais!

---

## 🕵️‍♂️ Inspeção e Comparação

```bash
git diff
git diff --staged
git blame <arquivo>
```

---

## 🧹 Limpeza e Manutenção

```bash
git clean -f
git clean -fd
git gc
```

---

## 🏷️ Tags (versões)

```bash
git tag v1.0.0
git push origin --tags
```

---

## 🧠 Boas Práticas para o Dia a Dia Frontend

✅ Commits pequenos e claros
✅ Sempre usar `.gitignore`
✅ Atualizar a branch antes de começar (`git pull`)
✅ Usar branches para features e bugs
✅ Nunca commitar `.env`
✅ Usar SSH para repositórios privados

---

## ✨ Dica Final

> Se algo deu errado, **pare, respire e use `git status`** 😄
> Ele quase sempre te diz o que fazer.


