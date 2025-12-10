# Aula 7: Compactação e Transferência de Arquivos

## 📚 Conceitos Fundamentais

### Compactação
Reduz tamanho de arquivos para armazenamento/transferência.

### Transferência
Move arquivos entre servidores de forma segura.

---

## 🎯 Conteúdo Principal

## tar (Tape Archive)

```bash
# Criar arquivo .tar
tar -cf arquivo.tar pasta/

# Criar com gzip (.tar.gz)
tar -czf arquivo.tar.gz pasta/

# Criar com bzip2 (.tar.bz2) - mais compressão
tar -cjf arquivo.tar.bz2 pasta/

# Extrair
tar -xzf arquivo.tar.gz

# Listar conteúdo
tar -tzf arquivo.tar.gz

# Extrair arquivo específico
tar -xzf arquivo.tar.gz arquivo.txt
```

## zip/unzip

```bash
# Compactar
zip -r arquivo.zip pasta/

# Descompactar
unzip arquivo.zip

# Listar
unzip -l arquivo.zip
```

## scp (Secure Copy)

```bash
# Copiar para servidor
scp arquivo.txt user@servidor:/path

# Copiar do servidor
scp user@servidor:/path/arquivo.txt .

# Copiar diretório
scp -r pasta/ user@servidor:/path

# Especificar porta
scp -P 2222 arquivo.txt user@servidor:/path
```

## rsync (melhor que scp)

```bash
# Sincronizar
rsync -avz pasta/ user@servidor:/path/

# Opções:
# -a = archive (preserva tudo)
# -v = verbose
# -z = compressão durante transfer
# --delete = remove do destino o que não existe na origem
# --exclude = excluir padrão

# Dry-run (testar sem executar)
rsync -avz --dry-run pasta/ user@servidor:/path/

# Mostrar progresso
rsync -avz --progress pasta/ user@servidor:/path/
```

---

## 💪 Exercício Prático

```bash
# Sistema de Backup

#!/bin/bash
BACKUP_DIR=~/backups
DATE=\$(date +%Y%m%d_%H%M%S)

mkdir -p $BACKUP_DIR

# Backup compactado
tar -czf $BACKUP_DIR/projeto_$DATE.tar.gz ~/projeto

# Transferir para servidor
rsync -avz $BACKUP_DIR/ backup@servidor:/backups/

# Limpar backups antigos (mais de 30 dias)
find $BACKUP_DIR -name "*.tar.gz" -mtime +30 -delete

echo "Backup concluído: projeto_$DATE.tar.gz"

```

---

## 📹 Recursos de Vídeo

1. **tar e gzip** - https://www.youtube.com/watch?v=wBp0Rb-ZJak
2. **scp e rsync** - https://www.youtube.com/watch?v=MYw7RUNIAR8
3. **Backup no Linux** - https://www.youtube.com/watch?v=5rsqBUlqGBo

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
