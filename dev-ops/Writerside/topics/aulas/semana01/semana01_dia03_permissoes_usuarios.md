# Aula 3: Permissões e Usuários no Linux

## 📚 Conceitos Fundamentais

### Por que permissões são críticas?
Linux é um sistema multiusuário. Imagine um prédio com vários apartamentos - você não quer que qualquer pessoa possa entrar no seu apartamento, certo? Permissões fazem isso no Linux: definem quem pode fazer o quê com cada arquivo.

**No mundo DevOps:** Um erro de permissão pode:
- Permitir que hackers acessem dados sensíveis
- Impedir que aplicações funcionem corretamente
- Causar problemas de segurança graves

**Analogia:** Permissões são como as chaves de um prédio:
- **Proprietário (owner):** Dono do apartamento - acesso total
- **Grupo (group):** Família - acesso compartilhado
- **Outros (others):** Visitantes - acesso limitado

---

## 🔐 Sistema de Permissões

### Entendendo rwx

Quando você executa `ls -l`, vê algo assim:
```
-rwxr-xr-- 1 usuario grupo 1234 Jan 15 10:00 arquivo.txt
```

Vamos decodificar:

```
- rwx r-x r--
│ │││ │││ │││
│ │││ │││ └└└─ Outros (Others): r-- = leitura apenas
│ │││ └└└───── Grupo (Group): r-x = leitura + execução
│ └└└───────── Dono (Owner): rwx = leitura + escrita + execução
└───────────── Tipo: - (arquivo) ou d (diretório)
```

### Significado de cada letra:
- **r** (read/leitura): pode ver o conteúdo
- **w** (write/escrita): pode modificar
- **x** (execute/execução): pode executar (scripts/programas) ou entrar (diretórios)

---

## 🎯 Comando chmod (Change Mode)

### Forma Simbólica (mais intuitiva)

```bash
# Adicionar permissão
chmod u+x script.sh      # Dono pode executar
chmod g+w arquivo.txt    # Grupo pode escrever
chmod o+r dados.txt      # Outros podem ler
chmod a+x script.sh      # Todos (all) podem executar

# Remover permissão
chmod u-x script.sh      # Remove execução do dono
chmod g-w arquivo.txt    # Remove escrita do grupo
chmod o-r dados.txt      # Remove leitura dos outros

# Definir permissão exata
chmod u=rwx arquivo.txt  # Dono: rwx
chmod g=rx arquivo.txt   # Grupo: r-x
chmod o=r arquivo.txt    # Outros: r--

# Combinar
chmod u+x,g-w,o-r script.sh
```

**Onde:**
- `u` = user (dono)
- `g` = group (grupo)
- `o` = others (outros)
- `a` = all (todos)

---

### Forma Numérica (mais comum em DevOps)

Cada permissão tem um valor:
- **r** = 4
- **w** = 2
- **x** = 1

Soma os valores para cada categoria:

```
rwx = 4+2+1 = 7
rw- = 4+2+0 = 6
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
-wx = 0+2+1 = 3
-w- = 0+2+0 = 2
--x = 0+0+1 = 1
--- = 0+0+0 = 0
```

**Exemplos práticos:**

```bash
# 755 = rwxr-xr-x (padrão para executáveis)
chmod 755 script.sh
# Dono: 7(rwx), Grupo: 5(r-x), Outros: 5(r-x)

# 644 = rw-r--r-- (padrão para arquivos)
chmod 644 config.txt
# Dono: 6(rw-), Grupo: 4(r--), Outros: 4(r--)

# 600 = rw------- (arquivos privados)
chmod 600 senha.txt
# Dono: 6(rw-), Grupo: 0(---), Outros: 0(---)

# 777 = rwxrwxrwx (EVITE! Muito permissivo)
chmod 777 arquivo.txt  # ❌ NUNCA faça isso em produção!

# 700 = rwx------ (executável privado)
chmod 700 backup.sh

# 400 = r-------- (só leitura, somente dono)
chmod 400 api-key.txt
```

---

### Permissões em Diretórios

Para diretórios, as permissões funcionam diferente:
- **r** = listar conteúdo (ls)
- **w** = criar/deletar arquivos dentro
- **x** = entrar no diretório (cd)

```bash
# Criar diretório e ajustar permissões
mkdir projeto
chmod 755 projeto  # Todos podem entrar e listar, só dono pode modificar

# Recursivo (aplica em tudo dentro)
chmod -R 755 /var/www/html
```

---

## 👥 Gerenciamento de Usuários

### Comando chown (Change Owner)

```bash
# Mudar dono
chown usuario arquivo.txt

# Mudar dono e grupo
chown usuario:grupo arquivo.txt

# Recursivo
chown -R usuario:grupo /var/www/

# Apenas grupo
chgrp grupo arquivo.txt
```

**Exemplo real - Deploy de aplicação:**
```bash
# Aplicação deve pertencer ao usuário www-data
sudo chown -R www-data:www-data /var/www/app
sudo chmod -R 755 /var/www/app
```

---

### Gerenciando Usuários do Sistema

```bash
# Criar usuário
sudo useradd -m -s /bin/bash devops
# -m = cria home directory
# -s = define shell

# Definir senha
sudo passwd devops

# Adicionar usuário a grupo
sudo usermod -aG docker devops
# -a = append (adicionar)
# -G = grupo

# Ver grupos do usuário
groups devops

# Criar grupo
sudo groupadd developers

# Deletar usuário
sudo userdel devops
sudo userdel -r devops  # remove home directory também

# Listar usuários
cat /etc/passwd

# Listar grupos
cat /etc/group
```

---

## 🔑 Comando sudo

### O que é sudo?
**Su**peruser **Do** = Fazer como superusuário (root)

```bash
# Executar comando como root
sudo apt update

# Trocar para root temporariamente
sudo su

# Executar como outro usuário
sudo -u www-data whoami

# Ver permissões de sudo
sudo -l

# Editar arquivo de configuração (CUIDADO!)
sudo visudo
```

**⚠️ IMPORTANTE:** 
- Use `sudo` apenas quando necessário
- NUNCA execute scripts desconhecidos com `sudo`
- `sudo rm -rf /` pode destruir todo o sistema!

---

## 🤔 Perguntas Socráticas

1. **Por que `chmod 777` é perigoso em produção?**
   - Resposta: Qualquer usuário pode modificar/executar o arquivo. Risco de segurança enorme!

2. **O que significa `chmod 600 ~/.ssh/id_rsa`?**
   - Resposta: Apenas o dono pode ler/escrever a chave SSH privada. Ninguém mais tem acesso.

3. **Por que diretórios precisam de permissão `x`?**
   - Resposta: Sem `x`, você não consegue entrar no diretório com `cd`.

4. **Qual a diferença entre `755` e `777`?**
   - 755: Dono pode tudo, outros só leem/executam (SEGURO)
   - 777: Todos podem fazer tudo (PERIGOSO)

5. **Quando você adicionaria um usuário ao grupo `docker`?**
   - Resposta: Para permitir que execute comandos Docker sem sudo.

---

## 💪 Exercício Prático

### Desafio: Configurar Ambiente Seguro de Aplicação

```bash
# 1. Criar estrutura de diretórios
mkdir -p ~/app/{src,config,logs,data}
cd ~/app

# 2. Criar arquivos de exemplo
touch src/app.py
touch config/database.yml
touch config/api-keys.txt
touch logs/app.log

# 3. Configurar permissões corretas

# Scripts devem ser executáveis
chmod 755 src/app.py

# Configs devem ser legíveis pelo grupo, mas não por outros
chmod 640 config/database.yml

# API keys só para o dono
chmod 600 config/api-keys.txt

# Logs podem ser lidos pelo grupo
chmod 644 logs/app.log

# 4. Criar usuário de aplicação
sudo useradd -m -s /bin/bash appuser

# 5. Criar grupo de desenvolvedores
sudo groupadd developers

# 6. Adicionar usuário ao grupo
sudo usermod -aG developers appuser

# 7. Mudar ownership
sudo chown -R appuser:developers ~/app

# 8. Verificar resultado
ls -lR ~/app

# 9. Testar acesso
sudo -u appuser cat ~/app/config/api-keys.txt  # deve funcionar
cat ~/app/config/api-keys.txt  # deve falhar se você não é o dono
```

---

### Desafio Extra: Cenário Real SSH

```bash
# Configurar chaves SSH corretamente

# 1. Criar diretório .ssh
mkdir -p ~/.ssh
chmod 700 ~/.ssh

# 2. Gerar par de chaves
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa

# 3. Permissões corretas (CRÍTICO!)
chmod 600 ~/.ssh/id_rsa          # Chave privada
chmod 644 ~/.ssh/id_rsa.pub      # Chave pública
chmod 600 ~/.ssh/authorized_keys # Chaves autorizadas
chmod 600 ~/.ssh/config          # Configuração SSH

# 4. Verificar
ls -la ~/.ssh/
```

**Por que essas permissões?**
- `700` no diretório: Só você pode entrar
- `600` na chave privada: Só você pode ler (NUNCA compartilhe!)
- SSH recusa chaves com permissões erradas por segurança

---

## ✅ Mini-Quiz de Revisão

**1. O que significa `chmod 644 arquivo.txt`?**
<details>
<summary>Resposta</summary>
Dono pode ler e escrever (6=rw-), grupo e outros só podem ler (4=r--)
</details>

**2. Como dar permissão de execução para todos?**
<details>
<summary>Resposta</summary>
`chmod +x arquivo` ou `chmod a+x arquivo` ou `chmod 755 arquivo`
</details>

**3. Como mudar o dono de um arquivo para o usuário 'nginx'?**
<details>
<summary>Resposta</summary>
`sudo chown nginx arquivo.txt`
</details>

**4. O que é mais seguro: 755 ou 777?**
<details>
<summary>Resposta</summary>
755 é muito mais seguro. 777 permite que qualquer um modifique o arquivo.
</details>

**5. Por que `chmod 600 ~/.ssh/id_rsa` é importante?**
<details>
<summary>Resposta</summary>
Protege sua chave privada SSH. Sem isso, SSH recusa usar a chave.
</details>

---

## 📹 Recursos de Vídeo

1. **Permissões Linux Explicadas**
   - https://www.youtube.com/watch?v=4e669hSjaX8

2. **chmod e chown na Prática**
   - https://www.youtube.com/watch?v=D-VqgvBMV7g

3. **Gerenciamento de Usuários Linux**
   - https://www.youtube.com/watch?v=jwnvKOjmtEA

4. **Segurança com Permissões**
   - https://www.youtube.com/watch?v=FKclANTD5e8

5. **sudo e Privilégios no Linux**
   - https://www.youtube.com/watch?v=YSSIm0g00m4

---

## 🎯 Aplicação no Mundo Real - Deploy Seguro

### Cenário: Você precisa fazer deploy de uma aplicação web

```bash
# 1. Criar usuário específico para a aplicação
sudo useradd -m -s /bin/bash webapp
sudo usermod -aG www-data webapp

# 2. Preparar diretórios
sudo mkdir -p /var/www/myapp/{public,config,logs}

# 3. Copiar aplicação
sudo cp -r ~/myapp/* /var/www/myapp/

# 4. Configurar ownership
sudo chown -R webapp:www-data /var/www/myapp

# 5. Permissões seguras

# Código fonte: só leitura para grupo
sudo chmod -R 750 /var/www/myapp/public

# Configs: apenas webapp pode ler
sudo chmod 600 /var/www/myapp/config/*.yml

# Logs: webapp pode escrever, grupo pode ler
sudo chmod 660 /var/www/myapp/logs/app.log

# Scripts: executáveis apenas para webapp
sudo chmod 700 /var/www/myapp/scripts/*.sh

# 6. Configurar NGINX para rodar como www-data
# (NGINX já roda como www-data, pode acessar grupo www-data)

# 7. Testar acesso
sudo -u webapp ls -la /var/www/myapp/  # deve funcionar
sudo -u www-data ls -la /var/www/myapp/public/  # deve funcionar
```

---

## 📝 Tabela de Referência Rápida

| Permissão | Numérico | Simbólico | Uso Comum |
|-----------|----------|-----------|-----------|
| `rwxrwxrwx` | 777 | ❌ Evitar | Muito permissivo |
| `rwxr-xr-x` | 755 | ✅ Scripts | Executáveis |
| `rwxr-x---` | 750 | ✅ Apps | Aplicações web |
| `rw-rw-r--` | 664 | ✅ Arquivos | Compartilhados no grupo |
| `rw-r--r--` | 644 | ✅ Configs | Arquivos normais |
| `rw-------` | 600 | ✅ Secrets | Senhas, chaves |
| `r--------` | 400 | ✅ API Keys | Só leitura privado |

---

## 📝 Resumo da Aula

Você aprendeu:
- ✅ Sistema rwx de permissões
- ✅ chmod (forma simbólica e numérica)
- ✅ chown e chgrp para mudar ownership
- ✅ Criar e gerenciar usuários e grupos
- ✅ Usar sudo com responsabilidade
- ✅ Configurar permissões seguras para aplicações
- ✅ Proteger chaves SSH

**Próxima aula:** Variáveis de Ambiente e Customização

---

## 💡 Dicas Profissionais

1. **Comando útil para debug:**
```bash
# Ver permissões em formato octal
stat -c "%a %n" arquivo.txt
```

2. **Permissões padrão:**
```bash
# Ver umask (define permissões padrão)
umask

# Arquivos criados: 666 - umask = permissão final
# Diretórios: 777 - umask = permissão final
```

3. **Auditar permissões:**
```bash
# Encontrar arquivos com 777 (perigoso!)
find /var/www -type f -perm 0777

# Encontrar arquivos sem dono
find / -nouser -o -nogroup 2>/dev/null
```

---

## 🔥 Desafio Final

**Você está pronto se conseguir:**

1. Criar um usuário `deploy` e adicionar ao grupo `developers`
2. Criar diretório `/opt/app` pertencente a `deploy:developers`
3. Configurar para que:
   - Apenas `deploy` possa modificar arquivos
   - Grupo `developers` possa ler e executar
   - Outros não tenham acesso algum
4. Criar um script executável apenas pelo dono
5. Criar um arquivo de configuração legível apenas pelo dono

**Tente resolver antes de olhar a solução!**

<details>
<summary>💡 Solução</summary>

```bash
# 1. Criar usuário e grupo
sudo useradd -m deploy
sudo groupadd developers
sudo usermod -aG developers deploy

# 2. Criar e configurar diretório
sudo mkdir -p /opt/app
sudo chown deploy:developers /opt/app
sudo chmod 750 /opt/app

# 3. Permissões corretas
cd /opt/app
sudo -u deploy touch app.py
sudo -u deploy chmod 640 app.py  # rw-r-----

# 4. Script executável
sudo -u deploy touch deploy.sh
sudo -u deploy chmod 700 deploy.sh  # rwx------

# 5. Arquivo de config
sudo -u deploy touch .env
sudo -u deploy chmod 600 .env  # rw-------

# Verificar
ls -la /opt/app/
```
</details>

---

**🚀 Conseguiu? Você domina permissões! Próxima aula: Variáveis de Ambiente!**
