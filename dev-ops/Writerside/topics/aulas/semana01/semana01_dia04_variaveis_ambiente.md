# Aula 4: Variáveis de Ambiente e Customização do Shell

## 📚 Conceitos Fundamentais

### O que são Variáveis de Ambiente?
Variáveis de ambiente são como "configurações globais" do seu sistema. Elas armazenam informações que programas e scripts podem usar.

**Analogia:** Pense em variáveis de ambiente como notas adesivas em um quadro de avisos da sua casa. Qualquer pessoa (programa) pode ler essas notas para saber informações importantes como "Onde fica a ferramenta X?" ou "Qual é o idioma padrão?".

**No DevOps:** Variáveis de ambiente são cruciais para:
- Configurar aplicações sem alterar código
- Armazenar credenciais (API keys, senhas de banco)
- Definir diferentes comportamentos (dev, staging, prod)
- Customizar ferramentas (Docker, kubectl, aws-cli)

---

## 🎯 Trabalhando com Variáveis

### Ver Variáveis de Ambiente

```bash
# Listar TODAS as variáveis
env
# ou
printenv

# Ver variável específica
echo $HOME
echo $USER
echo $PATH
echo $SHELL

# Ver com printenv
printenv HOME
printenv PATH
```

**Variáveis importantes:**
- `$HOME` - Diretório home do usuário (/home/usuario)
- `$USER` - Nome do usuário atual
- `$PATH` - Onde o sistema busca comandos
- `$SHELL` - Shell padrão (/bin/bash)
- `$PWD` - Diretório atual
- `$OLDPWD` - Diretório anterior
- `$LANG` - Idioma do sistema

---

### Criar Variáveis

```bash
# Variável local (só nesta sessão)
NOME="João"
echo $NOME

# Exportar (torna global para processos filhos)
export NOME="João"

# Criar e exportar em uma linha
export DATABASE_URL="postgresql://localhost:5432/mydb"

# Múltiplas variáveis
export API_KEY="abc123"
export API_SECRET="xyz789"
export AMBIENTE="desenvolvimento"
```

**Diferença importante:**
```bash
# LOCAL (não herdada por scripts/programas)
VARIAVEL="valor"

# GLOBAL (herdada por processos filhos)
export VARIAVEL="valor"
```

---

### A Variável PATH

**A mais importante!** PATH define onde o sistema busca comandos.

```bash
# Ver PATH atual
echo $PATH
# Saída: /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

# Adicionar diretório ao PATH (temporário)
export PATH=$PATH:/novo/diretorio

# Adicionar no INÍCIO do PATH (prioridade)
export PATH=/novo/diretorio:$PATH

# Exemplo real: Adicionar scripts pessoais
mkdir -p ~/scripts
export PATH=$PATH:~/scripts
```

**Como PATH funciona:**
Quando você digita `ls`, o sistema busca nesta ordem:
1. `/usr/local/bin/ls` (não encontrou)
2. `/usr/bin/ls` (ENCONTROU! executa este)

---

## 📁 Arquivos de Configuração do Shell

### Diferença entre os arquivos

```bash
~/.bashrc          # Executa em TODA nova sessão de terminal
~/.bash_profile    # Executa apenas no LOGIN
~/.profile         # Alternativa ao .bash_profile (mais genérico)
~/.bash_logout     # Executa ao SAIR do terminal
```

**Regra prática:**
- Coloque configurações em `~/.bashrc` (sempre funciona)
- Em sistemas macOS, use `~/.bash_profile` ou `~/.zshrc`

---

### Customizar ~/.bashrc

```bash
# Editar .bashrc
nano ~/.bashrc

# Adicione no final do arquivo:

# ===== VARIÁVEIS DE AMBIENTE =====
export EDITOR=vim
export VISUAL=vim
export HISTSIZE=10000
export HISTFILESIZE=20000

# ===== ALIASES =====
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'

# Aliases DevOps
alias dc='docker-compose'
alias k='kubectl'
alias tf='terraform'
alias logs='tail -f /var/log/syslog'

# ===== FUNÇÕES =====
# Criar e entrar em diretório
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extrair qualquer arquivo compactado
extract() {
    if [ -f $1 ]; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *)           echo "'$1' não pode ser extraído" ;;
        esac
    else
        echo "'$1' não é um arquivo válido"
    fi
}

# ===== PROMPT CUSTOMIZADO =====
# PS1 = como o prompt aparece
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ "

# ===== PATH =====
export PATH=$PATH:~/scripts:~/bin

# Aplicar mudanças SEM reiniciar terminal
source ~/.bashrc
```

---

### Prompt (PS1) Customizado

```bash
# Elementos do PS1:
# \u = nome do usuário
# \h = hostname
# \w = diretório completo
# \W = apenas nome do diretório atual
# \$ = $ (user normal) ou # (root)
# \t = hora (HH:MM:SS)
# \d = data

# Exemplos de prompts:

# Simples
export PS1="\u@\h:\w\$ "
# Saída: usuario@servidor:/home/usuario/projetos$

# Com cores
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ "

# Com Git branch (avançado)
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[01;31m\]\$(parse_git_branch)\[\033[00m\]\$ "
```

---

## 🐳 Variáveis para DevOps

### Docker

```bash
# Variáveis Docker
export DOCKER_HOST=unix:///var/run/docker.sock
export DOCKER_BUILDKIT=1  # Habilita BuildKit
export COMPOSE_DOCKER_CLI_BUILD=1
```

### Kubernetes

```bash
# Kubeconfig
export KUBECONFIG=~/.kube/config

# Namespace padrão
export KUBECTL_NAMESPACE=production

# Aliases úteis
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias kdp='kubectl describe pod'
```

### AWS

```bash
# Credenciais AWS
export AWS_ACCESS_KEY_ID="sua-key-id"
export AWS_SECRET_ACCESS_KEY="sua-secret-key"
export AWS_DEFAULT_REGION="us-east-1"
export AWS_PROFILE="production"
```

### Aplicações

```bash
# Node.js
export NODE_ENV=production
export PORT=3000

# Python
export PYTHONPATH=/opt/myapp
export FLASK_ENV=development

# Java
export JAVA_HOME=/usr/lib/jvm/java-11
export PATH=$PATH:$JAVA_HOME/bin

# Go
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

---

## 🔐 Variáveis Sensíveis

### NUNCA faça isso:

```bash
# ❌ ERRADO - expõe senha no histórico
export DB_PASSWORD="senha123"

# ❌ ERRADO - commit no Git
echo 'export API_KEY="abc123"' >> ~/.bashrc
git add ~/.bashrc
```

### Forma CORRETA:

```bash
# ✅ Use arquivo separado para secrets
touch ~/.env
chmod 600 ~/.env  # Apenas você pode ler

# Editar ~/.env
nano ~/.env
# Adicione:
# export DB_PASSWORD="senha123"
# export API_KEY="abc123"

# Carregar no ~/.bashrc
echo 'source ~/.env' >> ~/.bashrc

# OU use ferramentas como:
# - AWS Secrets Manager
# - HashiCorp Vault
# - Kubernetes Secrets
# - Docker Secrets
```

---

## 🤔 Perguntas Socráticas

1. **Por que usar `export` em vez de apenas criar a variável?**
   - Resposta: `export` torna a variável disponível para processos filhos (scripts e programas).

2. **O que acontece se você adicionar um diretório inexistente ao PATH?**
   - Resposta: Nada de grave, mas comandos desse diretório não serão encontrados.

3. **Por que ~/.bashrc é melhor que ~/.bash_profile para aliases?**
   - Resposta: .bashrc é executado em TODA nova sessão, .bash_profile só no login.

4. **Como você tornaria uma variável permanente?**
   - Resposta: Adicionar `export VARIAVEL=valor` no ~/.bashrc

5. **Por que é perigoso colocar senhas em variáveis de ambiente?**
   - Resposta: Elas ficam em texto puro, aparecem no histórico e podem vazar em logs.

---

## 💪 Exercício Prático

### Desafio 1: Customizar Ambiente

```bash
# 1. Backup do .bashrc atual
cp ~/.bashrc ~/.bashrc.backup

# 2. Adicionar aliases úteis
cat >> ~/.bashrc << 'EOF'

# Aliases DevOps
alias dps='docker ps'
alias dimg='docker images'
alias dcup='docker-compose up -d'
alias dcdown='docker-compose down'
alias dclog='docker-compose logs -f'

# Navegação
alias ..='cd ..'
alias ...='cd ../..'
alias ll='ls -lah'

# Git shortcuts
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git log --oneline'

# Função útil
mkcd() {
    mkdir -p "$1" && cd "$1"
}
EOF

# 3. Recarregar
source ~/.bashrc

# 4. Testar
mkcd ~/teste
ll
dps
```

---

### Desafio 2: Configurar Projeto Node.js

```bash
# 1. Criar estrutura
mkdir -p ~/projeto-node/{src,config}
cd ~/projeto-node

# 2. Criar arquivo .env
cat > .env << EOF
NODE_ENV=development
PORT=3000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp
DB_USER=postgres
DB_PASSWORD=senha123
API_KEY=abc123xyz
EOF

# 3. Proteger .env
chmod 600 .env

# 4. Criar script para carregar variáveis
cat > load-env.sh << 'EOF'
#!/bin/bash
if [ -f .env ]; then
    export $(cat .env | grep -v '^#' | xargs)
    echo "Variáveis carregadas!"
else
    echo "Arquivo .env não encontrado!"
fi
EOF

chmod +x load-env.sh

# 5. Usar
source ./load-env.sh
echo $NODE_ENV
echo $PORT
```

---

### Desafio 3: PATH Personalizado

```bash
# 1. Criar diretório de scripts
mkdir -p ~/bin

# 2. Criar script útil
cat > ~/bin/backup-projeto << 'EOF'
#!/bin/bash
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
tar -czf ~/backups/projeto_${TIMESTAMP}.tar.gz ~/projeto
echo "Backup criado: projeto_${TIMESTAMP}.tar.gz"
EOF

chmod +x ~/bin/backup-projeto

# 3. Adicionar ao PATH
echo 'export PATH=$PATH:~/bin' >> ~/.bashrc
source ~/.bashrc

# 4. Testar (de qualquer diretório)
cd /tmp
backup-projeto  # Funciona!
```

---

## ✅ Mini-Quiz de Revisão

**1. Qual a diferença entre variável local e exportada?**
<details>
<summary>Resposta</summary>
Local só existe na sessão atual. Exportada é herdada por processos filhos.
</details>

**2. Onde adicionar aliases permanentes?**
<details>
<summary>Resposta</summary>
No arquivo ~/.bashrc
</details>

**3. Como recarregar .bashrc sem fechar o terminal?**
<details>
<summary>Resposta</summary>
`source ~/.bashrc` ou `. ~/.bashrc`
</details>

**4. O que faz `export PATH=$PATH:/novo/dir`?**
<details>
<summary>Resposta</summary>
Adiciona /novo/dir ao final do PATH (menor prioridade)
</details>

**5. Por que usar chmod 600 em arquivos .env?**
<details>
<summary>Resposta</summary>
Para que apenas o dono possa ler/escrever, protegendo secrets.
</details>

---

## 📹 Recursos de Vídeo

1. **Variáveis de Ambiente no Linux**
   - https://www.youtube.com/watch?v=0NVt5wvXS-g

2. **Customizar Terminal Linux**
   - https://www.youtube.com/watch?v=PjAC9K53TM0

3. **Arquivo .bashrc Explicado**
   - https://www.youtube.com/watch?v=oxuRxtrO2Ag

4. **PATH no Linux**
   - https://www.youtube.com/watch?v=2cCqy15izLU

5. **Aliases e Funções Bash**
   - https://www.youtube.com/watch?v=Y_IROdWD3cg

---

## 🎯 Aplicação no Mundo Real

### Cenário: Deploy de Aplicação com Variáveis

```bash
# 1. Arquivo de configuração por ambiente

# config/development.env
NODE_ENV=development
DEBUG=true
DB_HOST=localhost
DB_PORT=5432
LOG_LEVEL=debug
API_URL=http://localhost:3000

# config/production.env
NODE_ENV=production
DEBUG=false
DB_HOST=prod-db.example.com
DB_PORT=5432
LOG_LEVEL=error
API_URL=https://api.example.com

# 2. Script de deploy
cat > deploy.sh << 'EOF'
#!/bin/bash

ENVIRONMENT=$1

if [ -z "$ENVIRONMENT" ]; then
    echo "Uso: ./deploy.sh [development|production]"
    exit 1
fi

# Carregar variáveis do ambiente
if [ -f "config/${ENVIRONMENT}.env" ]; then
    export $(cat config/${ENVIRONMENT}.env | grep -v '^#' | xargs)
    echo "✅ Variáveis do ambiente ${ENVIRONMENT} carregadas"
else
    echo "❌ Arquivo config/${ENVIRONMENT}.env não encontrado"
    exit 1
fi

# Verificar variáveis críticas
if [ -z "$DB_HOST" ] || [ -z "$API_URL" ]; then
    echo "❌ Variáveis críticas não definidas"
    exit 1
fi

echo "🚀 Fazendo deploy para ${ENVIRONMENT}"
echo "   DB_HOST: $DB_HOST"
echo "   API_URL: $API_URL"
echo "   LOG_LEVEL: $LOG_LEVEL"

# Aqui viria o código real de deploy
# docker-compose up -d
# kubectl apply -f deployment.yml
# etc.
EOF

chmod +x deploy.sh

# 3. Usar
./deploy.sh development
./deploy.sh production
```

---

## 📝 Resumo da Aula

Você aprendeu:
- ✅ O que são variáveis de ambiente e por que são importantes
- ✅ Criar e exportar variáveis
- ✅ Manipular a variável PATH
- ✅ Customizar ~/.bashrc com aliases e funções
- ✅ Personalizar o prompt (PS1)
- ✅ Gerenciar variáveis sensíveis de forma segura
- ✅ Configurar ambientes para diferentes projetos

**Próxima aula:** Editores de Texto (Vim e Nano)

---

## 💡 Dicas Profissionais

### 1. Arquivo ~/.bashrc Completo para DevOps

```bash
# ~/.bashrc otimizado

# ===== HISTÓRICO =====
HISTSIZE=10000
HISTFILESIZE=20000
HISTCONTROL=ignoredups:erasedups
shopt -s histappend

# ===== EDITOR =====
export EDITOR=vim
export VISUAL=vim

# ===== ALIASES =====
# Sistema
alias ll='ls -lah'
alias la='ls -A'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias mkdir='mkdir -pv'

# Git
alias gs='git status'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gl='git log --oneline --graph'
alias gco='git checkout'
alias gb='git branch'

# Docker
alias d='docker'
alias dc='docker-compose'
alias dps='docker ps'
alias dimg='docker images'
alias drm='docker rm $(docker ps -aq)'
alias drmi='docker rmi $(docker images -q)'

# Kubernetes
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias kgd='kubectl get deployments'
alias kdesc='kubectl describe'
alias klogs='kubectl logs -f'

# ===== FUNÇÕES =====
# Criar e entrar em diretório
mkcd() { mkdir -p "$1" && cd "$1"; }

# Backup rápido
backup() { cp "$1"{,.bak}; }

# Extrair arquivos
extract() {
    if [ -f $1 ]; then
        case $1 in
            *.tar.bz2) tar xjf $1 ;;
            *.tar.gz)  tar xzf $1 ;;
            *.tar.xz)  tar xJf $1 ;;
            *.bz2)     bunzip2 $1 ;;
            *.rar)     unrar e $1 ;;
            *.gz)      gunzip $1 ;;
            *.tar)     tar xf $1 ;;
            *.tbz2)    tar xjf $1 ;;
            *.tgz)     tar xzf $1 ;;
            *.zip)     unzip $1 ;;
            *.Z)       uncompress $1 ;;
            *.7z)      7z x $1 ;;
            *)         echo "'$1' não pode ser extraído" ;;
        esac
    else
        echo "'$1' não é um arquivo válido"
    fi
}

# ===== PROMPT =====
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[01;31m\]\$(parse_git_branch)\[\033[00m\]\$ "

# ===== PATH =====
export PATH=$PATH:~/bin:~/scripts

# ===== FERRAMENTAS DEVOPS =====
# Docker
export DOCKER_BUILDKIT=1
export COMPOSE_DOCKER_CLI_BUILD=1

# Kubernetes
export KUBECONFIG=~/.kube/config

# Carregar secrets (se existir)
[ -f ~/.env ] && source ~/.env
```

---

## 🔥 Desafio Final

**Você está pronto se conseguir:**

1. Criar um sistema de aliases para seus projetos mais usados
2. Configurar variáveis de ambiente para 3 ambientes diferentes
3. Criar uma função bash que automatiza uma tarefa repetitiva
4. Adicionar um diretório personalizado ao PATH
5. Customizar seu prompt com cores e informações úteis

**Teste prático:**
Crie um ambiente completo para um projeto com:
- Aliases para comandos comuns
- Variáveis de configuração
- Função para trocar entre ambientes
- Prompt mostrando o ambiente atual

---

**🚀 Dominou variáveis e customização? Próxima aula: Editores de Texto!**
