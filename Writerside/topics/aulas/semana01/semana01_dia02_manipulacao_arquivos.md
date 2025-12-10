# Aula 2: Manipulação de Arquivos no Linux

## 📚 Conceitos Fundamentais

### Por que manipular arquivos via terminal?
No mundo DevOps, você trabalhará constantemente com logs, configurações e scripts em servidores remotos sem interface gráfica. Dominar ferramentas de manipulação de texto é essencial para:
- Analisar logs de aplicações
- Buscar erros em arquivos gigantes
- Filtrar informações relevantes
- Automatizar processos

**Analogia:** Imagine que você é um detetive analisando milhares de documentos. Essas ferramentas são suas lupas e filtros especiais.

---

## 🎯 Ferramentas de Visualização

### 1. cat (Concatenate)
**Conceito:** Exibe conteúdo completo de arquivos pequenos.

```bash
# Ver arquivo
cat arquivo.txt

# Numerar linhas
cat -n arquivo.txt

# Mostrar caracteres especiais
cat -A arquivo.txt

# Concatenar múltiplos arquivos
cat arquivo1.txt arquivo2.txt > combinado.txt
```

**Quando usar:** Arquivos pequenos (<100 linhas)

---

### 2. less
**Conceito:** Visualizador paginado para arquivos grandes.

```bash
less arquivo-grande.log

# Navegação:
# Espaço ou f = próxima página
# b = página anterior
# g = início do arquivo
# G = fim do arquivo
# /texto = buscar texto
# n = próxima ocorrência
# q = sair
```

**Quando usar:** Logs e arquivos grandes
**Analogia:** Como ler um livro página por página

---

### 3. head
**Conceito:** Mostra as primeiras linhas de um arquivo.

```bash
# Primeiras 10 linhas (padrão)
head arquivo.txt

# Primeiras 20 linhas
head -n 20 arquivo.txt

# Múltiplos arquivos
head -n 5 *.log
```

**Uso real:** Ver cabeçalhos de logs ou início de arquivos de configuração

---

### 4. tail
**Conceito:** Mostra as últimas linhas de um arquivo.

```bash
# Últimas 10 linhas
tail arquivo.txt

# Últimas 50 linhas
tail -n 50 app.log

# Monitorar em tempo real (MUITO IMPORTANTE!)
tail -f /var/log/application.log

# Últimas 100 linhas e continuar monitorando
tail -n 100 -f app.log
```

**Uso real:** Monitorar logs em tempo real durante deploy!

---

## 🔍 Ferramentas de Busca

### 5. grep (Global Regular Expression Print)
**Conceito:** Busca padrões de texto em arquivos.

```bash
# Busca básica
grep "erro" app.log

# Case insensitive
grep -i "error" app.log

# Buscar recursivamente em diretórios
grep -r "TODO" src/

# Mostrar número da linha
grep -n "exception" app.log

# Inverter busca (linhas que NÃO contêm)
grep -v "INFO" app.log

# Contar ocorrências
grep -c "ERROR" app.log

# Buscar múltiplos padrões
grep -E "error|warning|critical" app.log

# Contexto (linhas antes/depois)
grep -A 3 -B 3 "Exception" app.log
# -A = After (depois)
# -B = Before (antes)
# -C = Context (antes e depois)
```

**Exemplo real - Encontrar erros em log:**
```bash
grep -i "error\|exception\|fatal" /var/log/application.log
```

---

### 6. find
**Conceito:** Busca arquivos no sistema por diversos critérios.

```bash
# Buscar por nome
find /home -name "*.txt"

# Case insensitive
find . -iname "readme*"

# Buscar por tipo
find . -type f  # arquivos
find . -type d  # diretórios

# Buscar por tamanho
find . -size +100M  # maior que 100MB
find . -size -1k    # menor que 1KB

# Buscar por data de modificação
find . -mtime -7    # modificado nos últimos 7 dias
find . -mtime +30   # modificado há mais de 30 dias

# Executar comando nos resultados
find . -name "*.log" -exec rm {} \;
find . -type f -name "*.txt" -exec grep "error" {} \;

# Buscar e deletar arquivos antigos
find /tmp -type f -mtime +30 -delete
```

**Exemplo real - Limpar logs antigos:**
```bash
find /var/log -name "*.log" -mtime +90 -delete
```

---

## ⚡ Redirecionamento e Pipes

### Conceito de Pipes (|)
**Analogia:** Imagine uma fábrica onde o produto passa por várias etapas. O pipe conecta essas etapas.

```bash
# Comando1 | Comando2 | Comando3
# Saída do Comando1 vira entrada do Comando2

# Exemplo: Contar linhas com erro
cat app.log | grep "ERROR" | wc -l

# Filtrar e ordenar
ls -l | grep ".txt" | sort

# Top 10 IPs mais frequentes em log
cat access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -10
```

---

### Redirecionamento

```bash
# > sobrescreve arquivo
echo "texto" > arquivo.txt
ls -l > listagem.txt

# >> adiciona ao final
echo "nova linha" >> arquivo.txt
date >> log.txt

# 2> redireciona erros
comando-inexistente 2> erros.txt

# &> redireciona saída e erros
comando &> saida-completa.txt

# /dev/null (lixeira do Linux)
comando 2> /dev/null  # ignora erros
```

**Exemplo real:**
```bash
# Salvar apenas erros de compilação
mvn clean install > /dev/null 2> erros-compilacao.txt
```

---

## 🤔 Perguntas Socráticas

1. **Por que `tail -f` é tão importante em DevOps?**
   - Resposta: Permite monitorar logs em tempo real durante deploys e troubleshooting.

2. **Quando você usaria `head` vs `tail` vs `less`?**
   - head: início de arquivo (headers, primeiras entradas)
   - tail: fim de arquivo (logs recentes)
   - less: navegação completa em arquivos grandes

3. **Por que `grep -v` é útil?**
   - Resposta: Filtrar ruído. Ex: remover linhas de INFO para focar em ERRORs.

4. **O que acontece se você usar `>` em vez de `>>` por engano?**
   - Resposta: Sobrescreve o arquivo, perdendo dados! Sempre use >> para adicionar.

5. **Como você encontraria todos os arquivos de log maiores que 500MB no servidor?**
   - Resposta: `find /var/log -name "*.log" -size +500M`

---

## 💪 Exercício Prático

### Desafio: Análise de Logs de Aplicação

```bash
# 1. Criar log simulado
cat > app.log << 'EOF'
2024-01-15 10:00:01 INFO Application started
2024-01-15 10:00:05 INFO User john logged in
2024-01-15 10:01:23 ERROR Database connection failed
2024-01-15 10:01:24 WARN Retrying connection...
2024-01-15 10:01:30 INFO Database connected
2024-01-15 10:05:00 ERROR File not found: /data/config.json
2024-01-15 10:05:01 CRITICAL System shutting down
2024-01-15 10:10:00 INFO Application restarted
2024-01-15 10:15:23 ERROR OutOfMemoryError in module X
2024-01-15 10:16:00 INFO Cleanup completed
EOF

# 2. Análises solicitadas:
# a) Quantos erros ocorreram?
grep -c "ERROR" app.log

# b) Mostrar todas as linhas de erro com contexto
grep -A 2 -B 1 "ERROR" app.log

# c) Listar apenas os erros, sem INFO/WARN
grep "ERROR\|CRITICAL" app.log

# d) Salvar erros em arquivo separado
grep "ERROR\|CRITICAL" app.log > erros-criticos.txt

# e) Monitorar log em tempo real (simular)
tail -f app.log  # (Ctrl+C para sair)

# 3. Buscar arquivos de configuração
find /etc -name "*.conf" -type f 2>/dev/null | head -20

# 4. Encontrar arquivos grandes
find ~ -size +100M -type f 2>/dev/null
```

---

## ✅ Mini-Quiz de Revisão

**1. Qual comando para ver as últimas 50 linhas de um log?**
<details>
<summary>Resposta</summary>
`tail -n 50 arquivo.log` ou `tail -50 arquivo.log`
</details>

**2. Como buscar "error" ignorando maiúsculas/minúsculas?**
<details>
<summary>Resposta</summary>
`grep -i "error" arquivo.log`
</details>

**3. Como monitorar um log em tempo real?**
<details>
<summary>Resposta</summary>
`tail -f arquivo.log`
</details>

**4. Como contar quantas vezes "Exception" aparece no arquivo?**
<details>
<summary>Resposta</summary>
`grep -c "Exception" arquivo.log`
</details>

**5. Como adicionar texto ao final de um arquivo sem sobrescrever?**
<details>
<summary>Resposta</summary>
`echo "texto" >> arquivo.txt`
</details>

---

## 📹 Recursos de Vídeo

1. **Grep e Find no Linux**
   - https://www.youtube.com/watch?v=VGgTmxXp7xQ

2. **Manipulação de Arquivos Linux**
   - https://www.youtube.com/watch?v=zRw0SKaXSfM

3. **Redirecionamento no Linux**
   - https://www.youtube.com/watch?v=kq8opgnLPuo

4. **Comandos para Análise de Logs**
   - https://www.youtube.com/watch?v=FPSryLFKQkk

5. **Expressões Regulares com Grep**
   - https://www.youtube.com/watch?v=bgBWp9EIlMM

---

## 🎯 Aplicação no Mundo Real - Cenário DevOps

### Situação: Aplicação em produção apresentando erros

```bash
# 1. Conectar ao servidor
ssh usuario@servidor-prod

# 2. Ir até o diretório de logs
cd /var/log/aplicacao

# 3. Monitorar log em tempo real
tail -f application.log

# 4. Em outro terminal, buscar erros das últimas 24h
grep "ERROR" application.log | grep "\$(date +%Y-%m-%d)"

# 5. Contar tipos de erro
grep "ERROR" application.log | awk '{print $4}' | sort | uniq -c | sort -rn

# 6. Encontrar quando começou o problema
grep -n "OutOfMemoryError" application.log | head -1

# 7. Ver contexto do erro
grep -A 10 -B 10 "OutOfMemoryError" application.log

# 8. Salvar relatório
{
  echo "=== Relatório de Erros - \$(date) ==="
  echo ""
  echo "Total de erros:"
  grep -c "ERROR" application.log
  echo ""
  echo "Top 5 erros:"
  grep "ERROR" application.log | awk '{print $4}' | sort | uniq -c | sort -rn | head -5
} > relatorio-erros.txt

# 9. Limpar logs antigos para liberar espaço
find /var/log/aplicacao -name "*.log" -mtime +30 -delete

# 10. Verificar espaço em disco
du -sh /var/log/aplicacao
```

---

## 📝 Resumo da Aula

Você aprendeu:
- ✅ Visualizar arquivos (cat, less, head, tail)
- ✅ Buscar conteúdo (grep com múltiplas opções)
- ✅ Encontrar arquivos (find por nome, tamanho, data)
- ✅ Redirecionar saída (>, >>, 2>, &>)
- ✅ Usar pipes para combinar comandos
- ✅ Analisar logs em produção

**Próxima aula:** Permissões e Usuários no Linux

---

## 💡 Dicas Profissionais

1. **Alias úteis** - Adicione no ~/.bashrc:
```bash
alias ll='ls -lah'
alias logs='tail -f /var/log/application.log'
alias errors='grep -i "error\|exception" /var/log/application.log'
```

2. **Combine comandos** - Power user:
```bash
# Top 10 processos usando memória
ps aux | sort -rn -k 4 | head -10

# Buscar e substituir em múltiplos arquivos
find . -name "*.txt" -exec sed -i 's/antigo/novo/g' {} \;
```

3. **Use `history`** - Ver comandos anteriores:
```bash
history | grep grep  # buscar comandos que usei com grep
!123  # executar comando número 123 do histórico
```

---

## 🔥 Desafio Final

**Você está pronto se conseguir fazer isso sem consultar:**

1. Encontrar todos os arquivos .log maiores que 10MB modificados nos últimos 7 dias
2. Buscar a palavra "timeout" (case insensitive) mostrando 3 linhas de contexto
3. Contar quantos erros únicos existem no log
4. Monitorar o log filtrando apenas linhas com "ERROR" ou "FATAL"
5. Salvar o resultado em um relatório com data no nome do arquivo

**Tente resolver antes de olhar a solução!**

<details>
<summary>💡 Solução</summary>

```bash
# 1. Encontrar arquivos
find /var/log -name "*.log" -size +10M -mtime -7

# 2. Buscar com contexto
grep -i -C 3 "timeout" application.log

# 3. Contar erros únicos
grep "ERROR" application.log | sort | uniq | wc -l

# 4. Monitorar filtrado
tail -f application.log | grep --line-buffered "ERROR\|FATAL"

# 5. Salvar relatório
grep "ERROR\|FATAL" application.log > relatorio-\$(date +%Y%m%d-%H%M%S).txt
```
</details>

---

**🚀 Conseguiu? Avance para a próxima aula!**
**Teve dúvidas? Pratique mais os exercícios desta aula.**
