# Compare Mais — Documento Único (SEO, EEAT, Modelos e Escopo)

Consolida: (1) spec de recriação na Hostinger · (2) blueprint de todas as páginas · (3) template da página de produto · (4) modelo 2× com escopo por produto · (5) planilha de captura de specs.
Base: engenharia reversa de `guiaqualcomprar.com.br` + arquitetura do Compare Mais. Regra-mãe: **profundidade honesta e verificável vence volume vazio.**

## Índice
1. Rota de publicação na Hostinger
2. Blueprint de todas as páginas
3. Template da página de produto (SEO + EEAT)
4. Modelo 2× — escopo por produto (com números medidos)
5. Ficha do Artigo (formato de inclusão/edição)
6. Planilha de captura de specs
7. Schema JSON-LD pronto
8. Checklists

---

# 1. Rota de publicação na Hostinger

| Formato (hPanel) | Ranqueia? | Uso |
|---|---|---|
| **WordPress** | ✅ rápido, sem dev | Recriar o modelo do zero |
| **Aplicativos Web (Node.js)** | ✅ para o app | Rodar o Compare Mais (React+Vite SSR+Express) |
| Horizontes | ❌ SPA, SEO fraco | Apps, não conteúdo |
| Construtor de Sites | ⚠️ limitado | Landing/institucional |
| PHP/HTML | ⚠️ cru | Você instalaria WordPress aqui |
| Migrações | ➖ situacional | Só migração |

Node.js exige plano Business/Cloud (ou VPS). Deploy: GitHub (build automático) / ZIP / Connector. Build: Node 22 · `pnpm build` · start `dist/index.js`. **Pendência:** OAuth (Manus) e IA (Forge) não existem fora do Manus — `/admin` e resumo IA precisam de novo provedor antes de dependerem deles. Páginas públicas e SSR rodam normalmente.

---

# 2. Blueprint de todas as páginas

Ordem de rotas: `/admin` · `/busca` · `/categoria/*` · **depois** `/:slug`.

| Rota | Indexar | Schema | Função |
|---|---|---|---|
| `/` | ✅ | WebSite + ItemList | Vitrine + categorias + últimos |
| `/categoria/{slug}` | ✅ | CollectionPage + ItemList | Hub tópico (o concorrente NÃO tem) |
| `/melhor-{produto}` | ✅ | Article+Breadcrumb+ItemList+FAQ | Página-dinheiro |
| `/autores/{slug}` | ✅ | ProfilePage+Person | EEAT |
| `/busca` | ❌ | — | Interno |
| `/sobre` | ✅ | AboutPage+Organization | Trust |
| `/metodologia` | ✅ | WebPage | EEAT (método real) |
| `/contato` | ✅ | ContactPage | Trust |
| `/politica-de-privacidade`, `/termos` | ✅ | WebPage | Legal |
| `/admin` | ❌ | — | Operação |
| `*` (404) | ❌ | — | Recuperação + busca |

**Onde você ganha do concorrente:** categorias-pilar (autoridade tópica), método honesto (EEAT sustentável), preço transparente e CNPJ visível. **Onde ele ganha:** volume publicado. Estratégia: vencer no que ele não tem e escalar com o modelo abaixo.

---

# 3. Template da página de produto (SEO + EEAT)

Ordem dos blocos: Breadcrumb → H1 (keyword exata) → Autor+datas → Box "Como analisamos" → Introdução → **Tabela comparativa** → Critérios → Ranking de produtos → Seções educativas → FAQ → Fontes → Bio do autor → Relacionados → Footer.

**O que corrigir vs o concorrente:**

| Fator | Falha dele | Sua correção |
|---|---|---|
| Experiência (EEAT) | "testado" sem prova | Box "Como analisamos" honesto |
| Dado mensurável | ausente | Tabela com dB/W/dimensão |
| Tabela comparativa | não tem | Obrigatória no topo |
| Preço | oculto | "Faixa estimada — confirme na loja" |
| Autor | persona sem credencial | Nome real + `sameAs` |
| Fontes | zero | Inmetro/Procel/fabricante |
| Arquitetura | tudo na raiz | Categorias + links internos |
| Schema | sem Product/FAQ | JSON-LD completo (seção 7) |

> Nunca marcar `aggregateRating`/estrelas sem nota própria e método real = risco de ação manual por spam de dados estruturados. Use "Veredito" textual.

---

# 4. Modelo 2× — escopo por produto (números MEDIDOS)

Medição real do artigo de 7 produtos do concorrente (corpo editorial, via `wc`/`grep`):

| Métrica | Concorrente | **Nosso padrão 2×** |
|---|---|---|
| Palavras | **2.061** | 4.000–5.000 |
| Produtos | 7 | 12–15 |
| Palavras/produto | ~180 | ~350 |
| FAQ | **8** (não 20) | 16 |
| Seções educativas | 2 | 4 |
| Critérios (lista) | 1 (7 itens) | 2 (12+ itens) |
| Tabela comparativa | 0 | 1 obrigatória |
| Dado mensurável/produto | 0 | ≥3 |
| Fontes | 0 | 2–4 |
| Imagens/produto | 1 | 2 |
| H1 (keyword) | 1 | 1 |
| H2 / H3 | 5 / 7 | 8–10 / 12–15 |
| Densidade keyword-cabeça | ~1,4% | **manter 1–1,5%** |

Densidade medida: keyword-cabeça exata < 1%; o que dá densidade é o campo semântico (motor 2,13%, controle remoto 1,55%, ruído 1,16%). **Copie o princípio, não repita a frase-alvo.**

⚠️ **Dobrar volume, NÃO densidade.** Em 4.000 palavras a 1,4%, a keyword aparece ~56× (não 29×): o percentual é constante, o absoluto cresce junto. Densidade acima de ~2% = stuffing.

## Bloco fixo por produto (~350 palavras)

```markdown
### {{N}}. {{Nome}}: {{keyword secundária}}
**Veredito: {{Melhor no geral | Custo-benefício | Melhor p/ {caso} | Bom e barato}}**
Faixa estimada: R$ {{x}}–{{y}} · Atualizado em {{DD/MM/AAAA}}

![{{alt com keyword}}]({{/img/produtos/slug.webp}})
![{{alt detalhe/uso}}]({{/img/produtos/slug-detalhe.webp}})
[Ver na Amazon]({{link}}) · [Ver no Mercado Livre]({{link}})

**Ficha técnica**
| Spec | Valor |
|---|---|
| {{Dado 1 (ex.: Ruído)}} | {{28 dB}} |
| {{Dado 2 (ex.: Potência)}} | {{30 W}} |
| {{Dado 3 (ex.: Garantia)}} | {{2 anos}} |

{{P1 — PARA QUEM SERVE (~90 palavras)}}
{{P2 — DESEMPENHO COM DADO (~110 palavras)}}
{{P3 — VEREDITO E RESSALVAS: quando NÃO comprar (~90 palavras)}}

**Prós** — 5–6 bullets, ao menos 1 com dado
**Contras** — 3–4 bullets
**Melhor para:** {{1 linha — caso de uso}}
```

## Escopo do artigo (metas de tamanho)

| Bloco | Meta |
|---|---|
| Box "Como analisamos" | ~60 palavras (honesto) |
| Introdução | ~120 palavras |
| Tabela comparativa | 12–15 linhas × 4 specs + preço |
| Critérios de escolha | ~200 + 12 bullets |
| "Erros comuns ao comprar" | ~150 + 5 bullets (o concorrente não tem) |
| Ranking | ~350 × 12–15 produtos |
| 4 seções educativas | ~180–200 cada (tecnologia, funcionalidades, uso, manutenção) |
| FAQ | 16 × ~40 palavras |
| Fontes | 2–4 |
| Bio do autor | ~90 palavras |
| Relacionados | 6 links |

Piso **4.000** / teto ~**6.000** palavras. Calibrar pelo nº de produtos.

## 16 perguntas — 4 tipos (4 de cada)

| Tipo | Gatilho |
|---|---|
| Decisão | "Qual o melhor {produto} para {caso}?" |
| Técnica | "Diferença entre {A} e {B}?" |
| Uso/Prático | "Como instalar/limpar {produto}?" |
| Comercial | "Quanto custa um bom {produto}?" |

Fonte: "As pessoas também perguntam" + autocomplete + dúvidas reais das avaliações.

---

# 5. Ficha do Artigo (formato de inclusão/edição)

Um JSON por artigo. Trocar texto = editar campo; trocar imagem = trocar `imagem`. Sem campo de nota (regra inviolável).

```json
{
  "titulo": "Qual Melhor {{Produto}} {{Modificador}}? {{N}} Opções Analisadas em {{Ano}}",
  "slug": "melhor-{{produto-modificador}}",
  "categoria": "{{slug-categoria}}",
  "meta_description": "{{150–160 caracteres, keyword + diferencial}}",
  "og_image": "/img/og/melhor-{{produto}}.jpg",
  "autor_slug": "{{autor}}",
  "data_publicacao": "AAAA-MM-DD",
  "data_atualizacao": "AAAA-MM-DD",
  "tempo_leitura_min": 15,
  "metodo": "{{honesto — 'análise/curadoria' se não houve teste físico}}",
  "introducao": "{{120 palavras}}",
  "criterios": [{"titulo":"{{}}","texto":"{{}}"}],
  "tabela_comparativa": {"colunas":["Modelo","{{spec}}","Faixa de preço","Melhor para"],"linhas":[["{{}}","{{}}","R$ {{x–y}}","{{}}"]]},
  "produtos": [{
    "posicao":1,"nome":"{{}}","titulo_h3":"{{}}: {{benefício}}",
    "selo":"{{}}","faixa_preco":"R$ {{x}}–{{y}}",
    "imagem":"/img/produtos/{{slug}}.webp","imagem_alt":"{{}}",
    "ficha_tecnica":[{"spec":"{{}}","valor":"{{}}"}],
    "link_amazon":"{{}}","link_mercadolivre":"{{}}",
    "paragrafo_1":"{{}}","paragrafo_2":"{{}}","paragrafo_3":"{{}}",
    "pros":["{{}}"],"contras":["{{}}"],"melhor_para":"{{}}"
  }],
  "secoes_educativas": [{"titulo":"{{}}","texto":"{{}}","bullets":["{{}}"]}],
  "faq": [{"pergunta":"{{}}","resposta":"{{}}"}],
  "fontes": [{"nome":"{{}}","url":"{{}}"}],
  "relacionados": ["{{slug}}"]
}
```

**Fluxo:** preencher a Ficha → subir imagens em `/img/produtos/` e `/img/og/` → colar no `/admin` (resumo IA no editor, Zod) → definir categoria/relacionados → publicar → conferir por `curl` (canonical, ld+json, "Resumo rápido") → validar no Rich Results Test → sitemap + Search Console.

**Imagens:** `.webp` ≤120 KB, caminho `/img/produtos/{slug}.webp`, `alt` com keyword, `width`/`height` sempre (evita CLS), imagem alinhada à loja de destino.

---

# 6. Planilha de captura de specs

Arquivo `.xlsx` separado (`captura-specs-produtos.xlsx`). Estrutura, 1 linha por produto:

| Coluna | Conteúdo |
|---|---|
| # | Posição (1 = melhor) |
| Nome / Marca | Como na loja |
| Slug imagem | `/img/produtos/` |
| Selo | Veredito |
| Spec 1–3 (nome+valor) | ≥3 dados mensuráveis reais |
| Preço mín/máx | Faixa exibida = automática (`R$ mín–máx`) |
| Link Amazon / ML | URLs de afiliado |
| Fonte dos specs | Fabricante/Inmetro/Procel/loja |
| Melhor para | Caso de uso |

Regra: sem número real, deixar em branco — nunca inventar. Cada linha alimenta a "Ficha técnica" do produto.

---

# 7. Schema JSON-LD (um `@graph` por página de produto)

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@graph":[
 {"@type":"Article","headline":"{{título}}","description":"{{meta}}","image":"{{og}}",
  "datePublished":"{{AAAA-MM-DD}}","dateModified":"{{AAAA-MM-DD}}",
  "author":{"@type":"Person","name":"{{autor}}","jobTitle":"{{cargo}}","url":"{{/autores/slug}}","sameAs":["{{linkedin}}"]},
  "publisher":{"@type":"Organization","name":"Compare Mais","logo":{"@type":"ImageObject","url":"{{logo}}"}},
  "mainEntityOfPage":"{{url}}"},
 {"@type":"BreadcrumbList","itemListElement":[
  {"@type":"ListItem","position":1,"name":"Início","item":"{{origin}}"},
  {"@type":"ListItem","position":2,"name":"{{Categoria}}","item":"{{/categoria}}"},
  {"@type":"ListItem","position":3,"name":"{{Título}}","item":"{{url}}"}]},
 {"@type":"ItemList","itemListElement":[
  {"@type":"ListItem","position":1,"item":{"@type":"Product","name":"{{Produto}}","image":"{{img}}",
   "brand":{"@type":"Brand","name":"{{marca}}"},
   "offers":{"@type":"AggregateOffer","priceCurrency":"BRL","lowPrice":"{{x}}","highPrice":"{{y}}","availability":"https://schema.org/InStock","url":"{{link}}"}}}]},
 {"@type":"FAQPage","mainEntity":[
  {"@type":"Question","name":"{{Pergunta}}","acceptedAnswer":{"@type":"Answer","text":"{{Resposta}}"}}]}
]}
</script>
```

Incluir `Review`/`aggregateRating` só com nota e método próprios reais.

---

# 8. Checklists

**Por artigo — On-page**
- [ ] Keyword no slug, H1, title, meta e 1º parágrafo · Title ≤60 · Meta 150–160
- [ ] Tabela comparativa com ≥1 dado mensurável · alt com keyword
- [ ] 3–5 links internos (pilar + irmãos) · 1–2 links externos de autoridade
- [ ] Densidade keyword-cabeça 1–1,5% (medir com `grep -o -i`)

**Por artigo — EEAT**
- [ ] Box "Como analisamos" honesto (sem "testado" falso)
- [ ] Autor real + `sameAs` · Fontes citadas · Disclaimer afiliado visível
- [ ] Faixa de preço "estimada — confirme na loja" · ≥3 specs reais/produto

**Por artigo — Técnico**
- [ ] JSON-LD Article+Breadcrumb+ItemList+FAQ validado no Rich Results Test
- [ ] Canonical absoluto sem barra final · `dateModified` real
- [ ] No sitemap.xml → Search Console · CWV verde (webp, lazy, cache)

**Site (uma vez)**
- [ ] Categorias-pilar com texto-cabeça + tabela + FAQ · malha de links internos
- [ ] `/busca` e `/admin` noindex · metodologia com método real
- [ ] Autores com credencial · CNPJ e contato visíveis
- [ ] `robots.txt` + `sitemap.xml` · `CANONICAL_ORIGIN` sem barra final
- [ ] Rotina trimestral de atualização

---
*Fim. Documento único de referência do Compare Mais.*
