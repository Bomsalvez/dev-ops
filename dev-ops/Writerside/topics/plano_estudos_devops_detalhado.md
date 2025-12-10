# Plano de Estudos DevOps Completo - 2h/dia

## 📋 Visão Geral
- **Duração Total:** ~20 semanas
- **Carga Diária:** 2 horas
- **Formato:** Teoria (40min) + Prática (80min)
- **Objetivo:** Domínio completo do ciclo DevOps

---

# 🐧 BLOCO 1: FUNDAMENTOS LINUX (1.5 semanas)

## Semana 1 - Linux Essencial

### **Dia 1 - Fundamentos e Navegação (2h)**
- Sistema de arquivos Linux (teoria: 30min)
- Comandos básicos: ls, cd, pwd, mkdir, rm, cp, mv (prática: 45min)
- Wildcards e expansão de shell (teoria: 15min)
- **Prática:** Criar estrutura de diretórios para projeto DevOps (30min)

### **Dia 2 - Manipulação de Arquivos (2h)**
- Comandos: cat, less, head, tail, grep, find (teoria: 30min)
- Redirecionamento e pipes (teoria: 20min)
- **Prática:** Scripts de busca e filtros de logs (70min)

### **Dia 3 - Permissões e Usuários (2h)**
- Permissões rwx, chmod, chown, chgrp (teoria: 30min)
- Usuários e grupos: useradd, groupadd, su, sudo (teoria: 20min)
- **Prática:** Configurar ambiente multi-usuário (70min)

### **Dia 4 - Variáveis e Ambiente (2h)**
- Variáveis de ambiente e shell (teoria: 25min)
- PATH, .bashrc, .profile (teoria: 20min)
- Editores: vim básico e nano (teoria: 15min)
- **Prática:** Customizar ambiente shell (60min)

### **Dia 5 - Processos e Serviços (2h)**
- Gerenciamento: ps, top, htop, kill, killall (teoria: 30min)
- Background/foreground, jobs, nohup (teoria: 20min)
- **Prática:** Monitorar e gerenciar processos (70min)

### **Dia 6 - Gerenciamento de Pacotes (2h)**
- APT (Debian/Ubuntu): teoria: 20min
- YUM/DNF (RedHat/CentOS): teoria: 20min
- **Prática:** Instalar stack LAMP do zero (80min)

### **Dia 7 - Compactação e Transferência (2h)**
- tar, gzip, bzip2, zip, unzip (teoria: 25min)
- scp, rsync: teoria: 20min
- **Prática:** Backup automatizado com compressão (75min)

## Semana 2 - Linux Avançado

### **Dia 1 - SSH e Segurança (2h)**
- Configuração SSH, chaves públicas/privadas (teoria: 30min)
- ssh-keygen, ssh-copy-id, config file (teoria: 20min)
- **Prática:** Configurar acesso SSH sem senha entre VMs (70min)

### **Dia 2 - Shell Script - Parte 1 (2h)**
- Estrutura de scripts, shebang, variáveis (teoria: 25min)
- Entrada de usuário, argumentos ($1, $2, $@) (teoria: 20min)
- **Prática:** Script de setup inicial de servidor (75min)

### **Dia 3 - Shell Script - Parte 2 (2h)**
- Condicionais: if, case (teoria: 25min)
- Loops: for, while (teoria: 20min)
- Funções e debugging (teoria: 15min)
- **Prática:** Script de monitoramento de recursos (60min)

### **Dia 4 - Logs e Troubleshooting (2h)**
- Sistema de logs: /var/log, syslog, journalctl (teoria: 30min)
- awk e sed básico (teoria: 25min)
- **Prática:** Análise e parsing de logs (65min)

---

# 📦 BLOCO 2: VIRTUALIZAÇÃO E IaC BÁSICO (1 semana)

## Semana 3 - Vagrant

### **Dia 1 - Fundamentos Vagrant (2h)**
- Conceitos de virtualização (teoria: 20min)
- Instalação e Vagrantfile básico (teoria: 25min)
- **Prática:** Primeira VM com Vagrant (75min)

### **Dia 2 - Configuração Avançada (2h)**
- Provedores: VirtualBox, VMware (teoria: 20min)
- Configuração de rede (teoria: 25min)
- **Prática:** Multi-VM com rede privada (75min)

### **Dia 3 - Provisionamento (2h)**
- Shell provisioning (teoria: 20min)
- Compartilhamento de pastas (teoria: 15min)
- **Prática:** VM provisionada com stack LAMP (85min)

### **Dia 4 - Vagrant Boxes (2h)**
- Criando boxes customizadas (teoria: 30min)
- **Prática:** Criar e compartilhar box própria (90min)

### **Dia 5 - Projeto Integrado (2h)**
- **Prática Completa:** Ambiente dev com 3 VMs (app, db, cache) (120min)

---

# 🌿 BLOCO 3: CONTROLE DE VERSÃO (1.5 semanas)

## Semana 4 - Git Essencial

### **Dia 1 - Fundamentos Git (2h)**
- Conceitos: repositório, commit, staging (teoria: 30min)
- Instalação e configuração inicial (teoria: 15min)
- **Prática:** Primeiro repositório e commits (75min)

### **Dia 2 - Operações Básicas (2h)**
- git add, commit, status, log, diff (teoria: 25min)
- .gitignore (teoria: 15min)
- **Prática:** Projeto com histórico limpo (80min)

### **Dia 3 - Conventional Commits (2h)**
- Padrão de mensagens: feat, fix, docs, etc (teoria: 30min)
- Semantic versioning (teoria: 20min)
- **Prática:** Refatorar histórico com commits convencionais (70min)

### **Dia 4 - Branches (2h)**
- Estratégias de branching (teoria: 30min)
- git branch, checkout, switch (teoria: 15min)
- **Prática:** Workflow com feature branches (75min)

### **Dia 5 - Merges e Conflitos (2h)**
- Tipos de merge: fast-forward, 3-way (teoria: 25min)
- Resolução de conflitos (teoria: 20min)
- **Prática:** Simular e resolver conflitos complexos (75min)

### **Dia 6 - Git Avançado (2h)**
- Rebase vs merge (teoria: 25min)
- Cherry-pick, stash (teoria: 20min)
- **Prática:** Limpar histórico com rebase interativo (75min)

### **Dia 7 - Tags e Releases (2h)**
- Tags anotadas vs lightweight (teoria: 20min)
- GitHub releases (teoria: 15min)
- **Prática:** Versionamento completo de projeto (85min)

## Semana 5 - GitHub e Colaboração

### **Dia 1 - GitHub Essencial (2h)**
- Repositórios remotos (teoria: 20min)
- Push, pull, fetch, clone (teoria: 25min)
- **Prática:** Sincronizar projeto com GitHub (75min)

### **Dia 2 - Pull Requests (2h)**
- Workflow de colaboração (teoria: 25min)
- Code review (teoria: 20min)
- **Prática:** Simular processo de PR (75min)

### **Dia 3 - Git Flow (2h)**
- Estratégias: Git Flow, GitHub Flow, Trunk-based (teoria: 35min)
- **Prática:** Implementar Git Flow em projeto (85min)

---

# 🤖 BLOCO 4: AUTOMAÇÃO E CONFIGURAÇÃO (2 semanas)

## Semana 6 - Ansible

### **Dia 1 - Fundamentos Ansible (2h)**
- Arquitetura e conceitos (teoria: 30min)
- Instalação e inventory (teoria: 20min)
- **Prática:** Primeira automação com ad-hoc commands (70min)

### **Dia 2 - Playbooks Básicos (2h)**
- Estrutura YAML (teoria: 20min)
- Módulos essenciais (teoria: 25min)
- **Prática:** Playbook de instalação de pacotes (75min)

### **Dia 3 - Variáveis e Templates (2h)**
- Variáveis: group_vars, host_vars (teoria: 25min)
- Jinja2 templates (teoria: 25min)
- **Prática:** Configuração dinâmica com templates (70min)

### **Dia 4 - Roles (2h)**
- Estrutura de roles (teoria: 30min)
- Dependencies e defaults (teoria: 20min)
- **Prática:** Criar role reutilizável (70min)

### **Dia 5 - Ansible Avançado (2h)**
- Handlers e tags (teoria: 20min)
- Ansible Vault (teoria: 20min)
- **Prática:** Playbook com secrets criptografados (80min)

### **Dia 6 - Deploy de Aplicação (2h)**
- Estratégias de deploy (teoria: 25min)
- **Prática:** Deploy completo de app web (95min)

### **Dia 7 - Projeto Integrado (2h)**
- **Prática:** Infraestrutura completa: web + db + monitoring (120min)

## Semana 7 - Ansible + Vagrant

### **Dia 1 - Integração (2h)**
- Vagrant com provisioner Ansible (teoria: 25min)
- **Prática:** VMs provisionadas via Ansible (95min)

### **Dia 2 - Projeto Final (2h)**
- **Prática:** Ambiente completo automatizado (120min)

---

# 🐳 BLOCO 5: CONTAINERS (4 semanas)

## Semana 8 - Docker Fundamentos

### **Dia 1 - Introdução ao Docker (2h)**
- Conceitos: imagens, containers, registry (teoria: 35min)
- Instalação e configuração (teoria: 15min)
- **Prática:** Primeiros containers (70min)

### **Dia 2 - Comandos Essenciais (2h)**
- docker run, ps, stop, rm, logs, exec (teoria: 30min)
- **Prática:** Gerenciamento de ciclo de vida (90min)

### **Dia 3 - Imagens (2h)**
- Layers e cache (teoria: 25min)
- docker pull, push, tag (teoria: 20min)
- **Prática:** Trabalhar com Docker Hub (75min)

### **Dia 4 - Dockerfile Básico (2h)**
- Instruções: FROM, RUN, COPY, CMD, ENTRYPOINT (teoria: 30min)
- **Prática:** Primeira imagem customizada (90min)

### **Dia 5 - Volumes (2h)**
- Tipos de volumes (teoria: 25min)
- Named volumes vs bind mounts (teoria: 20min)
- **Prática:** Persistência de dados (75min)

### **Dia 6 - Redes Docker (2h)**
- Bridge, host, none (teoria: 30min)
- Comunicação entre containers (teoria: 20min)
- **Prática:** App multi-container na mesma rede (70min)

### **Dia 7 - Projeto Prático (2h)**
- **Prática:** App com banco de dados (120min)

## Semana 9 - Docker Avançado

### **Dia 1 - Multi-stage Builds (2h)**
- Conceito e vantagens (teoria: 25min)
- Build vs runtime (teoria: 20min)
- **Prática:** Imagem otimizada para Java/Node (75min)

### **Dia 2 - Otimização de Builds (2h)**
- Cache de dependências (teoria: 25min)
- .dockerignore (teoria: 15min)
- **Prática:** Build 10x mais rápido (80min)

### **Dia 3 - Imagens Distroless (2h)**
- Segurança e tamanho (teoria: 30min)
- **Prática:** App em imagem distroless (90min)

### **Dia 4 - JVM em Containers (2h)**
- Limites de CPU e memória (teoria: 25min)
- Tuning JVM: Xms, Xmx, GC (teoria: 25min)
- **Prática:** App Java com recursos limitados (70min)

### **Dia 5 - Healthchecks e Logs (2h)**
- HEALTHCHECK no Dockerfile (teoria: 20min)
- Estratégias de logging (teoria: 25min)
- **Prática:** Container com health check (75min)

### **Dia 6 - Segurança (2h)**
- Scan de vulnerabilidades (teoria: 25min)
- Non-root user, read-only filesystem (teoria: 25min)
- **Prática:** Hardening de imagem (70min)

### **Dia 7 - Build Avançado (2h)**
- BuildKit e buildx (teoria: 30min)
- **Prática:** Multi-platform builds (90min)

## Semana 10 - Docker Compose

### **Dia 1 - Fundamentos Compose (2h)**
- Estrutura docker-compose.yml (teoria: 30min)
- Services, networks, volumes (teoria: 25min)
- **Prática:** Stack básica (65min)

### **Dia 2 - Configuração Avançada (2h)**
- Variáveis de ambiente e .env (teoria: 25min)
- depends_on e healthcheck (teoria: 20min)
- **Prática:** Stack com dependências (75min)

### **Dia 3 - Múltiplos Ambientes (2h)**
- Override files (teoria: 25min)
- Profiles (teoria: 20min)
- **Prática:** Dev, staging, prod configs (75min)

### **Dia 4 - Redes e Volumes (2h)**
- Redes customizadas (teoria: 25min)
- Named volumes externos (teoria: 20min)
- **Prática:** Isolamento de serviços (75min)

### **Dia 5 - Políticas e Recursos (2h)**
- restart_policy (teoria: 20min)
- Limites de recursos (teoria: 25min)
- **Prática:** Stack resiliente (75min)

### **Dia 6 - Projeto Complexo (2h)**
- **Prática:** App + DB + Cache + Queue (120min)

### **Dia 7 - Projeto Real (2h)**
- **Prática:** Stack completa com monitoring (120min)

## Semana 11 - Docker Profissional

### **Dia 1 - Design Patterns (2h)**
- Sidecar, ambassador, adapter (teoria: 35min)
- **Prática:** Implementar patterns (85min)

### **Dia 2 - Dev Containers (2h)**
- Ambiente de desenvolvimento (teoria: 30min)
- **Prática:** Dev env completo (90min)

### **Dia 3 - Docker Registry (2h)**
- Registry privado (teoria: 30min)
- **Prática:** Setup e uso de registry local (90min)

### **Dia 4 - Troubleshooting (2h)**
- Debug de containers (teoria: 25min)
- Análise de recursos (teoria: 20min)
- **Prática:** Diagnosticar problemas comuns (75min)

### **Dia 5 - Projeto Final Docker (2h)**
- **Prática:** Aplicação production-ready completa (120min)

---

# 🔄 BLOCO 6: CI/CD (2 semanas)

## Semana 12 - GitHub Actions

### **Dia 1 - Fundamentos (2h)**
- Workflows, jobs, steps (teoria: 30min)
- Triggers e eventos (teoria: 20min)
- **Prática:** Primeiro workflow (70min)

### **Dia 2 - CI Básico (2h)**
- Matrix builds (teoria: 25min)
- Caching (teoria: 20min)
- **Prática:** Pipeline de testes (75min)

### **Dia 3 - Actions Avançado (2h)**
- Secrets e environments (teoria: 25min)
- Reusable workflows (teoria: 25min)
- **Prática:** Build e push Docker (70min)

### **Dia 4 - CD com Actions (2h)**
- Deploy strategies (teoria: 30min)
- **Prática:** Deploy automatizado (90min)

## Semana 13 - GitLab CI e Jenkins

### **Dia 1 - GitLab CI Fundamentos (2h)**
- .gitlab-ci.yml (teoria: 30min)
- Stages e jobs (teoria: 20min)
- **Prática:** Pipeline básico (70min)

### **Dia 2 - GitLab Avançado (2h)**
- Runners (teoria: 25min)
- Cache e artifacts (teoria: 20min)
- **Prática:** Pipeline completo (75min)

### **Dia 3 - Jenkins Setup (2h)**
- Instalação com Docker (teoria: 20min)
- Conceitos básicos (teoria: 25min)
- **Prática:** Primeiro job (75min)

### **Dia 4 - Jenkins Pipelines (2h)**
- Declarative vs Scripted (teoria: 30min)
- **Prática:** Pipeline declarativo (90min)

### **Dia 5 - Jenkins Avançado (2h)**
- Plugins essenciais (teoria: 25min)
- Blue Ocean (teoria: 15min)
- **Prática:** Pipeline com Docker (80min)

### **Dia 6 - Projeto CI/CD (2h)**
- **Prática:** Pipeline completo em 2 ferramentas (120min)

### **Dia 7 - Comparativo (2h)**
- Escolher ferramenta para cenários (teoria: 40min)
- **Prática:** Migração de pipeline (80min)

---

# 🌐 BLOCO 7: WEB SERVER E PROXY (1.5 semanas)

## Semana 14 - NGINX

### **Dia 1 - Fundamentos NGINX (2h)**
- Arquitetura e conceitos (teoria: 30min)
- Instalação e estrutura (teoria: 20min)
- **Prática:** Servidor estático básico (70min)

### **Dia 2 - Configuração Avançada (2h)**
- Server blocks (virtual hosts) (teoria: 25min)
- Location blocks (teoria: 20min)
- **Prática:** Múltiplos sites no mesmo servidor (75min)

### **Dia 3 - Reverse Proxy (2h)**
- Conceitos de proxy reverso (teoria: 25min)
- Configuração proxy_pass (teoria: 20min)
- **Prática:** NGINX como reverse proxy (75min)

### **Dia 4 - Load Balancer (2h)**
- Algoritmos: round-robin, least_conn, ip_hash (teoria: 30min)
- Healthchecks (teoria: 20min)
- **Prática:** LB com 3 backends (70min)

### **Dia 5 - NGINX + Docker (2h)**
- Imagem customizada (teoria: 20min)
- Config via volumes (teoria: 20min)
- **Prática:** NGINX containerizado (80min)

### **Dia 6 - NGINX + Compose (2h)**
- Proxy para múltiplos serviços (teoria: 25min)
- **Prática:** Gateway com NGINX (95min)

### **Dia 7 - NGINX Avançado (2h)**
- Rate limiting (teoria: 20min)
- Cache reverso (teoria: 20min)
- SSL/TLS (teoria: 15min)
- **Prática:** NGINX hardened (65min)

## Semana 15 - NGINX Profissional

### **Dia 1 - Reescrita de URLs (2h)**
- Rewrite rules (teoria: 30min)
- **Prática:** Regras complexas de reescrita (90min)

### **Dia 2 - Logs e Monitoring (2h)**
- Formato de logs customizado (teoria: 25min)
- Análise de logs (teoria: 20min)
- **Prática:** Logs estruturados JSON (75min)

### **Dia 3 - API Gateway (2h)**
- Conceito de API Gateway (teoria: 30min)
- **Prática:** Mini API Gateway local (90min)

### **Dia 4 - Performance (2h)**
- Tuning de performance (teoria: 30min)
- **Prática:** Otimização completa (90min)

---

# 📊 BLOCO 8: OBSERVABILIDADE (1.5 semanas)

## Semana 16 - Monitoramento

### **Dia 1 - Fundamentos (2h)**
- Métricas, logs, traces (teoria: 35min)
- Observabilidade vs monitoramento (teoria: 25min)
- **Prática:** Conceitos aplicados (60min)

### **Dia 2 - Grafana (2h)**
- Instalação e conceitos (teoria: 25min)
- Dashboards (teoria: 20min)
- **Prática:** Primeiros dashboards (75min)

### **Dia 3 - InfluxDB (2h)**
- Time series database (teoria: 25min)
- InfluxQL básico (teoria: 20min)
- **Prática:** Armazenamento de métricas (75min)

### **Dia 4 - Telegraf (2h)**
- Coleta de métricas (teoria: 25min)
- Plugins (teoria: 20min)
- **Prática:** Coletar métricas do sistema (75min)

### **Dia 5 - Stack TICK (2h)**
- Integração Telegraf + InfluxDB + Grafana (teoria: 30min)
- **Prática:** Stack completa (90min)

### **Dia 6 - Prometheus + Grafana (2h)**
- Prometheus basics (teoria: 30min)
- **Prática:** Monitoramento com Prometheus (90min)

### **Dia 7 - Alertas (2h)**
- Configuração de alertas (teoria: 25min)
- **Prática:** Sistema de alertas funcional (95min)

## Semana 17 - Logs e APM

### **Dia 1 - ELK Stack Intro (2h)**
- Elasticsearch, Logstash, Kibana (teoria: 35min)
- **Prática:** Setup básico (85min)

### **Dia 2 - Logs Centralizados (2h)**
- Coleta de logs com Filebeat (teoria: 25min)
- **Prática:** Centralização de logs (95min)

### **Dia 3 - Projeto Observabilidade (2h)**
- **Prática:** Stack completa de observabilidade (120min)

---

# ☸️ BLOCO 9: ORQUESTRAÇÃO (2 semanas)

## Semana 18 - Kubernetes Fundamentos

### **Dia 1 - Introdução K8s (2h)**
- Arquitetura: control plane, nodes (teoria: 35min)
- Instalação: minikube, kind (teoria: 20min)
- **Prática:** Cluster local (65min)

### **Dia 2 - Pods (2h)**
- Conceito de Pod (teoria: 25min)
- kubectl essencial (teoria: 20min)
- **Prática:** Deploy de Pods (75min)

### **Dia 3 - Deployments (2h)**
- ReplicaSets (teoria: 20min)
- Rolling updates (teoria: 25min)
- **Prática:** Deployment com updates (75min)

### **Dia 4 - Services (2h)**
- ClusterIP, NodePort, LoadBalancer (teoria: 30min)
- **Prática:** Expor aplicações (90min)

### **Dia 5 - ConfigMaps e Secrets (2h)**
- Configuração de aplicações (teoria: 30min)
- **Prática:** App configurável (90min)

### **Dia 6 - Volumes (2h)**
- PV e PVC (teoria: 30min)
- StorageClass (teoria: 20min)
- **Prática:** Persistência em K8s (70min)

### **Dia 7 - Projeto Básico (2h)**
- **Prática:** App completa com DB (120min)

## Semana 19 - Kubernetes Avançado

### **Dia 1 - StatefulSets (2h)**
- Aplicações stateful (teoria: 30min)
- **Prática:** Deploy de banco de dados (90min)

### **Dia 2 - Ingress (2h)**
- Ingress controllers (teoria: 30min)
- **Prática:** Roteamento HTTP (90min)

### **Dia 3 - Autoscaling (2h)**
- HPA e VPA (teoria: 30min)
- **Prática:** Scaling automático (90min)

### **Dia 4 - Namespaces e RBAC (2h)**
- Isolamento e segurança (teoria: 35min)
- **Prática:** Multi-tenant cluster (85min)

### **Dia 5 - Helm (2h)**
- Package manager para K8s (teoria: 30min)
- **Prática:** Deploy com Helm charts (90min)

### **Dia 6 - Troubleshooting (2h)**
- Debug de aplicações (teoria: 25min)
- **Prática:** Resolver problemas comuns (95min)

### **Dia 7 - Projeto K8s (2h)**
- **Prática:** Deploy completo microserviços (120min)

---

# 🏗️ BLOCO 10: INFRAESTRUTURA COMO CÓDIGO (2 semanas)

## Semana 20 - Terraform

### **Dia 1 - Fundamentos Terraform (2h)**
- IaC e conceitos (teoria: 30min)
- HCL syntax (teoria: 25min)
- **Prática:** Primeiro recurso (65min)

### **Dia 2 - Recursos e Provedores (2h)**
- Providers (teoria: 25min)
- Resources e data sources (teoria: 25min)
- **Prática:** Múltiplos recursos (70min)

### **Dia 3 - State (2h)**
- Terraform state (teoria: 30min)
- Remote state (teoria: 25min)
- **Prática:** State no S3/backend (65min)

### **Dia 4 - Variáveis e Outputs (2h)**
- Variables, locals, outputs (teoria: 30min)
- **Prática:** Código reutilizável (90min)

### **Dia 5 - Módulos (2h)**
- Criação de módulos (teoria: 30min)
- Registry público (teoria: 20min)
- **Prática:** Módulo customizado (70min)

### **Dia 6 - Terraform Avançado (2h)**
- Workspaces (teoria: 20min)
- Provisioners (teoria: 20min)
- **Prática:** Multi-ambiente (80min)

### **Dia 7 - Projeto Terraform (2h)**
- **Prática:** Infra completa modular (120min)

## Semana 21 - Terraform na Prática

### **Dia 1 - Terraform + Docker (2h)**
- Provider Docker (teoria: 20min)
- **Prática:** Gerenciar containers (100min)

### **Dia 2 - Terraform + Kubernetes (2h)**
- Provider Kubernetes (teoria: 25min)
- **Prática:** Deploy K8s via Terraform (95min)

### **Dia 3 - Boas Práticas (2h)**
- Estrutura de projeto (teoria: 30min)
- Testing (teoria: 25min)
- **Prática:** Refatorar código (65min)

### **Dia 4 - Projeto Final IaC (2h)**
- **Prática:** Infra completa automatizada (120min)

---

# ☁️ BLOCO 11: CLOUD AWS (3.5 semanas)

## Semana 22 - AWS Fundamentos

### **Dia 1 - Introdução AWS (2h)**
- Visão geral de serviços (teoria: 40min)
- Console e CLI (teoria: 20min)
- **Prática:** Setup conta e CLI (60min)

### **Dia 2 - IAM (2h)**
- Users, groups, roles, policies (teoria: 35min)
- **Prática:** Configurar IAM security (85min)

### **Dia 3 - VPC (2h)**
- Subnets, routing, gateways (teoria: 35min)
- **Prática:** Criar VPC customizada (85min)

### **Dia 4 - EC2 - Parte 1 (2h)**
- Instâncias, tipos, AMIs (teoria: 30min)
- Security groups (teoria: 20min)
- **Prática:** Lançar e configurar instância (70min)

### **Dia 5 - EC2 - Parte 2 (2h)**
- EBS, snapshots (teoria: 25min)
- Load Balancers (teoria: 25min)
- **Prática:** Auto Scaling Group (70min)

### **Dia 6 - S3 (2h)**
- Buckets, objects, versionamento (teoria: 30min)
- **Prática:** Storage e website estático (90min)

### **Dia 7 - Route 53 (2h)**
- DNS na AWS (teoria: 30min)
- **Prática:** Configurar domínio (90min)

## Semana 23 - AWS Backend Services

### **Dia 1 - RDS (2h)**
- Bancos gerenciados (teoria: 25min)
- Backups e réplicas (teoria: 20min)
- **Prática:** MySQL RDS (75min)

### **Dia 2 - Lambda (2h)**
- Serverless computing (teoria: 30min)
- **Prática:** Funções Lambda (90min)

### **Dia 3 - API Gateway (2h)**
- REST APIs (teoria: 30min)
- **Prática:** API + Lambda (90min)

### **Dia 4 - SQS + SNS (2h)**
- Mensageria (teoria: 30min)
- **Prática:** Sistema de filas e notificações (90min)

### **Dia 5 - DynamoDB (2h)**
- NoSQL na AWS (teoria: 30min)
- **Prática:** CRUD DynamoDB (90min)

### **Dia 6 - CloudWatch (2h)**
- Logs e métricas (teoria: 25min)
- **Prática:** Monitoramento completo (95min)

### **Dia 7 - Projeto AWS Backend (2h)**
- **Prática:** API completa serverless (120min)

## Semana 24 - AWS Containers

### **Dia 1 - ECR (2h)**
- Registry Docker na AWS (teoria: 20min)
- **Prática:** Push de imagens (100min)

### **Dia 2 - ECS - Parte 1 (2h)**
- Tasks e services (teoria: 30min)
- **Prática:** Deploy com Fargate (90min)

### **Dia 3 - ECS - Parte 2 (2h)**
- ALB integration (teoria: 25min)
- **Prática:** Load balanced service (95min)

### **Dia 4 - EKS Intro (2h)**
- Kubernetes gerenciado (teoria: 30min)
- **Prática:** Cluster EKS básico (90min)

### **Dia 5 - Cognito (2h)**
- Autenticação (teoria: 30min)
- **Prática:** User pool (90min)

## Semana 25 - LocalStack

### **Dia 1 - Introdução LocalStack (2h)**
- AWS local via Docker (teoria: 30min)
- **Prática:** Setup LocalStack (90min)

### **Dia 2 - AWS CLI Local (2h)**
- Configuração endpoint (teoria: 20min)
- **Prática:** S3 e SQS local (100min)

### **Dia 3 - Lambda Local (2h)**
- Funções serverless local (teoria: 25min)
- **Prática:** Lambda + API Gateway local (95min)

### **Dia 4 - DynamoDB Local (2h)**
- NoSQL local (teoria: 20min)
- **Prática:** CRUD completo local (100min)

### **Dia 5 - Terraform + LocalStack (2h)**
- IaC para ambiente local (teoria: 25min)
- **Prática:** Infra AWS local automatizada (95min)

### **Dia 6 - Projeto LocalStack (2h)**
- **Prática:** Sistema completo AWS local (120min)

---

# 🎯 BLOCO 12: PROJETOS FINAIS (2 semanas)

## Semana 26 - Projeto Integrado 1

### **Dias 1-7 (14h total)**
- **Prática Completa:** Sistema e-commerce
  - Frontend (React/Vue)
  - Backend API (Node/Java/Python)
  - Banco PostgreSQL
  - Cache Redis
  - Message Queue (RabbitMQ)
  - Deploy com Docker Compose
  - CI/CD completo
  - Monitoramento
  - NGINX como proxy

## Semana 27 - Projeto Integrado 2

### **Dias 1-7 (14h total)**
- **Prática Completa:** Deploy em Cloud
  - Terraform para provisionar AWS
  - Kubernetes para orquestração
  - Pipeline completo GitHub Actions
  - Monitoring com Prometheus + Grafana
  - Logs centralizados
  - Auto scaling
  - Disaster recovery
  - Documentação completa

---

# 📚 CONTEÚDOS ADICIONAIS IMPORTANTES

## Tópicos Essenciais Adicionados:

### Segurança DevOps (DevSecOps)
- Scan de vulnerabilidades
- Secret management
- Hardening de containers
- Least privilege principle
- Network policies

### Networking
- DNS
- Load balancers
- Proxies
- Firewalls
- VPNs

### Observabilidade Completa
- Distributed tracing
- APM (Application Performance Monitoring)
- Logs centralizados
- SLIs, SLOs, SLAs

### Metodologias
- 12-factor app
- Microservices patterns
- Event-driven architecture
- Design patterns para containers

### Troubleshooting
- Debug de containers
- Debug de cluster K8s
- Análise de performance
- Root cause analysis

---

# 🎓 CRONOGRAMA RESUMIDO

| Semanas | Tema | Carga |
|---------|------|-------|
| 1-2 | Linux Completo | 3 semanas |
| 3 | Vagrant | 1 semana |
| 4-5 | Git/GitHub | 1.5 semanas |
| 6-7 | Ansible | 2 semanas |
| 8-11 | Docker Completo | 4 semanas |
| 12-13 | CI/CD | 2 semanas |
| 14-15 | NGINX | 1.5 semanas |
| 16-17 | Monitoramento | 1.5 semanas |
| 18-19 | Kubernetes | 2 semanas |
| 20-21 | Terraform | 2 semanas |
| 22-25 | AWS + LocalStack | 3.5 semanas |
| 26-27 | Projetos Finais | 2 semanas |

**Total: ~27 semanas (6.5 meses)**

---

# 💡 DICAS DE ESTUDO

## Organização Diária
- **00-40min:** Teoria (leitura + anotações)
- **40-120min:** Prática hands-on
- **Revisão semanal:** 2h aos domingos

## Recursos
- Documentação oficial (sempre!)
- Labs gratuitos: Play with Docker, K8s playground
- GitHub para salvar práticas
- Blog pessoal para documentar aprendizado

## Critérios de Progresso
- Só avance se conseguir refazer a prática sem consulta
- Mantenha repositório Git com todos os exercícios
- Documente problemas e soluções

---

# 🔗 RECURSOS ESSENCIAIS

- **Linux:** Linux Journey, OverTheWire
- **Docker:** Docker Docs, Docker Mastery (Udemy)
- **Kubernetes:** Kubernetes Docs, K8s the Hard Way
- **Terraform:** HashiCorp Learn
- **AWS:** AWS Skill Builder, AWS Free Tier
- **Git:** Pro Git Book (gratuito)
- **CI/CD:** Documentação oficial de cada ferramenta

---

**Boa sorte na sua jornada DevOps! 🚀**
