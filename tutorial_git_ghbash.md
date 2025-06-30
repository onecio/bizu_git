# Tutorial: Automatizando Git e GitHub com Aliases no Git Bash (Windows)

##  Parte 1: Configurar Aliases para Git e GitHub

### Alias 1: `gini`

Este alias executa os seguintes comandos Git em sequência, com pequenas pausas para evitar sobreposição:

```bash
git init                    # Inicializa um repositório Git local
git add .                  # Adiciona todos os arquivos ao staging
git commit -m "Primeiro commit"   # Cria o primeiro commit
```

Mensagem final de sucesso é exibida após os comandos.

### Alias 2: `ghrepo`

Este alias solicita o nome de um projeto e:

```bash
gh repo create <nome_projeto> --public --source=. --remote=origin --push
git remote -v              # Mostra os remotos configurados
```

Depois, imprime um resumo da operação com sucesso ou erro.

### Código a ser adicionado no `~/.bashrc`:

```bash
alias gini='echo "Iniciando repositório Git local..."; sleep 1; git init && sleep 1 && git add . && sleep 1 && git commit -m "Primeiro commit" && echo " Repositório iniciado e commit criado com sucesso!" || echo " Falha na inicialização." && echo "Comandos executados: git init, git add ., git commit"'

alias ghrepo='read -p "Digite o nome do repositório no GitHub: " repo; gh repo create $repo --public --source=. --remote=origin --push && git remote -v && echo " Repositório remoto criado e vinculado com sucesso!" || echo " Falha ao criar o repositório remoto."; echo "Comandos executados: gh repo create $repo, git remote -v"'
```

##  Parte 2: Configurando `.bashrc` e `.bash_profile` no Git Bash (Windows)

### 1. Verifique o diretório HOME

```bash
echo ~
```

Normalmente retorna algo como: `C:/Users/SeuNome`.

### 2. Crie ou edite o arquivo `.bashrc`

```bash
touch ~/.bashrc
nano ~/.bashrc
# ou
notepad ~/.bashrc
```

### 3. Garanta que o `.bashrc` seja carregado

Crie/edite o `.bash_profile`:

```bash
nano ~/.bash_profile
```

Adicione:

```bash
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi
```

### 4. Reinicie o Git Bash

Feche e reabra o terminal para que as alterações tenham efeito.

---

Pronto! Agora você pode usar `gini` para iniciar um projeto e `ghrepo` para subir no GitHub com apenas um comando.
