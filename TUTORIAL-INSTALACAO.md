# Instalação da KANEKI STORE

## 1. Supabase novo

Crie um projeto exclusivo para a KANEKI STORE. Em **SQL Editor**, cole e execute todo o arquivo `supabase.sql`. Ele cria tabelas, índices, funções, triggers lógicos, RLS, buckets e Realtime. Não execute no projeto da REZEX STORE.

Em **Project Settings → API**, copie a URL do projeto e a chave pública `anon/publishable`. Cole somente essas duas informações em `supabase-config.js`. Copie também a `service_role`, mas coloque-a exclusivamente nas variáveis da Vercel.

## 2. Google OAuth

No Google Cloud, crie um cliente OAuth do tipo Web. Em **Authorized JavaScript origins**, cadastre:

- `http://localhost:3000` (opcional para testes)
- `https://SEU-PROJETO.vercel.app`
- `https://SEU-DOMINIO.com.br`

Em **Authorized redirect URIs**, cadastre exatamente:

- `https://SEU-PROJETO-SUPABASE.supabase.co/auth/v1/callback`

No Supabase, abra **Authentication → Providers → Google**, ative o provedor e informe Client ID e Client Secret. Em **Authentication → URL Configuration**, use o domínio final como Site URL e adicione:

- `https://SEU-PROJETO.vercel.app/**`
- `https://SEU-DOMINIO.com.br/**`
- `http://localhost:3000/**` (opcional)

## 3. Primeiro administrador

Entre uma vez com Google na loja para o usuário aparecer em `auth.users`. Depois, no SQL Editor, execute a linha indicada no final de `supabase.sql`, trocando `SEUEMAIL@gmail.com`. Somente e-mails cadastrados em `admin_users` entram no painel.

## 4. Mercado Pago PIX

No painel de desenvolvedores do Mercado Pago, crie uma aplicação, obtenha o Access Token de produção e crie uma assinatura secreta para Webhooks. Na Vercel, adicione:

- `MERCADOPAGO_ACCESS_TOKEN`
- `MERCADOPAGO_WEBHOOK_SECRET`

Cadastre o evento **Payments** apontando para:

- `https://SEU-DOMINIO.com.br/api/mercadopago-webhook`

O webhook verifica HMAC, consulta o pagamento diretamente no Mercado Pago, compara ID, pedido e valor, e usa função idempotente no banco. O navegador nunca aprova pagamentos.

## 5. Variáveis da Vercel

Copie os nomes de `.env.example` para **Vercel → Project Settings → Environment Variables**. Use os valores do projeto novo. `PUBLIC_SITE_URL` precisa começar com `https://` e não deve terminar com `/`.

Para limpeza agendada, use `CRON_SECRET` longo e faça uma chamada autorizada a `/api/cleanup-expired` com `Authorization: Bearer SEU_CRON_SECRET`. O próprio fluxo do PIX também libera reservas expiradas quando consultado.

## 6. Publicar na Vercel

Compacte o conteúdo da pasta sem criar uma pasta extra, importe em **Vercel → Add New → Project**, mantenha o preset como “Other” e publique. Não há etapa de build.

Depois do primeiro deploy, confira:

- Loja: `/`
- Painel ADM: `/admin.html`
- Login Google e retorno ao domínio
- Criação de produto sem produto de demonstração
- PIX com valor correto
- Webhook aprovado
- Ticket privado após pagamento

## 7. Domínio

Em **Vercel → Settings → Domains**, adicione o domínio. Copie os registros DNS mostrados pela Vercel para seu provedor. Depois que ficar “Valid Configuration”, atualize `PUBLIC_SITE_URL`, as URLs permitidas do Supabase e as origens do Google Cloud.

## 8. Banner e imagens

O banner inicial é propositalmente neutro. No painel ADM, em **Visual do site**, envie ou informe a URL da arte definitiva. Os buckets aceitam JPEG, PNG, WebP e GIF de até 8 MB. Use imagens otimizadas em WebP quando possível.
