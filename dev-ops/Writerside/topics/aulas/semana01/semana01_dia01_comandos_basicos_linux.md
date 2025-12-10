# Aula 1: Comandos Básicos do Linux

## 📚 Conceitos Fundamentais

### O que é o Linux?
O Linux é um sistema operacional de código aberto baseado em Unix. Diferente do Windows ou macOS, o Linux oferece controle total sobre o sistema através da linha de comando (terminal). Pense no terminal como uma conversa direta com o computador - você dá comandos em texto e ele responde.

**Analogia do mundo real:** Imagine que você está dirigindo um carro. No Windows/Mac, você tem um painel automático (interface gráfica). No Linux, você tem acesso direto ao motor e pode ajustar cada peça manualmente.

### Sistema de Arquivos Linux
O Linux organiza tudo em uma estrutura de árvore que começa na raiz `/`:
- `/home` - Diretório dos usuários (como "Meus Documentos")
- `/etc` - Arquivos de configuração do sistema
- `/var` - Dados variáveis (logs, cache)
- `/usr` - Programas e bibliotecas
- `/tmp` - Arquivos temporários

---

## 🎯 Comandos Essenciais

### 1. pwd (Print Working Directory)
**Conceito:** Mostra onde você está no sistema de arquivos.

```bash
pwd
# Saída: /home/usuario
```

**Analogia:** É como perguntar "Onde estou?" em um shopping.

---

### 2. ls (List)
**Conceito:** Lista arquivos e diretórios.

```bash
# Básico
ls

# Com detalhes
ls -l

# Incluindo arquivos ocultos
ls -a

# Combinando opções
ls -lah
```

**Analogia:** Como abrir uma gaveta e ver o que tem dentro.

---

### 3. cd (Change Directory)
**Conceito:** Navega entre diretórios.

```bash
# Entrar em um diretório
cd Documents

# Voltar um nível
cd ..

# Ir para home
cd ~

# Voltar ao diretório anterior
cd -
```

**Analogia:** Como andar por diferentes cômodos de uma casa.

---

### 4. mkdir (Make Directory)
**Conceito:** Cria novos diretórios.

```bash
# Criar um diretório
mkdir projetos

# Criar estrutura aninhada
mkdir -p projetos/devops/docker
```

---

### 5. touch
**Conceito:** Cria arquivos vazios ou atualiza data de modificação.

```bash
touch arquivo.txt
touch script.sh config.yml
```

---

### 6. cp (Copy)
**Conceito:** Copia arquivos e diretórios.

```bash
# Copiar arquivo
cp origem.txt destino.txt

# Copiar diretório recursivamente
cp -r pasta_origem pasta_destino

# Copiar preservando atributos
cp -p arquivo.txt backup/
```

---

### 7. mv (Move)
**Conceito:** Move ou renomeia arquivos.

```bash
# Renomear
mv nome_antigo.txt nome_novo.txt

# Mover para outro diretório
mv arquivo.txt /home/usuario/Documents/

# Mover múltiplos arquivos
mv *.txt Documents/
```

---

### 8. rm (Remove)
**Conceito:** Remove arquivos e diretórios.

```bash
# Remover arquivo
rm arquivo.txt

# Remover diretório vazio
rmdir pasta_vazia

# Remover diretório com conteúdo
rm -r pasta_com_arquivos

# Remover forçadamente (cuidado!)
rm -rf pasta
```

**⚠️ ATENÇÃO:** `rm -rf` é destrutivo e permanente!

---

### 9. cat (Concatenate)
**Conceito:** Exibe conteúdo de arquivos.

```bash
# Ver conteúdo
cat arquivo.txt

# Concatenar múltiplos arquivos
cat arquivo1.txt arquivo2.txt

# Criar arquivo com conteúdo
cat > novo.txt
# (digite o conteúdo e pressione Ctrl+D)
```

---

### 10. Permissões
**Conceito:** Controla quem pode ler, escrever ou executar arquivos.

```bash
# Ver permissões
ls -l
# -rwxr-xr-- 1 usuario grupo

# r (read) = 4
# w (write) = 2
# x (execute) = 1

# Mudar permissões
chmod 755 script.sh  # rwxr-xr-x
chmod +x script.sh   # adiciona execução

# Mudar dono
chown usuario:grupo arquivo.txt
```

**Interpretando permissões:**
- `rwx` (owner) = dono pode ler, escrever e executar
- `r-x` (group) = grupo pode ler e executar
- `r--` (others) = outros só podem ler

---

## 🤔 Perguntas Socráticas

1. **Por que você acha que o Linux usa `/` em vez de `\` como o Windows?**
   - Resposta: Unix foi criado antes, e o padrão se manteve. O `\` é usado como escape.

2. **O que aconteceria se você executasse `rm -rf /` como root?**
   - Resposta: Deletaria todo o sistema! Por isso nunca use root sem necessidade.

3. **Por que arquivos ocultos começam com `.` no Linux?**
   - Resposta: Convenção para arquivos de configuração que não devem aparecer normalmente.

4. **Qual a diferença entre `cp` e `mv`?**
   - Resposta: `cp` duplica mantendo o original; `mv` transfere o arquivo.

5. **Por que permissões são importantes em servidores?**
   - Resposta: Segurança! Evita que usuários modifiquem arquivos críticos do sistema.

---

## 💪 Exercício Prático

### Desafio: Criar Estrutura de Projeto DevOps

```bash
# 1. Crie a estrutura de diretórios
mkdir -p ~/devops-project/{docker,kubernetes,terraform,scripts}

# 2. Navegue até o diretório
cd ~/devops-project

# 3. Crie arquivos de exemplo
touch docker/Dockerfile
touch kubernetes/deployment.yml
touch terraform/main.tf
touch scripts/deploy.sh

# 4. Dê permissão de execução ao script
chmod +x scripts/deploy.sh

# 5. Liste toda a estrutura
ls -lR

# 6. Copie a estrutura para backup
cp -r ~/devops-project ~/devops-project-backup

# 7. Verifique o resultado
tree ~/devops-project  # (instale com: sudo apt install tree)
```

---

## ✅ Verificação de Conhecimento

**Você está pronto para avançar se conseguir:**

1. Navegar entre diretórios usando apenas o terminal
2. Criar, copiar, mover e deletar arquivos sem medo
3. Entender e modificar permissões básicas
4. Explicar a estrutura de diretórios do Linux

**Teste rápido:**
```bash
# Sem olhar os comandos acima, tente:
# 1. Criar um diretório chamado "teste"
# 2. Entrar nele
# 3. Criar 3 arquivos .txt
# 4. Dar permissão de execução para um arquivo
# 5. Listar com detalhes
# 6. Voltar e deletar tudo
```

**Conseguiu? ✅ Próxima aula!**
**Teve dificuldades? 🔄 Revise os conceitos acima.**

---

## 📹 Recursos de Vídeo

1. **Linux Básico para Iniciantes (Português)**
   - https://www.youtube.com/watch?v=JEhVB4VHsTI

2. **Comandos Linux Essenciais**
   - https://www.youtube.com/watch?v=oxuRxtrO2Ag

3. **Terminal Linux do Zero**
   - https://www.youtube.com/watch?v=Sf8M9SSgHZE

4. **Permissões no Linux Explicadas**
   - https://www.youtube.com/watch?v=4e669hSjaX8

5. **Curso Completo Linux - Introdução**
   - https://www.youtube.com/watch?v=WMy3OzvBWc0

---

## 🎯 Aplicação no Mundo Real

**Cenário DevOps:** Você precisa fazer deploy de uma aplicação em um servidor Linux.

1. **Conectar ao servidor:** `ssh usuario@servidor`
2. **Navegar até o diretório:** `cd /var/www/app`
3. **Fazer backup:** `cp -r app app_backup_$(date +%Y%m%d)`
4. **Baixar nova versão:** `git pull origin main`
5. **Ajustar permissões:** `chmod 755 scripts/*.sh`
6. **Verificar logs:** `cat /var/log/app.log`

**Viu como os comandos básicos são fundamentais no dia a dia?**

---

## 📝 Resumo da Aula

Você aprendeu:
- ✅ Navegação no sistema de arquivos (pwd, cd, ls)
- ✅ Manipulação de arquivos (touch, cp, mv, rm, cat)
- ✅ Criação de diretórios (mkdir)
- ✅ Sistema de permissões (chmod, chown)
- ✅ Estrutura do Linux (/, /home, /etc, /var)

**Próxima aula:** Manipulação de Arquivos e Editores de Texto

---

## 💡 Dicas Profissionais

1. **Use Tab para autocompletar** - economiza tempo e evita erros
2. **Use setas ↑↓** - navega no histórico de comandos
3. **Ctrl+C** - cancela comando em execução
4. **Ctrl+L** - limpa a tela (ou digite `clear`)
5. **man comando** - abre o manual de qualquer comando
6. **comando --help** - ajuda rápida

---

**🚀 Pronto para a próxima aula? Primeiro pratique esse exercício!**
