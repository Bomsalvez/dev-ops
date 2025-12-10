# Aula 6: Gerenciamento de Pacotes - APT e YUM

## 📚 Conceitos Fundamentais

### O que são Gerenciadores de Pacotes?
São ferramentas que automatizam instalação, atualização e remoção de software.

**Analogia:** Como uma App Store, mas via linha de comando.

**APT** (Debian/Ubuntu) e **YUM/DNF** (RedHat/CentOS) resolvem dependências automaticamente.

---

## 🎯 Conteúdo Principal

## APT (Advanced Package Tool)

```bash
# Atualizar lista de pacotes
sudo apt update

# Atualizar pacotes instalados
sudo apt upgrade

# Instalar pacote
sudo apt install nginx

# Remover pacote
sudo apt remove nginx

# Remover com configs
sudo apt purge nginx

# Buscar pacote
apt search nginx

# Ver info de pacote
apt show nginx

# Listar instalados
apt list --installed

# Limpar cache
sudo apt clean
sudo apt autoclean
sudo apt autoremove
```

## YUM/DNF (RedHat/CentOS)

```bash
# Atualizar
sudo yum update

# Instalar
sudo yum install nginx

# Remover
sudo yum remove nginx

# Buscar
yum search nginx

# Info
yum info nginx

# Listar
yum list installed
```

---

## 💪 Exercício Prático

```bash
# Instalar Stack LAMP
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y

# Verificar
sudo systemctl status apache2
sudo systemctl status mysql
php -v

# Testar
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
curl localhost/info.php
```

---

## 📹 Recursos de Vídeo

1. **APT no Ubuntu** - https://www.youtube.com/watch?v=HXTHm0hY5l0
2. **YUM no CentOS** - https://www.youtube.com/watch?v=PrJQFNhZjvs
3. **Gerenciadores de Pacotes** - https://www.youtube.com/watch?v=SKyM4gS5pxc

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
