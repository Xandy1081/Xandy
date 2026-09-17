# Atualização KANEKI STORE

Esta versão mantém a estrutura e os sistemas existentes e adiciona:

- Logo principal usando a imagem enviada, recortada somente para a área circular.
- Barra de categorias no início da loja, acima do banner.
- Categorias públicas ordenadas pela tabela `categories` do Supabase; se a tabela estiver vazia, as categorias dos produtos continuam funcionando como fallback.
- Painel ADM com criação/edição/ordenação/visibilidade de categorias.
- Edição de produtos pelo ADM: nome, categoria, descrição, preço, desconto, estoque, visibilidade e imagem por URL.
- Edição das imagens/configurações visuais do site por URL no ADM.
- Mantidos os fluxos existentes de pedidos, tickets, PIX, avaliações, comunidade e suporte.

## Observação sobre Supabase

As alterações do catálogo e das imagens são salvas no Supabase. O bucket Storage existente continua sendo usado para os arquivos de atendimento. Para imagens do catálogo/site, basta informar uma URL pública no ADM.

A Vercel deve receber as mesmas variáveis de ambiente já usadas pelo projeto.
