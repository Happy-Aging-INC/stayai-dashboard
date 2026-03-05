# Stay.AI Dashboard â Setup para AtualizaÃ§Ã£o AutomÃ¡tica

## O que isso faz
- Todo dia Ã s 8h (horÃ¡rio de BrasÃ­lia), o GitHub Actions roda o script que puxa dados frescos do BigQuery
- Atualiza o dashboard e faz deploy automÃ¡tico no Netlify
- Qualquer pessoa com o link do Netlify sempre vÃª os dados mais recentes

---

## Passo a passo (20 minutos)

### 1. Criar conta no GitHub (se nÃ£o tiver)
â https://github.com/signup

### 2. Criar um repositÃ³rio novo
1. VÃ¡ em https://github.com/new
2. Nome: `stayai-dashboard`
3. Marque **Private** (dados de assinantes)
4. Clique **Create repository**
5. FaÃ§a upload de TODOS os arquivos desta pasta (arraste os arquivos para a pÃ¡gina do repositÃ³rio)

### 3. Criar chave de serviÃ§o no Google Cloud
1. Acesse https://console.cloud.google.com/iam-admin/serviceaccounts?project=happy-aging-466917
2. Clique **+ Create Service Account**
3. Nome: `dashboard-refresh`
4. Clique **Create and Continue**
5. No campo Role, selecione **BigQuery Data Viewer** e **BigQuery Job User**
6. Clique **Done**
7. Clique na conta criada â aba **Keys** â **Add Key** â **Create new key** â **JSON** â **Create**
8. Um arquivo `.json` serÃ¡ baixado â guarde-o com seguranÃ§a

### 4. Criar conta no Netlify
1. Acesse https://app.netlify.com/signup (pode usar a conta do GitHub)
2. Clique **Add new site** â **Import an existing project** â selecione o repositÃ³rio `stayai-dashboard`
3. Clique **Deploy site**
4. Anote o **Site ID** (em Site Settings â General)
5. Crie um **Personal Access Token** em https://app.netlify.com/user/applications#personal-access-tokens

### 5. Configurar os Secrets no GitHub
1. No seu repositÃ³rio, vÃ¡ em **Settings** â **Secrets and variables** â **Actions**
2. Clique **New repository secret** e adicione estes 3 secrets:

| Nome do Secret | Valor |
|---|---|
| `GCP_SERVICE_ACCOUNT_KEY` | O conteÃºdo INTEIRO do arquivo JSON baixado no passo 3 |
| `NETLIFY_AUTH_TOKEN` | O token criado no passo 4.5 |
| `NETLIFY_SITE_ID` | O Site ID anotado no passo 4.4 |

### 6. Testar
1. No repositÃ³rio, vÃ¡ em **Actions** â **Refresh Dashboard Data** â **Run workflow**
2. Espere ~2 minutos
3. Acesse seu link Netlify â os dados devem estar atualizados!

---

## Compartilhar
Basta enviar o link do Netlify (ex: `https://stayai-dashboard.netlify.app`) para quem quiser. A pessoa abre no navegador e vÃª os dados mais recentes.

## AtualizaÃ§Ã£o manual
AlÃ©m da atualizaÃ§Ã£o diÃ¡ria automÃ¡tica, vocÃª pode rodar manualmente a qualquer momento:
â GitHub â Actions â Refresh Dashboard Data â Run workflow
