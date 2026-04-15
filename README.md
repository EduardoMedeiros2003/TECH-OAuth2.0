# 🔐 Projeto de Autenticação com OAuth2.0 usando Django

## 📌 Visão Geral

Este projeto consiste em uma aplicação web desenvolvida com Django que implementa autenticação de usuários utilizando o protocolo OAuth2.0 com integração ao GitHub.

O objetivo principal é demonstrar, de forma prática e profissional, a implementação de login social, controle de acesso a áreas restritas e boas práticas de segurança em aplicações web.

---

## 🚀 Funcionalidades

* ✅ Autenticação via GitHub (OAuth2.0)
* ✅ Login social utilizando django-allauth
* ✅ Controle de acesso com `@login_required`
* ✅ Área restrita para usuários autenticados
* ✅ Logout funcional
* ✅ Redirecionamento automático após login e logout
* ✅ Gerenciamento seguro de credenciais com variáveis de ambiente
* ✅ Estrutura organizada de arquivos estáticos (CSS, imagens)

---

## 🧱 Tecnologias Utilizadas

* Python 3
* Django
* django-allauth
* HTML5
* CSS3

---

## ⚙️ Configuração do Projeto

### 1. Clone o repositório

```bash
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_PROJETO>
```

### 2. Crie e ative o ambiente virtual

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### 3. Instale as dependências

```bash
pip install -r requirements.txt
```

---

## 🔐 Configuração das Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
GITHUB_CLIENT_ID=seu_client_id
GITHUB_SECRET=seu_client_secret
SECRET_KEY=sua_chave_django
```

⚠️ Importante:

* Nunca versionar o arquivo `.env`
* Adicionar `.env` ao `.gitignore`

---

## 🔗 Configuração do OAuth no GitHub

Crie uma aplicação OAuth no GitHub com as seguintes configurações:

* **Homepage URL:**

```
http://127.0.0.1:8000
```

* **Authorization Callback URL:**

```
http://127.0.0.1:8000/accounts/github/login/callback/
```

⚠️ A URL deve ser exatamente igual (incluindo a barra final `/`)

---

## 🧠 Configurações no Django

### settings.py

```python
LOGIN_REDIRECT_URL = '/members/'
LOGOUT_REDIRECT_URL = '/'
SOCIALACCOUNT_LOGIN_ON_GET = True
ACCOUNT_LOGOUT_ON_GET = True
SITE_ID = 1
```

### Configuração do provider

```python
from decouple import config

SOCIALACCOUNT_PROVIDERS = {
    'github': {
        'APP': {
            'client_id': config('GITHUB_CLIENT_ID'),
            'secret': config('GITHUB_SECRET'),
            'key': ''
        }
    }
}
```

---

## 🌐 Rotas principais

* `/` → Página inicial
* `/members/` → Área restrita (requer login)
* `/accounts/login/` → Login
* `/accounts/logout/` → Logout
* `/accounts/github/login/` → Login com GitHub

---

## 🔒 Controle de Acesso

Utilização do decorator para proteger rotas:

```python
from django.contrib.auth.decorators import login_required

@login_required
def members(request):
    return render(request, 'members.html')
```

---

## 🎨 Interface

* Página inicial com opção de login social
* Área de membros personalizada
* Botão de logout
* Estilização com CSS separado por páginas

---

## 📁 Estrutura do Projeto

```
project/
│
├── static/
│   ├── index.css
│   ├── members.css
│   └── assets/
│       ├── logo.jpeg
│       └── github.svg
│
├── templates/
│   ├── index.html
│   └── members.html
│
├── .env
├── manage.py
```

---

## 🛡️ Boas Práticas Aplicadas

* Uso de variáveis de ambiente para dados sensíveis
* Separação entre arquivos estáticos e templates
* Organização de rotas
* Uso de bibliotecas consolidadas para autenticação
* Controle de sessão seguro

---

## 📈 Possíveis Melhorias Futuras

* Exibir dados do usuário (nome, avatar do GitHub)
* Implementar sistema de permissões (roles)
* Criar dashboard personalizada
* Deploy em produção (Render, Railway, etc.)
* Implementar testes automatizados

---

## 👨‍💻 Autor

Projeto desenvolvido por Eduardo Medeiros.

---

## 📄 Licença

Este projeto está sob a licença MIT.
