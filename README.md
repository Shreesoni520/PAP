# Reporta Évora

Plataforma web para registo e gestão de ocorrências urbanas na cidade de Évora. O projeto inclui um **site público** para cidadãos e um **painel de administração** para funcionários e administradores.

---

## Índice

- [Sobre o projeto](#sobre-o-projeto)
- [Parte pública](#parte-pública)
- [Parte de administração](#parte-de-administração)
- [Tecnologias](#tecnologias)
- [Requisitos](#requisitos)
- [Instalação](#instalação)
- [Configuração de segredos](#configuração-de-segredos)
- [Base de dados](#base-de-dados)
- [URLs principais](#urls-principais)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Dependências PHP](#dependências-php)
- [Mover para outro PC](#mover-para-outro-pc)
- [GitHub](#github)

---

## Sobre o projeto

O **Reporta Évora** permite que os cidadãos consultem informação útil, reportem ocorrências no espaço urbano, leiam notícias e interajam com a plataforma através de uma conta pessoal.

Do lado da administração, a equipa pode gerir árvores, estados de intervenção, ocorrências, notícias, utilizadores, mensagens de contacto e newsletter.

---

## Parte pública

Site acessível em `http://localhost/PAP/`

### Funcionalidades

| Área | Descrição |
|------|-----------|
| **Início** | Página principal com destaques e acesso rápido às secções |
| **Informação útil** | Informação para o cidadão sobre o sistema e serviços |
| **Mapa 2D** | Visualização geográfica de ocorrências e espaços verdes |
| **Ocorrências urbanas** | Reporte de problemas no espaço público com localização e foto |
| **Ocorrências de estrada** | Reporte de problemas rodoviários com localização e foto |
| **Listagens públicas** | Consulta de ocorrências urbanas e de estrada |
| **Notícias** | Leitura de notícias; comentários exigem login e usam o nome da conta |
| **Contacto** | Formulário de mensagens; utilizadores autenticados usam nome/email da conta |
| **Newsletter** | Subscrição com confirmação por email (requer login) |
| **Conta pública** | Registo, login, perfil, segurança e recuperação de palavra-passe |
| **Área pessoal** | As minhas ocorrências e as minhas mensagens |

### Conta pública

Os cidadãos podem:

- Criar conta e iniciar sessão
- Gerir perfil (nome, email, telefone, foto, etc.)
- Ativar autenticação em dois fatores (2FA) por email
- Recuperar palavra-passe
- Ver as suas ocorrências e mensagens de contacto
- Comentar notícias apenas com o nome associado à conta

### Rotas públicas

O site público usa o parâmetro `evora_p` em `index.php`:

```
index.php?evora_p=inicio
index.php?evora_p=login
index.php?evora_p=signup
index.php?evora_p=profile
index.php?evora_p=noticias
index.php?evora_p=mapa
index.php?evora_p=ocorrencias
index.php?evora_p=ocorrenciasestrada
index.php?evora_p=contact
index.php?evora_p=information
```

---

## Parte de administração

Painel acessível em `http://localhost/PAP/Admin/`

### Tipos de utilizador

| Tipo | Acesso |
|------|--------|
| **Funcionário** | Dashboard, mapas, ocorrências, intervenções, perfil e segurança |
| **Administrador** | Tudo o que o funcionário tem + gestão de árvores, estados, notícias, utilizadores, contactos e newsletter |

### Funcionalidades

| Módulo | Descrição |
|--------|-----------|
| **Dashboard** | Estatísticas e gráficos da atividade da plataforma |
| **Mapa 2D unificado** | Visualização administrativa de ocorrências e árvores |
| **Árvores** | Adicionar, listar, editar e remover árvores |
| **Estados** | Gestão dos estados de intervenção |
| **Ocorrências urbanas** | Criar, listar, editar intervenções e remover registos |
| **Ocorrências de estrada** | Criar, listar, editar intervenções e remover registos |
| **Intervenções** | Atribuição e acompanhamento de tarefas por funcionário |
| **Notícias** | Criar, editar, listar e remover notícias |
| **Comentários** | Moderação de comentários nas notícias |
| **Contacto** | Gestão das mensagens enviadas pelo formulário público |
| **Newsletter** | Envio de newsletters aos subscritores |
| **Utilizadores internos** | Gestão de contas de funcionários e administradores |
| **Utilizadores públicos** | Gestão de contas de cidadãos |
| **Perfil e segurança** | Alteração de dados, password e 2FA |
| **Exportação PDF** | Exportação de dados selecionados |
| **Notificações** | Alertas de novas ocorrências e atividade |

### Alertas automáticos

Quando uma ocorrência é registada, o sistema pode:

- Enviar **email** ao administrador
- Enviar **SMS** via Twilio (se configurado)

### Rotas de administração

O painel usa o parâmetro `evora` em `Admin/index.php`:

```
Admin/index.php?evora=inicio
Admin/index.php?evora=mapa2d
Admin/index.php?evora=addocorrencias
Admin/index.php?evora=listocorrencias
Admin/index.php?evora=addnoticias
Admin/index.php?evora=listarnoticias
Admin/index.php?evora=addutilizador
Admin/index.php?evora=profile
Admin/index.php?evora=security
```

---

## Tecnologias

| Camada | Tecnologia |
|--------|------------|
| Backend | PHP 8.0+ |
| Base de dados | MySQL / MariaDB |
| Servidor local | XAMPP (Apache + MySQL) |
| Frontend público | HTML, CSS, Bootstrap, JavaScript |
| Painel admin | Mazer Admin Template, Bootstrap, ApexCharts |
| Email | PHP `mail()` |
| SMS | Twilio SDK |
| PDF | Dompdf |
| Gestão de dependências | Composer |

---

## Requisitos

- **XAMPP** com PHP **8.0 ou superior**
- **MySQL / MariaDB**
- **Composer** (apenas se precisar de reinstalar a pasta `vendor`)

---

## Instalação

### 1. Copiar o projeto

Coloque a pasta do projeto em:

```
C:\xampp\htdocs\PAP
```

### 2. Configurar segredos

Veja a secção [Configuração de segredos](#configuração-de-segredos).

### 3. Importar a base de dados

1. Abra o **phpMyAdmin**
2. Crie ou importe a base de dados **`pap`**
3. Importe o ficheiro SQL do projeto (se disponível)

### 4. Instalar dependências PHP

Se a pasta `vendor` não existir:

```bash
cd C:\xampp\htdocs\PAP
php composer.phar install
```

### 5. Iniciar o servidor

1. Abra o **XAMPP Control Panel**
2. Inicie **Apache** e **MySQL**
3. Aceda a:
   - Público: `http://localhost/PAP/`
   - Admin: `http://localhost/PAP/Admin/`

---

## Configuração de segredos

**Nunca coloque passwords, tokens Twilio ou credenciais dentro do código do projeto.**

### Ficheiro real (fora do projeto)

```
C:\xampp\secrets\pap-secrets.php
```

### Como criar

1. Crie a pasta `C:\xampp\secrets\`
2. Copie `pap-secrets.example.php` para `C:\xampp\secrets\pap-secrets.php`
3. Edite com os seus valores reais:

```php
return [
    'DB_HOST' => 'localhost',
    'DB_USER' => 'root',
    'DB_PASS' => '',
    'DB_NAME' => 'pap',
    'ADMIN_EMAIL' => 'seu-email@exemplo.com',
    'TWILIO_SID'   => 'SEU_TWILIO_SID',
    'TWILIO_TOKEN' => 'SEU_TWILIO_TOKEN',
    'TWILIO_FROM'  => '+1XXXXXXXXXX',
    'TWILIO_TO'    => '+351XXXXXXXXX',
];
```

### Alterar credenciais

Para mudar Twilio, email, base de dados, etc., edite **apenas**:

```
C:\xampp\secrets\pap-secrets.php
```

---

## Base de dados

Nome da base de dados: **`pap`**

### Tabelas principais

| Tabela | Uso |
|--------|-----|
| `users` | Utilizadores do painel admin |
| `users_public` | Utilizadores do site público |
| `ocorrencias` | Ocorrências urbanas |
| `ocorrencias_estrada` | Ocorrências de estrada |
| `arvores` | Árvores / espaços verdes |
| `states` | Estados de intervenção |
| `intervencoes` | Intervenções atribuídas |
| `noticias` | Notícias |
| `comentarios_noticias` | Comentários nas notícias |
| `contact` | Mensagens de contacto |
| `contact_info` | Informações de contacto do site |
| `newsletter_subscribers` | Subscritores da newsletter |
| `notificacoes` | Notificações do admin |
| `atividade` | Registo de atividade dos utilizadores admin |
| `log` | Logs do sistema |

---

## URLs principais

| Página | URL |
|--------|-----|
| Site público | `http://localhost/PAP/` |
| Login público | `http://localhost/PAP/index.php?evora_p=login` |
| Notícias | `http://localhost/PAP/index.php?evora_p=noticias` |
| Mapa público | `http://localhost/PAP/index.php?evora_p=mapa` |
| Contacto | `http://localhost/PAP/index.php?evora_p=contact` |
| Admin | `http://localhost/PAP/Admin/` |
| Login admin | `http://localhost/PAP/Admin/login.php` |

---

## Estrutura do projeto

```
PAP/
├── index.php              # Router do site público
├── config.php             # Ligação à BD e leitura de segredos
├── inicio.php             # Página inicial pública
├── login.php              # Login público
├── signup.php             # Registo público
├── profile.php            # Perfil do cidadão
├── noticias.php           # Notícias e comentários
├── contact.php            # Formulário de contacto
├── ocorrencias.php        # Reportar ocorrência urbana
├── ocorrencias_estrada.php
├── map2d.php              # Mapa público
├── forms/                 # Newsletter e confirmações
├── assets/                # CSS, JS e imagens do site público
├── uploads/               # Fotos e ficheiros enviados (não vai para GitHub)
├── vendor/                # Dependências Composer (Twilio, Dompdf)
├── pap-secrets.example.php
├── composer.json
├── README.md
└── Admin/
    ├── index.php          # Router do painel admin
    ├── config.php         # Usa o config.php da raiz
    ├── login.php          # Login admin
    ├── inicio.php         # Dashboard
    ├── menu.php           # Menu lateral e notificações
    ├── add_*.php          # Páginas de criação
    ├── listar_*.php       # Páginas de listagem
    ├── editar_*.php       # Páginas de edição
    ├── remove_*.php       # Páginas de remoção
    ├── export_pdf.php     # Exportação PDF
    └── assets/            # CSS, JS e recursos do admin
```

### Ficheiro de segredos (fora do projeto)

```
C:\xampp\secrets\pap-secrets.php
```

---

## Dependências PHP

| Pacote | Função |
|--------|--------|
| `twilio/sdk` | Envio de SMS quando ocorrências são registadas |
| `dompdf/dompdf` | Geração de PDFs no painel admin |

Instalação:

```bash
php composer.phar install
```

---

## Mover para outro PC

Copie estes 3 elementos:

1. **Pasta do projeto**
   ```
   C:\xampp\htdocs\PAP
   ```

2. **Ficheiro de segredos**
   ```
   C:\xampp\secrets\pap-secrets.php
   ```

3. **Base de dados** `pap` (exportar no phpMyAdmin e importar no novo PC)

No novo PC:

- Instale XAMPP com PHP 8.0+
- Se `vendor` não existir, execute `php composer.phar install`
- Inicie Apache e MySQL

---

## GitHub

### O que vai para o GitHub

- Código do projeto
- `pap-secrets.example.php` (template sem segredos reais)
- `README.md`

### O que NÃO deve ir para o GitHub

- `C:\xampp\secrets\pap-secrets.php` (segredos reais)
- Pasta `uploads/` (fotos dos utilizadores)
- Pasta `vendor/` (reinstalar com Composer)

### Depois de clonar o repositório

```bash
cd PAP
php composer.phar install
```

Crie também `C:\xampp\secrets\pap-secrets.php` com os seus dados reais.

---

## Notas de segurança

- Comentários em notícias exigem login e usam o nome da conta
- Formulário de contacto usa nome/email da conta quando o utilizador está autenticado
- Segredos (Twilio, BD, email) ficam fora da pasta do projeto
- Logout limpa corretamente os dados de sessão

---

## Autor

Projeto desenvolvido no âmbito da PAP — **Reporta Évora**.
