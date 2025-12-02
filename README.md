# 🚀 GitHub Actions CI/CD Deployment Workflow

[![Deploy to GitHub Pages](https://github.com/Crise-Ergodica/gh-deployment-workflow/actions/workflows/deploy.yml/badge.svg)](https://github.com/Crise-Ergodica/gh-deployment-workflow/actions/workflows/deploy.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://crise-ergodica.github.io/gh-deployment-workflow/)

Projeto prático de **Continuous Integration (CI)** e **Continuous Deployment (CD)** usando **GitHub Actions** para deploy automático de site estático no **GitHub Pages**.

> 🗺️ **Projeto baseado em**: [roadmap.sh - GitHub Actions Deployment Workflow](https://roadmap.sh/projects/github-actions-deployment-workflow)

## 🎯 Objetivo do Projeto

Aprender os conceitos fundamentais de **CI/CD** criando um workflow automatizado que:

- ✅ Detecta mudanças no arquivo `index.html`
- ✅ Executa automaticamente o build
- ✅ Faz deploy no GitHub Pages
- ✅ Disponibiliza o site publicamente

## 🌐 Site ao Vivo

**Acesse**: [https://crise-ergodica.github.io/gh-deployment-workflow/](https://crise-ergodica.github.io/gh-deployment-workflow/)

O site é atualizado **automaticamente** a cada commit que modifica `index.html` no branch `main`!

## ✨ Características

### 📦 Estrutura do Projeto

```
gh-deployment-workflow/
├── .github/
│   └── workflows/
│       └── deploy.yml        # Workflow do GitHub Actions
├── index.html              # Site estático
└── README.md               # Este arquivo
```

### 🔄 Workflow CI/CD

**Trigger**: Apenas quando `index.html` é modificado no branch `main`

```yaml
on:
  push:
    branches:
      - main
    paths:
      - 'index.html'
```

**Jobs**:
1. **Build** - Prepara o site para deploy
2. **Deploy** - Publica no GitHub Pages

## 🚀 Como Funciona

### **Passo 1: Commit & Push**
```bash
# Editar index.html
nano index.html

# Commit
git add index.html
git commit -m "feat: update homepage"

# Push (ISSO DISPARA O WORKFLOW!)
git push origin main
```

### **Passo 2: GitHub Actions Executa Automaticamente**
```
📦 Checkout do código
🔧 Configura GitHub Pages
🏗️ Build do site
📤 Upload do artifact
🚀 Deploy no GitHub Pages
✨ Site publicado!
```

### **Passo 3: Site Atualizado em ~30 segundos**
```
🌐 https://crise-ergodica.github.io/gh-deployment-workflow/
```

## 💻 Instalação e Uso

### **1. Clonar o Repositório**

```bash
git clone https://github.com/Crise-Ergodica/gh-deployment-workflow.git
cd gh-deployment-workflow
```

### **2. Modificar o Site**

```bash
# Editar index.html
nano index.html

# Testar localmente
python -m http.server 8000
# Acesse: http://localhost:8000
```

### **3. Fazer Deploy Automático**

```bash
git add index.html
git commit -m "feat: nova versão do site"
git push origin main

# O GitHub Actions fará deploy automaticamente!
```

### **4. Acompanhar o Workflow**

```
👁️ GitHub → Actions → Deploy to GitHub Pages
```

Ou visite: [https://github.com/Crise-Ergodica/gh-deployment-workflow/actions](https://github.com/Crise-Ergodica/gh-deployment-workflow/actions)

## 🔧 Configuração do GitHub Pages

### **Habilitar GitHub Pages (se necessário)**

1. Vá em **Settings** → **Pages**
2. **Source**: GitHub Actions
3. **Branch**: main
4. Salvar

**O workflow já está configurado com as permissões corretas!**

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

## 📊 Anatomia do Workflow

### **deploy.yml Explicado**

```yaml
name: Deploy to GitHub Pages

# 1. TRIGGER - Quando executar?
on:
  push:
    branches:
      - main          # Apenas no branch main
    paths:
      - 'index.html'  # Apenas quando index.html mudar

# 2. PERMISSÕES - O que pode fazer?
permissions:
  contents: read      # Ler o repositório
  pages: write        # Escrever no Pages
  id-token: write     # Token de autenticação

# 3. JOBS - O que fazer?
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4           # Baixa o código
      - uses: actions/configure-pages@v4    # Configura Pages
      - run: echo "🚀 Building..."           # Build (pode ser complexo)
      - uses: actions/upload-pages-artifact@v3  # Empacota site

  deploy:
    needs: build                            # Espera build terminar
    runs-on: ubuntu-latest
    steps:
      - uses: actions/deploy-pages@v4       # Faz deploy!
```

## 🎓 Conceitos Aprendidos

### **1. GitHub Actions**
- Workflows YAML
- Triggers (on: push, paths)
- Jobs e steps
- Actions do marketplace
- Artifacts

### **2. GitHub Pages**
- Hospedagem gratuita
- Deploy via Actions
- URLs personalizadas
- HTTPS automático

### **3. CI/CD**
- Continuous Integration
- Continuous Deployment
- Automação de deploy
- Pipeline de publicação

### **4. DevOps Prático**
- Versionamento com Git
- Automação de tarefas
- Infraestrutura como código
- Monitoramento de builds

## 🚀 Próximos Passos (Metas Adicionais)

### **Nível 2: Site com Gerador Estático**

```bash
# Usar Hugo, Jekyll, Astro, etc.
# Workflow mais complexo com build steps
```

### **Nível 3: Portfólio Pessoal**

```bash
# CV online
# Projetos
# Blog
# Contato
```

### **Nível 4: Testes Automatizados**

```yaml
jobs:
  test:
    - run: npm test        # Testes unitários
    - run: npm run lint    # Linter
  
  deploy:
    needs: test            # Só deploya se passar nos testes
```

### **Nível 5: Múltiplos Ambientes**

```yaml
# Staging: dev branch → staging.github.io
# Production: main branch → github.io
```

## 📊 Status do Workflow

Veja o status dos deploys:

[![Deploy Status](https://github.com/Crise-Ergodica/gh-deployment-workflow/actions/workflows/deploy.yml/badge.svg)](https://github.com/Crise-Ergodica/gh-deployment-workflow/actions)

## 🐛 Troubleshooting

### **Erro: "Permissões negadas"**

**Solução**: Verificar permissões do workflow no repositório:
```
Settings → Actions → General → Workflow permissions
✅ Read and write permissions
```

### **Erro: "Página 404"**

**Solução**: Esperar 1-2 minutos após o deploy. Verificar:
```
Settings → Pages → Your site is live at...
```

### **Workflow não executou**

**Solução**: Verificar se modificou `index.html` no branch `main`:
```bash
git log --oneline -1  # Último commit
git diff HEAD~1 HEAD index.html  # Mudanças
```

## 📚 Recursos Adicionais

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [YAML Syntax](https://yaml.org/spec/1.2/spec.html)
- [roadmap.sh - DevOps Roadmap](https://roadmap.sh/devops)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)

## 📝 Licença

MIT License - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 👤 Autor

**Aurora Ergodica**
- GitHub: [@Crise-Ergodica](https://github.com/Crise-Ergodica)
- Email: gdcm10@gmail.com
- Portfólio: [DevOps Roadmap](https://github.com/Crise-Ergodica/DevOps-roadmap)

## 🔗 Projetos Relacionados

- [📊 Linux Server Stats](https://github.com/Crise-Ergodica/Linux-server-stats)
- [📈 Nginx Log Analyser](https://github.com/Crise-Ergodica/nginx-log-analyser)
- [📦 Log Archive Tool](https://github.com/Crise-Ergodica/log-archive-tool)

---

<div align="center">

**🎉 Deploy automático ativo!**

**Modifique `index.html` e veja a mágica acontecer!**

*"God's in His heaven, all's right with the world!"*

Feito com ❤️ por [Aurora Ergodica](https://github.com/Crise-Ergodica)

</div>
