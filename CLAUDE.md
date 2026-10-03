# Dashboard Finanças (PetinatiFinance)

Dashboard financeiro pessoal em arquivo único: `index.html` (~8.800 linhas, HTML + CSS + JS inline). Sem build, sem package.json.

- Repo: https://github.com/Petinati2201/PetinatiFinance (branch `main`)
- Libs via CDN: Chart.js, PapaParse, Supabase JS, SheetJS (xlsx), pdf.js. Dados na Supabase + localStorage.
- Idioma da interface, dos comentários e dos commits: português (pt-BR). Valores no formato brasileiro (ponto = milhar, vírgula = decimal; ver `parseBRL`).

## Como trabalhar
- Edite só o `index.html`, salvo pedido em contrário. Não crie arquivos novos nem adicione frameworks/dependências sem eu pedir.
- Arquivo grande: use Grep para localizar a função/seção e leia só o trecho necessário. Não releia o arquivo inteiro.
- Mudanças pequenas e cirúrgicas; siga o estilo existente (nomes, indentação, comentários com `// ───`).
- Ao mexer em tela, lembre do tema claro/escuro e do layout mobile.
- Antes de commitar, valide a sintaxe do JS (extrair o `<script>` e rodar `node --check`) e, se der, abra a página para ver se há erros no console.

## Deploy
- O deploy é o `git push` na `main` (publicação automática a partir do repo).
- Commits curtos, em português, no padrão do histórico: `fix: ...`, `feat: ...`, `refactor: ...`.
- NÃO faça push sem eu aprovar: mostre o resumo do diff e pergunte. Depois de aprovado: commit + push.

## Dados sensíveis
- Repo público: nunca coloque no arquivo dados financeiros reais, senhas, nem chaves privadas/service-role da Supabase. Só a chave pública (anon) pode existir no código.
