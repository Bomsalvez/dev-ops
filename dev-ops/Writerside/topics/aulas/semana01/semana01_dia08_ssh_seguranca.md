# Aula 8: SSH e Segurança Avançada

## 📚 Conceitos Fundamentais

### SSH (Secure Shell)
Protocolo para acesso remoto seguro a servidores.

**Por que é importante:**
- Todo trabalho DevOps envolve servidores remotos
- Chaves SSH são mais seguras que senhas
- Base para Git, Ansible, deploy automatizado

---

## 🎯 Conteúdo Principal

## Configuração SSH

```bash
# Conectar
ssh usuario@servidor

# Porta customizada
ssh -p 2222 usuario@servidor

# Executar comando remoto
ssh usuario@servidor 'ls -la'

# Túnel SSH (port forwarding)
ssh -L 8080:localhost:80 usuario@servidor

# Arquivo de config
nano ~/.ssh/config

Host servidor-prod
    HostName 192.168.1.100
    User deploy
    Port 22
    IdentityFile ~/.ssh/id_rsa_prod

# Agora pode usar:
ssh servidor-prod
```

## Chaves SSH

```bash
# Gerar par de chaves
ssh-keygen -t rsa -b 4096 -C "email@example.com"

# Ed25519 (mais seguro e rápido)
ssh-keygen -t ed25519 -C "email@example.com"

# Copiar chave pública para servidor
ssh-copy-id usuario@servidor

# Ou manualmente
cat ~/.ssh/id_rsa.pub | ssh usuario@servidor 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'

# Permissões corretas (CRÍTICO!)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/config
```

## Hardening SSH

```bash
# Editar config do servidor
sudo nano /etc/ssh/sshd_config

# Mudanças recomendadas:
Port 2222                          # Mudar porta padrão
PermitRootLogin no                 # Desabilitar login root
PasswordAuthentication no          # Apenas chaves
PubkeyAuthentication yes
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2

# Aplicar mudanças
sudo systemctl restart sshd

# Firewall
sudo ufw allow 2222/tcp
sudo ufw enable
```

## SSH Agent

```bash
# Iniciar agent
eval "$(ssh-agent -s)"

# Adicionar chave
ssh-add ~/.ssh/id_rsa

# Listar chaves
ssh-add -l

# Remover todas
ssh-add -D
```

---

## 💪 Exercício Prático

```bash
# Configurar Acesso SSH Seguro

# 1. Gerar chave
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_devops

# 2. Copiar para servidor
ssh-copy-id -i ~/.ssh/id_ed25519_devops.pub user@servidor

# 3. Criar config
cat >> ~/.ssh/config << EOF
Host devserver
    HostName 192.168.1.100
    User devops
    Port 22
    IdentityFile ~/.ssh/id_ed25519_devops
    ServerAliveInterval 60
EOF

chmod 600 ~/.ssh/config

# 4. Testar
ssh devserver

# 5. Hardening no servidor
ssh devserver 'sudo sed -i "s/#PasswordAuthentication yes/PasswordAuthentication no/" /etc/ssh/sshd_config'
ssh devserver 'sudo systemctl restart sshd'

```

---

## 📹 Recursos de Vídeo

1. **SSH Completo** - https://www.youtube.com/watch?v=hQWRp-FdTpc
2. **Chaves SSH** - https://www.youtube.com/watch?v=_BFHvESEJfs
3. **Segurança SSH** - https://www.youtube.com/watch?v=7_BbVKLYm-w
4. **SSH Config File** - https://www.youtube.com/watch?v=gZx9yCbQg50

---

## 🤔 Perguntas Socráticas

1. **Por que este conceito é importante no DevOps?**
   - Ajuda a entender aplicação prática no dia a dia

2. **Quais problemas este tema resolve?**
   - Conexão com cenários reais

3. **Como isso se integra com outras ferramentas?**
   - Visão do ecosistema completo

---

## ✅ Mini-Quiz de Revisão

**1. [Pergunta prática sobre o tema]**
<details>
<summary>Resposta</summary>
[Explicação detalhada da resposta]
</details>

**2. [Outra pergunta aplicada]**
<details>
<summary>Resposta</summary>
[Outra explicação]
</details>

---

## 📝 Resumo da Aula

Você aprendeu os fundamentos e práticas essenciais deste tema, com foco em aplicação real no ambiente DevOps.

---

## 🎯 Aplicação no Mundo Real

[Cenário prático de como usar este conhecimento em produção]

---

## 🔥 Desafio Final

**Você está pronto para avançar se conseguir:**

1. [Objetivo prático 1]
2. [Objetivo prático 2]
3. [Objetivo prático 3]

**Crie um projeto real aplicando estes conceitos!**

---

**🚀 Dominou este tema? Avance para a próxima aula!**
