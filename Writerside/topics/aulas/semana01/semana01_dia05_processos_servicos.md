# Aula 5: Gerenciamento de Processos e Serviços

## 📚 Conceitos Fundamentais

### O que são Processos?
Um processo é um programa em execução. Quando você abre o navegador, cria um processo. Quando roda um script, cria um processo.

**Analogia:** Pense no seu computador como uma cozinha. Cada processo é um prato sendo preparado. Alguns pratos (processos) precisam de mais fogo (CPU), outros de mais espaço (RAM).

**No DevOps:** Você constantemente precisa:
- Monitorar processos que consomem muita CPU/memória
- Matar processos travados
- Iniciar/parar serviços (Docker, NGINX, bancos de dados)
- Entender o que está rodando no servidor

---

## 🎯 Comandos Essenciais de Processos

### 1. ps (Process Status)

```bash
# Ver processos do usuário atual
ps

# Ver TODOS os processos (formato detalhado)
ps aux
# a = all users
# u = user-oriented format
# x = include processes without terminal

# Colunas importantes:
# USER = dono do processo
# PID  = Process ID (identificador único)
# %CPU = uso de CPU
# %MEM = uso de memória
# VSZ  = memória virtual
# RSS  = memória real usada
# STAT = estado (R=running, S=sleeping, Z=zombie)
# START= hora que iniciou
# TIME = tempo de CPU usado
# COMMAND = comando executado

# Ver processos em árvore
ps auxf

# Buscar processo específico
ps aux | grep nginx
ps aux | grep docker

# Ordenar por CPU
ps aux --sort=-%cpu | head -10

# Ordenar por memória
ps aux --sort=-%mem | head -10
```

---

### 2. top e htop

**top** - Monitor interativo de processos

```bash
top

# Comandos dentro do top:
# q = sair
# k = matar processo (kill)
# u = filtrar por usuário
# M = ordenar por memória
# P = ordenar por CPU
# c = mostrar comando completo
# 1 = mostrar todos os cores da CPU
```

**htop** - Versão melhorada (precisa instalar)

```bash
# Instalar
sudo apt install htop  # Ubuntu/Debian
sudo yum install htop  # CentOS/RHEL

# Executar
htop

# Vantagens sobre top:
# - Interface colorida
# - Mouse funciona
# - Mais fácil de matar processos
# - Mostra árvore de processos
# - Configurável
```

**Interpretando a saída:**

```
CPU: [|||||||||||........] 45%
Mem: [|||||||||||||||||..] 85% 
Swp: [|..................] 5%

PID USER     %CPU %MEM    VSZ   RSS   COMMAND
1234 user    25.0  5.2  500M  200M  /usr/bin/node app.js
5678 root    15.0  2.1  300M  80M   /usr/sbin/nginx
```

---

### 3. Sinais e Kill

```bash
# Matar processo por PID
kill PID
kill 1234

# Força matar (SIGKILL - não pode ser ignorado)
kill -9 PID
kill -KILL PID

# Matar gracefully (SIGTERM - recomendado)
kill -15 PID
kill -TERM PID

# Outros sinais úteis
kill -HUP PID   # Hangup (recarregar config)
kill -STOP PID  # Pausar
kill -CONT PID  # Continuar

# Matar por nome (cuidado!)
killall nome_processo
killall chrome

# Mais seguro - confirma antes
pkill -9 nome_processo

# Ver sinais disponíveis
kill -l
```

**Diferença importante:**
- `kill` (SIGTERM): "Por favor, termine o que está fazendo e saia"
- `kill -9` (SIGKILL): "MORRA AGORA!" (pode corromper dados)

---

### 4. Processos em Background

```bash
# Executar em background
comando &
sleep 100 &

# Ver jobs em background
jobs

# Trazer de volta para foreground
fg %1  # job número 1

# Mandar para background
Ctrl+Z  # pausa o processo
bg %1   # continua em background

# nohup - continua mesmo depois de logout
nohup script.sh &

# Melhor ainda: usar screen ou tmux
nohup python3 app.py > app.log 2>&1 &
```

---

## 🔧 Gerenciamento de Serviços

### systemctl (SystemD)

**Comandos básicos:**

```bash
# Iniciar serviço
sudo systemctl start nginx

# Parar serviço
sudo systemctl stop nginx

# Reiniciar serviço
sudo systemctl restart nginx

# Recarregar configuração (sem parar)
sudo systemctl reload nginx

# Ver status
sudo systemctl status nginx

# Habilitar na inicialização
sudo systemctl enable nginx

# Desabilitar na inicialização
sudo systemctl disable nginx

# Ver se está habilitado
sudo systemctl is-enabled nginx

# Ver se está ativo
sudo systemctl is-active nginx
```

**Ver serviços:**

```bash
# Listar todos os serviços
systemctl list-units --type=service

# Apenas ativos
systemctl list-units --type=service --state=active

# Apenas falhos
systemctl list-units --type=service --state=failed

# Ver logs de um serviço
sudo journalctl -u nginx

# Seguir logs em tempo real
sudo journalctl -u nginx -f

# Últimas 50 linhas
sudo journalctl -u nginx -n 50
```

---

### Criar Serviço Customizado

```bash
# Criar arquivo de serviço
sudo nano /etc/systemd/system/meuapp.service

# Conteúdo:
[Unit]
Description=Minha Aplicação Node.js
After=network.target

[Service]
Type=simple
User=appuser
WorkingDirectory=/opt/app
ExecStart=/usr/bin/node /opt/app/server.js
Restart=always
RestartSec=10
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=meuapp

Environment=NODE_ENV=production
Environment=PORT=3000

[Install]
WantedBy=multi-user.target

# Recarregar systemd
sudo systemctl daemon-reload

# Iniciar e habilitar
sudo systemctl start meuapp
sudo systemctl enable meuapp

# Verificar
sudo systemctl status meuapp
```

---

## 🤔 Perguntas Socráticas

1. **Quando você usaria `kill -9` vs `kill -15`?**
   - -15 (SIGTERM): Sempre tente primeiro. Permite limpeza graceful.
   - -9 (SIGKILL): Apenas se -15 falhar. Mata imediatamente mas pode corromper dados.

2. **Por que processos em background são úteis?**
   - Permitem rodar tarefas longas sem travar o terminal.

3. **Qual a diferença entre `restart` e `reload`?**
   - restart: Para e inicia o serviço (downtime)
   - reload: Recarrega config sem parar (sem downtime)

4. **Por que usar `systemctl enable`?**
   - Faz o serviço iniciar automaticamente no boot do sistema.

5. **O que é um processo "zombie"?**
   - Processo que terminou mas o parent process não reconheceu. Aparece com Z no STAT.

---

## 💪 Exercício Prático

### Desafio 1: Monitoramento de Sistema

```bash
# 1. Ver top 5 processos por CPU
ps aux --sort=-%cpu | head -6

# 2. Ver top 5 processos por memória  
ps aux --sort=-%mem | head -6

# 3. Monitorar processo específico
watch -n 1 'ps aux | grep nginx'

# 4. Ver uso total de recursos
free -h  # memória
df -h    # disco
uptime   # load average

# 5. Encontrar processo usando porta
sudo lsof -i :80
sudo netstat -tulpn | grep :80

# 6. Criar script de monitoramento
cat > monitor.sh << 'EOF'
#!/bin/bash
echo "=== Monitoramento do Sistema ==="
echo "Data: $(date)"
echo ""
echo "=== Top 5 CPU ==="
ps aux --sort=-%cpu | head -6
echo ""
echo "=== Top 5 Memória ==="
ps aux --sort=-%mem | head -6
echo ""
echo "=== Uso de Memória ==="
free -h
echo ""
echo "=== Uso de Disco ==="
df -h
echo ""
echo "=== Load Average ==="
uptime
EOF

chmod +x monitor.sh
./monitor.sh
```

---

### Desafio 2: Gerenciar Serviço Nginx

```bash
# 1. Instalar NGINX
sudo apt update
sudo apt install nginx -y

# 2. Verificar status
sudo systemctl status nginx

# 3. Parar serviço
sudo systemctl stop nginx

# 4. Iniciar serviço
sudo systemctl start nginx

# 5. Verificar se está escutando na porta 80
sudo lsof -i :80

# 6. Ver logs
sudo journalctl -u nginx -n 20

# 7. Habilitar na inicialização
sudo systemctl enable nginx

# 8. Testar configuração
sudo nginx -t

# 9. Recarregar sem downtime
sudo systemctl reload nginx

# 10. Ver processo do nginx
ps aux | grep nginx
```

---

### Desafio 3: Criar Serviço para Aplicação

```bash
# 1. Criar app simples
mkdir -p /opt/minha-app
cat > /opt/minha-app/app.py << 'EOF'
#!/usr/bin/env python3
import time
import datetime

while True:
    print(f"[{datetime.datetime.now()}] App rodando...")
    time.sleep(10)
EOF

chmod +x /opt/minha-app/app.py

# 2. Criar serviço systemd
sudo tee /etc/systemd/system/minha-app.service << 'EOF'
[Unit]
Description=Minha Aplicação de Teste
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/minha-app
ExecStart=/usr/bin/python3 /opt/minha-app/app.py
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

# 3. Recarregar systemd
sudo systemctl daemon-reload

# 4. Iniciar serviço
sudo systemctl start minha-app

# 5. Verificar status
sudo systemctl status minha-app

# 6. Ver logs
sudo journalctl -u minha-app -f

# 7. Habilitar na inicialização
sudo systemctl enable minha-app

# 8. Testar restart automático
sudo kill -9 $(pgrep -f "python3 /opt/minha-app")
sleep 6
sudo systemctl status minha-app  # Deve estar rodando novamente!
```

---

## ✅ Mini-Quiz de Revisão

**1. Como ver top 10 processos usando mais CPU?**
<details>
<summary>Resposta</summary>
`ps aux --sort=-%cpu | head -11` ou usar `top` e pressionar P
</details>

**2. Qual a diferença entre kill e kill -9?**
<details>
<summary>Resposta</summary>
kill (SIGTERM) permite que o processo termine gracefully. kill -9 (SIGKILL) mata imediatamente.
</details>

**3. Como fazer um serviço iniciar no boot?**
<details>
<summary>Resposta</summary>
`sudo systemctl enable nome-servico`
</details>

**4. Como ver logs de um serviço em tempo real?**
<details>
<summary>Resposta</summary>
`sudo journalctl -u nome-servico -f`
</details>

**5. Como recarregar configuração do NGINX sem downtime?**
<details>
<summary>Resposta</summary>
`sudo systemctl reload nginx` ou `sudo nginx -s reload`
</details>

---

## 📹 Recursos de Vídeo

1. **Gerenciamento de Processos Linux**
   - https://www.youtube.com/watch?v=XMUYJRidMzA

2. **Comandos ps, top, kill**
   - https://www.youtube.com/watch?v=2cCqy15izLU

3. **Systemd e Systemctl**
   - https://www.youtube.com/watch?v=AtEqbYTLHfs

4. **Criar Serviços no Linux**
   - https://www.youtube.com/watch?v=fYQBvjYQ63U

5. **Monitoramento de Servidores Linux**
   - https://www.youtube.com/watch?v=lZ74kuDsONw

---

## 🎯 Aplicação no Mundo Real

### Cenário: Servidor Web com Problemas

```bash
# Situação: Servidor lento, precisa investigar

# 1. Ver load average
uptime
# Se > número de CPUs, está sobrecarregado

# 2. Identificar processo problemático
htop
# ou
ps aux --sort=-%cpu | head -10

# 3. Ver detalhes do processo
top -p PID

# 4. Ver o que o processo está fazendo
sudo strace -p PID

# 5. Ver arquivos abertos
sudo lsof -p PID

# 6. Se for necessário, matar
sudo kill -15 PID  # Tente graceful primeiro
sleep 5
sudo kill -9 PID   # Se não funcionou

# 7. Verificar se é problema de memória
free -h
# Se swap estiver alto, falta RAM

# 8. Ver logs do sistema
sudo journalctl -p err -n 50

# 9. Reiniciar serviço problemático
sudo systemctl restart nome-servico

# 10. Monitorar por alguns minutos
watch -n 2 'ps aux | grep nome-servico'
```

---

## 📝 Resumo da Aula

Você aprendeu:
- ✅ Comandos ps, top, htop para monitorar processos
- ✅ Gerenciar processos com kill, killall, pkill
- ✅ Processos em background com &, jobs, fg, bg
- ✅ Systemctl para gerenciar serviços
- ✅ Criar serviços customizados com systemd
- ✅ Ver logs com journalctl
- ✅ Troubleshooting de performance

**Próxima aula:** Gerenciamento de Pacotes

---

## 💡 Dicas Profissionais

### 1. Aliases úteis para .bashrc

```bash
alias psg='ps aux | grep'
alias topcpu='ps aux --sort=-%cpu | head -10'
alias topmem='ps aux --sort=-%mem | head -10'
alias ports='sudo netstat -tulpn'
alias listening='sudo lsof -i -P -n | grep LISTEN'
```

### 2. Script de Monitoramento

```bash
#!/bin/bash
# monitor.sh - Monitoramento automático

THRESHOLD_CPU=80
THRESHOLD_MEM=90

# Verificar CPU
CPU=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')

if (( $(echo "$CPU > $THRESHOLD_CPU" | bc -l) )); then
    echo "ALERTA: CPU em ${CPU}%"
    ps aux --sort=-%cpu | head -5
fi

# Verificar memória
MEM=$(free | grep Mem | awk '{print ($3/$2) * 100.0}')

if (( $(echo "$MEM > $THRESHOLD_MEM" | bc -l) )); then
    echo "ALERTA: Memória em ${MEM}%"
    ps aux --sort=-%mem | head -5
fi
```

---

## 🔥 Desafio Final

**Cenário Real:** Você é DevOps e recebe alerta de servidor lento.

**Tarefas:**
1. Identificar top 3 processos usando mais CPU
2. Identificar top 3 processos usando mais memória
3. Verificar se algum serviço está falhando
4. Ver logs dos últimos 5 minutos
5. Se encontrar processo problemático, matá-lo de forma segura
6. Documentar o que encontrou

**Crie um script que automatize essa investigação inicial!**

---

**🚀 Dominou processos? Próxima aula: Gerenciamento de Pacotes!**
