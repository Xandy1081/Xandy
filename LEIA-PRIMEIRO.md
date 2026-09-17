# KANEKI STORE 1.0.1

Projeto novo e independente, pronto para Vercel + Supabase + Google OAuth + Mercado Pago PIX.

## Ordem correta

1. Crie um projeto **novo** no Supabase.
2. Execute `supabase.sql` no SQL Editor.
3. Configure Google OAuth conforme `TUTORIAL-INSTALACAO.md`.
4. O arquivo `supabase-config.js` já está conectado ao novo projeto Supabase da KANEKI STORE.
5. Cadastre o primeiro administrador usando a instrução no final de `supabase.sql`.
6. Importe esta pasta no Vercel e cadastre as variáveis de `.env.example`.
7. Configure o webhook do Mercado Pago.

Painel administrativo: `/admin.html` (também responde em `/admin`).

O catálogo começa vazio de propósito. Cadastre categorias e produtos no painel ADM. O banner atual é apenas um espaço substituível; envie sua arte do Kaneki pelo painel depois.

Nunca publique `.env`, Service Role, Access Token ou segredo do webhook.
