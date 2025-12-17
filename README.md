# AULA DE GIT E GITHUB

## Comandos de git
```bash
# inicializar um repositorio local
git init

# mudar o nome da branch
git branch -M <nome atual> <novo nome>

# listar todas as branchs
git branch

# listar repositorio remoto
git remote

# criar e selecionar uma nova branch
git checkout -b <nome da branch>

# mudar de branch
git checkout <nome da branch>
```

## Trabalhando com repositorio remoto

```bash
# adicionando repositorio remoto
git remote add <nome opcional ou origin> <URL do repositorio remoto>


# sincronizar repositorio remoto com local
git pull <remote> <branch>

# Evitar merge commit
git pull --rebase github main


# utilizando git fetch
# git fetch: Baixa as novidades (refs e objetos) sem mexer no seu código.
# git pull: Baixa E mescla as novidades no seu branch, atualizando seus arquivos.
git fetch <remote> <branch> 

# Envio para o repositorio remoto
git push <remote> <branch>

```