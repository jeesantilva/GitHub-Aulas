

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
# Ver arquivos em conflito
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
# Ver diferenças
git diff

# Ver diferenças do staging
git diff --staged

# Ver quem alterou uma linha
git blame <arquivo>
```

---

## 🧹 Limpeza e Manutenção

```bash
# Remover arquivos não rastreados
git clean -f

# Remover pastas não rastreadas
git clean -fd

# Otimizar repositório
git gc
```

---

## 🏷️ Tags (versões)

```bash
# Criar tag
git tag v1.0.0

# Enviar tags para o remoto
git push origin --tags
```

---

## 🧠 Boas Práticas para o Dia a Dia Frontend

✅ Commits pequenos e claros
✅ Sempre usar `.gitignore`
✅ Atualizar a branch antes de começar (`git pull`)
✅ Usar branches para features e bugs
✅ Nunca commitar `.env`

---

## ✨ Dica Final

> Se algo deu errado, **pare, respire e use `git status`** 😄
> Ele quase sempre te diz o que fazer.

---
