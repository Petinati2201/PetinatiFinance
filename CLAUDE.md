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

## Aba "Análise de carteira"
- View `view-analise` (menu Investimentos), renderizada por `renderAnalise()` em `index.html`. Lê `public.relatorios_ia` com o login normal (chave anon): pega o `briefing` mais recente e os `ativo` com o mesmo `rodada_id`. Avisa se a rodada tiver mais de 10 dias.
- Texto vem de notícias da web: só insere no DOM via `textContent` (helper `anEl`), nunca `innerHTML`. Nada da carteira fixo no código; a tela não usa as palavras comprar/vender.
- Fluxo: agentes locais (`agente*.mjs`, ficam fora do git) → `npm run publicar` (`publicar-dashboard.mjs`, usa a service key do `.env`, grava 1 rodada) → dashboard. Atalhos: `npm run semanal`, `trimestral`, `tudo` (semanal + trimestral + final + publicar).
- Sub-abas (`anSub`): **Notícias** (padrão; briefing + ativos) e **Seu gestor**. O gestor lê a linha `tipo 'gestor'` mais recente de `relatorios_ia` (`order by gerado_em desc limit 1`), só no primeiro clique (`carregarGestor` / `anGestorHtml`). Avisa se tiver mais de 14 dias. Candidatos ficam num `<details>` recolhido; `mercado_eua` true/null aparecem separados e false só como tickers descartados. Sem botões/selos de comprar/vender: reduzir/aumentar/entrar/sair só como tipo da ideia, em texto.
- Fluxo do gestor: `npm run gestor` (agente7, gera `gestor-carteira.json`) → `npm run publicar` (grava 1 linha `gestor`, idempotente por `gerado_em`; fora do `tudo`) → sub-aba "Seu gestor".
- O formato do `conteudo` (briefing e ativo) está documentado no próprio `publicar-dashboard.mjs`; se mudar lá, ajuste `anBlocoBriefing`/`anDetalheAtivo`.
